# Azure SQL Managed Instance: Freeing Up Unused Space - Overview 

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com) 
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-01-20

----------

For Azure SQL Managed Instance, consider these strategies:

> - DBCC SHRINKFILE: Shrinks a specific database file by moving data pages and reducing the file size. <br/>
> - DBCC SHRINKFILE (TRUNCATEONLY): Releases unused space at the end of a specific file without moving data pages.
> - DBCC SHRINKDATABASE: Shrinks all data and log files in a database by moving data pages and reducing the overall size. <br/>

## Wiki 

<details>
<summary><b> References </b> (Click to expand)</summary>

- [Microsoft Learn - Maintaining indexes optimally to improve performance and reduce resource utilization](https://learn.microsoft.com/en-us/sql/relational-databases/indexes/reorganize-and-rebuild-indexes?view=sql-server-ver16)
    
</details>

## Content 

<details>
<summary><b> Content </b> (Click to expand)</summary>

- [Wiki](#wiki)
- [Content](#content)
- [Gather more detailed information](#gather-more-detailed-information)
    - [Detailed Space Usage by File](#detailed-space-usage-by-file)
    - [Space Usage by Table](#space-usage-by-table)
    - [Space Usage by Index](#space-usage-by-index)
    - [Database Size and Space Usage](#database-size-and-space-usage)
    - [Filegroup Space Usage](#filegroup-space-usage)
- [Shrink the Database File](#shrink-the-database-file)
- [Monitor the Shrink Operation](#monitor-the-shrink-operation)
- [Check for Active Transactions](#check-for-active-transactions)
- [Check for Long-Running Queries](#check-for-long-running-queries)
- [Shrinking the Database](#shrinking-the-database)
- [Archiving Old Data](#archiving-old-data)
- [Removing Unused Indexes](#removing-unused-indexes)
- [Using Filegroups](#using-filegroups)
- [Fragmentation](#fragmentation)
    - [Measuring Fragmentation](#measuring-fragmentation)
    - [How to resolve it](#how-to-resolve-it)
    - [Automating Maintenance in Azure SQL Managed Instance](#automating-maintenance-in-azure-sql-managed-instance)
    
</details>


## Gather more detailed information

> Gather more detailed information about the current used and allocated space in your database

### Detailed Space Usage by File

> This query provides detailed information about each file, including the file name, type, growth settings, and more:

  ```sql
  WITH CTE AS (
      SELECT 
          file_id,
          name AS file_name,
          type_desc AS file_type,
          physical_name,
          CAST(FILEPROPERTY(name, 'SpaceUsed') AS bigint) * 8 / 1024.0 AS space_used_mb,
          CAST(size AS bigint) * 8 / 1024.0 AS space_allocated_mb,
          CAST(max_size AS bigint) * 8 / 1024.0 AS max_size_mb,
          growth,
          CASE 
              WHEN is_percent_growth = 1 THEN 'Percentage'
              ELSE 'MB'
          END AS growth_type
      FROM sys.database_files
  )
  SELECT 
      file_id,
      file_name,
      file_type,
      physical_name,
      space_used_mb,
      space_allocated_mb,
      max_size_mb,
      growth,
      growth_type,
      space_used_mb / space_allocated_mb * 100 AS [Occupancy %],
      100 - (space_used_mb / space_allocated_mb * 100) AS [Free %]
  FROM CTE
  ORDER BY [Occupancy %];
  ```

<img width="700" alt="image" src="https://github.com/user-attachments/assets/b6ca6507-668c-427c-b01a-6a66e7e0fedd" />

| **Category**       | **Recommendation**                                                                                                                                                                                                 |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **LOG Files**      | - **Free Space**: Maintain at least 25-30% free space in your log files. This ensures there is enough room for transaction logs to grow and prevents the database from running out of space during peak operations.<br>- **Monitoring**: Use the `sys.dm_db_log_space_usage`. Regularly check the percentage of log space used to avoid unexpected issues.<br>- **Maintenance**: Regularly back up your transaction logs to truncate inactive portions and free up space. |
| **ROWS (Data Files)** | - **Free Space**: Aim to keep around 20-25% free space in your data files. This allows for growth and helps avoid performance issues related to frequent auto-growth events.<br>- **Auto-Growth Settings**: Configure auto-growth settings appropriately to avoid frequent small growths. Setting a fixed size for growth (e.g., 500 MB or 1 GB) is often better than a percentage-based growth.<br>- **Monitoring**: Use the `sys.database_files` view to monitor the size and free space of your data files. |
| **FILESTREAM Data** | - **Free Space**: Ensure there is sufficient free space on the disk where the FILESTREAM data is stored. A good rule of thumb is to keep at least 20% free space.<br>- **Disk Monitoring**: Regularly monitor the disk space and set up alerts to notify you when free space falls below a certain threshold.<br>- **Maintenance**: Regularly clean up old or unused FILESTREAM data to free up space. |

### Space Usage by Table

> This query provides information about space usage at the table level, including the number of rows, reserved space, data space, index space, and unused space. Will iterate through all tables in your database and execute sp_spaceused for each one:
  
  ```sql
  -- Create a temporary table to store the results
  CREATE TABLE #SpaceUsed (
      TableName NVARCHAR(256),
      [Rows] INT,
      Reserved VARCHAR(50),
      Data VARCHAR(50),
      IndexSize VARCHAR(50),
      Unused VARCHAR(50),
      [Free %] FLOAT
  );
  
  DECLARE @TableName NVARCHAR(256);
  
  DECLARE TableCursor CURSOR FOR
  SELECT QUOTENAME(SCHEMA_NAME(schema_id)) + '.' + QUOTENAME(name)
  FROM sys.tables;
  
  OPEN TableCursor;
  FETCH NEXT FROM TableCursor INTO @TableName;
  
  WHILE @@FETCH_STATUS = 0
  BEGIN
      INSERT INTO #SpaceUsed (TableName, [Rows], Reserved, Data, IndexSize, Unused)
      EXEC sp_spaceused @TableName;
  
      FETCH NEXT FROM TableCursor INTO @TableName;
  END;
  
  CLOSE TableCursor;
  DEALLOCATE TableCursor;
  
  -- Use a CTE to calculate the Free %
  WITH CTE AS (
      SELECT 
          TableName,
          [Rows],
          CAST(REPLACE(Reserved, ' KB', '') AS FLOAT) AS ReservedKB,
          CAST(REPLACE(Data, ' KB', '') AS FLOAT) AS DataKB,
          CAST(REPLACE(IndexSize, ' KB', '') AS FLOAT) AS IndexSizeKB,
          CAST(REPLACE(Unused, ' KB', '') AS FLOAT) AS UnusedKB
      FROM #SpaceUsed
  )
  UPDATE #SpaceUsed
  SET [Free %] = 
      CASE 
          WHEN ReservedKB = 0 THEN 0
          ELSE (UnusedKB / ReservedKB) * 100
      END
  FROM CTE
  WHERE #SpaceUsed.TableName = CTE.TableName;
  
  -- Select the results from the temporary table
  SELECT * FROM #SpaceUsed
  ORDER BY TableName;
  
  -- Drop the temporary table
  DROP TABLE #SpaceUsed;
  ```

<img width="550" alt="image" src="https://github.com/user-attachments/assets/401323a7-7ffc-4d6f-aade-96991793b677" />

| **Aspect**            | **Recommendation**|
|-----------------------|---------------------------------------------------|
| **Free Space**        | Maintain around 20-25% free space in your data files to accommodate table growth.|
| **Index Maintenance** | Regularly rebuild or reorganize indexes to optimize performance and reclaim space. Fragmented indexes can lead to inefficient space usage.|
| **Partitioning**      | Consider partitioning large tables to improve manageability and performance. This can also help in efficiently managing space.|
| **Archiving**         | Implement an archiving strategy for old or infrequently accessed data. This can free up space and improve performance for active data.|
| **Compression**       | Use data compression techniques to reduce the size of tables and indexes. SQL Server supports row and page compression, which can significantly reduce space usage.|

### Space Usage by Index

> This query provides detailed information about space usage by indexes, including the index name, type, and space used.

  ```sql
  SELECT 
      OBJECT_NAME(i.object_id) AS table_name,
      i.name AS index_name,
      i.type_desc AS index_type,
      SUM(a.used_pages) * 8 / 1024.0 AS index_size_mb
  FROM 
      sys.indexes AS i
      JOIN sys.partitions AS p ON i.object_id = p.object_id AND i.index_id = p.index_id
      JOIN sys.allocation_units AS a ON p.partition_id = a.container_id
  GROUP BY 
      i.object_id, i.index_id, i.name, i.type_desc
  ORDER BY 
      index_size_mb DESC;
  ```

<img width="550" alt="image" src="https://github.com/user-attachments/assets/9e73aa43-59a8-412a-b8e1-757478050b8c" />

### Database Size and Space Usage

> This query provides an overview of the database size and space usage, including the total size, used space, and free space.
    
  ```sql
  WITH SpaceInfo AS (
      SELECT 
          file_id,
          type_desc,
          name AS file_name,
          physical_name,
          size * 8 / 1024 AS size_mb,
          FILEPROPERTY(name, 'SpaceUsed') * 8 / 1024 AS space_used_mb
      FROM 
          sys.database_files
  )
  SELECT 
      db_name.database_name,
      SUM(size_mb) AS total_size_mb,
      SUM(space_used_mb) AS used_space_mb,
      SUM(size_mb) - SUM(space_used_mb) AS free_space_mb
  FROM 
      SpaceInfo,
      (SELECT DB_NAME() AS database_name) AS db_name
  GROUP BY 
      db_name.database_name;
  ```

<img width="550" alt="image" src="https://github.com/user-attachments/assets/bd6cbfa5-aec0-48d6-a8dc-440023bca0d0">

### Filegroup Space Usage

> This query provides information about space usage by filegroups, including the filegroup name, total size, used space, and free space.
  
  ```sql
  -- Calculate the total size, used space, and free space for each filegroup
  SELECT 
      fg.name AS filegroup_name,
      SUM(df.size * 8 / 1024.0) AS total_size_mb,
      SUM(df.size * 8 / 1024.0) - SUM(a.total_pages * 8 / 1024.0) AS free_space_mb,
      SUM(a.total_pages * 8 / 1024.0) AS used_space_mb
  FROM 
      sys.filegroups AS fg
  JOIN 
      sys.database_files AS df ON fg.data_space_id = df.data_space_id
  JOIN 
      sys.allocation_units AS a ON df.data_space_id = a.data_space_id
  GROUP BY 
      fg.name
  ORDER BY 
      total_size_mb DESC;
  ```

<img width="550" alt="image" src="https://github.com/user-attachments/assets/a7dce4f9-f32e-4b7e-bd92-d4709bd0ed7b">

## Shrink the Database File

> [!TIP]
> Shrink files in parallel by opening multiple database sessions and running the `DBCC SHRINKFILE` command on each session with a different `file_id` value.

> Shrink the database file to reclaim unused space

| **Command**                      | **Description**                                                                 | **Syntax**                                                                                   | **Example**                                                                                   |
|----------------------------------|---------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------|
| **DBCC SHRINKFILE**              | DBCC SHRINKFILE is used to shrink the size of a specific database file. This command attempts to move data pages from the end of the file to unoccupied space closer to the beginning of the file, thereby reducing the file size.            | `DBCC SHRINKFILE (file_id, target_size_in_MB);`                                              | `DBCC SHRINKFILE (1, 100);` -- Shrinks the file with ID 1 to 100 MB                       |
| **DBCC SHRINKFILE (TRUNCATEONLY)** | DBCC SHRINKFILE (TRUNCATEONLY) is a specific option for DBCC SHRINKFILE that releases all free space at the end of the file to the operating system without moving any data pages. This command is useful when you want to quickly release unused space without the overhead of moving data. | `DBCC SHRINKFILE (file_id, TRUNCATEONLY);`                                                   | `DBCC SHRINKFILE (1, TRUNCATEONLY);` -- Releases unused space at the end of the file with ID 1 |


```sql
-- Shrink the database file (replace 1 with your file_id)
DBCC SHRINKFILE (1);
```

  <img width="550" alt="image" src="https://github.com/user-attachments/assets/96c7be25-ade3-4851-a2cd-8735273c4c6f">

> If you specify a target size that is just enough to hold all the data pages, the result can be a file with no free space.

**Before Shrink:**

| $${\color{red}\text{Data Page}}$$ | $${\color{red}\text{Data Page}}$$ | $${\color{green}\text{Free Space}}$$ | $${\color{red}\text{Data Page}}$$ | $${\color{green}\text{Free Space}}$$ | $${\color{green}\text{Free Space}}$$ |

- **After Shrink with TRUNCATEONLY:** When you use DBCC SHRINKFILE with the TRUNCATEONLY option `DBCC SHRINKFILE (file_id, TRUNCATEONLY)`, it releases the unused space at the end of the file without moving any data pages. This means that the data pages remain in their original locations, and only the free space at the end of the file is released.

  | $${\color{red}\text{Data Page}}$$ | $${\color{red}\text{Data Page}}$$ | $${\color{green}\text{Free Space}}$$ | $${\color{red}\text{Data Page}}$$ |

  > If you don't move the pages, the space within the file might not be optimized because the data pages could be scattered throughout the file, leaving gaps of unused space in between. This can lead to fragmentation, where the data is not stored contiguously, potentially affecting performance. In this case, the free space at the end is released, but the data pages remain scattered, which might not be optimal for performance.

- After `DBCC SHRINKFILE (file_id, target_size_in_MB)`: In this case, the data pages are moved to fill the gaps, and the file is shrunk to the target size, eliminating free space.

    > The `target_percent_free_space`: parameter `defines the desired final size of the file after the shrink operation`. It indicates the final size in megabytes. For instance, setting target_size_in_MB to 2000 will reduce the file to 2000 MB. 

    | $${\color{red}\text{Data Page}}$$ | $${\color{red}\text{Data Page}}$$ | $${\color{red}\text{Data Page}}$$ |

> [!IMPORTANT]
> - After each shrink operation, monitor the file size and fragmentation. <br/>
> - Repeat the shrinking process in increments until you reach your desired target size.

## Monitor the Shrink Operation

> While the shrink operation is running, you can monitor for any blocking operations that might be affecting the process.

  ```sql
  -- Check for blocking operations
  SELECT 
      blocking_session_id, 
      wait_type, 
      wait_time, 
      wait_resource
  FROM 
      sys.dm_exec_requests
  WHERE 
      blocking_session_id <> 0;
  ```

 
 <img width="350" alt="image" src="https://github.com/user-attachments/assets/0d724ca6-8ac1-478b-820d-7ae124af8937" />

## Check for Active Transactions

> Ensure there are no active transactions that might be preventing the shrink operation from completing.

 ```sql
 -- Check for active transactions
  DBCC OPENTRAN;
 ```

 <img width="350" alt="image" src="https://github.com/user-attachments/assets/5c64c734-4999-40a2-8333-40090e88e37b">

## Check for Long-Running Queries

> Identify any long-running queries that might be affecting the performance.

  ```sql
  -- Check for long-running queries
  SELECT 
      session_id, 
      start_time, 
      status, 
      command, 
      wait_type, 
      wait_time, 
      blocking_session_id
  FROM 
      sys.dm_exec_requests
  WHERE 
      status = 'running'
  ORDER BY
  ```

 <img width="550" alt="image" src="https://github.com/user-attachments/assets/da27cedb-e113-4127-85c4-1ab10b9b09e6">

## Shrinking the Database

> Reclaim unused space with. Shrink the entire database to leave `target_percent_free_space`% free space.

| **Command**                      | **Description**                                                                 | **Syntax**                                                                                   | **Example**                                                                                   |
|----------------------------------|---------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------|
| **DBCC SHRINKDATABASE**          | DBCC SHRINKDATABASE is used to shrink the size of all data and log files in a database. This command attempts to move data pages from the end of the files to unoccupied space closer to the beginning of the files, thereby reducing the overall size of the database. `target_percent_free_space: The desired percentage of free space to remain in the database after the shrink operation.`  | `DBCC SHRINKDATABASE (database_name, target_percent_free_space);`                             | `DBCC SHRINKDATABASE (YourDatabaseName, 10);` -- Shrinks the database to leave 10% free space |


 ```sql
 DBCC SHRINKDATABASE (YourDatabaseName, 10);
 ```
 
  **Before Shrink:**
  
  | $${\color{red}\text{Data Page}}$$ | $${\color{red}\text{Data Page}}$$ | $${\color{green}\text{Free Space}}$$ | $${\color{red}\text{Data Page}}$$ | $${\color{green}\text{Free Space}}$$ | $${\color{green}\text{Free Space}}$$ |
  
  After `DBCC SHRINKDATABASE (database_name, target_percent_free_space)`: The data pages are moved to reduce fragmentation, and the file is shrunk to maintain a small percentage of free space.
  
  | $${\color{red}\text{Data Page}}$$ | $${\color{red}\text{Data Page}}$$ | $${\color{red}\text{Data Page}}$$ | $${\color{green}\text{Free Space}}$$ |

 <img width="550" alt="image" src="https://github.com/user-attachments/assets/f906adcd-732e-4efa-849c-90d8fed2e9d3">

 To check for blocking operations:
 ```sql
 SELECT blocking_session_id, wait_type, wait_time, wait_resource
 FROM sys.dm_exec_requests
 WHERE blocking_session_id <> 0;
 ```

## Archiving Old Data

> Move old data to an archive database using SQL Server's built-in tools or third-party solutions.

## Removing Unused Indexes

> Identify and remove indexes that are not being used.

 ```sql
 SELECT * FROM sys.dm_db_index_usage_stats WHERE user_seeks = 0 AND user_scans = 0 AND user_lookups = 0;
 ```

<img width="550" alt="image" src="https://github.com/user-attachments/assets/8e9dfe79-c4a7-40c8-9ae8-7210c35eb6f1">

## Using Filegroups

> Distribute objects across multiple filegroups to improve performance and manageability:

 ```sql
 CREATE TABLE YourTableName (...) ON [PrimaryFileGroup];
 ```

## Fragmentation 

> `Fragmentation` in Azure SQL Managed Instance, like in other SQL Server environments, refers to the `condition where the logical order of data pages in an index does not match the physical order on the disk`. This can lead to inefficient data retrieval and increased I/O operations. Fragmentation is generally categorized into two types: **internal fragmentation** and **external fragmentation**.

| Type of Fragmentation | Definition | Cause | Impact | Example |
|-----------------------|------------|-------|--------|---------|
| **Internal Fragmentation** | Unused space within index pages. | Typically caused by page splits, where a page is only partially filled after an insert or update operation. | Leads to wasted space and can reduce the efficiency of data storage. | A page split occurs when a new row is inserted into a full page, causing SQL Server to split the page into two, each partially filled. |
| **External Fragmentation** | Logical order of pages does not match the physical order on the disk. | Caused by frequent inserts, updates, and deletes that result in pages being out of order. | Causes the disk head to move more frequently, slowing down data access and increasing I/O operations. | When rows are inserted or updated, they may be placed in different physical locations, causing the logical sequence of pages to be disrupted. |

### Measuring Fragmentation

> Azure SQL Managed Instance provides the `sys.dm_db_index_physical_stats` dynamic management function to measure fragmentation. This function returns information about the physical storage of indexes, including the average fragmentation percentage.

Key Metrics:
- **avg_fragmentation_in_percent**: Indicates the percentage of logical fragmentation in the index. Higher values suggest more fragmentation.
- **page_count**: The number of pages in the index. Larger indexes with high fragmentation can significantly impact performance.

### How to resolve it 

1. **Rebuild Indexes**:
   - **Command**: `ALTER INDEX [IndexName] ON [SchemaName].[TableName] REBUILD;`
   - **Effect**: Drops and re-creates the index, removing fragmentation and compacting the pages.
2. **Reorganize Indexes**:
   - **Command**: `ALTER INDEX [IndexName] ON [SchemaName].[TableName] REORGANIZE;`
   - **Effect**: Defragments the leaf level of the index pages without dropping the index.
3. **Set Fill Factor**:
   - **Definition**: The fill factor setting determines how much space to leave free on each page during index creation or rebuild.
   - **Impact**: A lower fill factor can reduce fragmentation but may increase the number of pages.

### Automating Maintenance in Azure SQL Managed Instance

1. **Analyze Fragmentation**:  Use the following query to get detailed fragmentation information.

     ```sql
     SELECT 
         S.name AS 'Schema', 
         T.name AS 'Table', 
         I.name AS 'Index', 
         I.type_desc AS 'Index Type',
         DDIPS.index_type_desc AS 'Index Level',
         DDIPS.alloc_unit_type_desc AS 'Allocation Unit Type',
         DDIPS.avg_fragmentation_in_percent AS 'Fragmentation (%)', 
         DDIPS.page_count AS 'Page Count',
         (DDIPS.page_count * 8 / 1024) AS 'Index Size (MB)'
     FROM 
         sys.dm_db_index_physical_stats(DB_ID(), NULL, NULL, NULL, 'DETAILED') AS DDIPS
     INNER JOIN 
         sys.tables T ON T.object_id = DDIPS.object_id 
     INNER JOIN 
         sys.schemas S ON T.schema_id = S.schema_id 
     INNER JOIN 
         sys.indexes I ON I.object_id = DDIPS.object_id
     WHERE 
         DDIPS.index_id > 0
     ORDER BY 
         DDIPS.avg_fragmentation_in_percent DESC;
     ```
    
    <img width="550" alt="image" src="https://github.com/user-attachments/assets/78a0afbb-c110-4a66-8ebd-0c79ef30485f" />

2. **Rebuild or Reorganize Indexes**:

   - **Rebuild Indexes**: Drops and re-creates the index, removing fragmentation and compacting the pages.

     ```sql
     ALTER INDEX [IndexName] ON [SchemaName].[TableName] REBUILD;
     ```
     > E.g `ALTER INDEX [PK__People__3214EC27785B7549] ON [dbo].[People] REBUILD;`

    | Before Rebuilt index | After REBUILD| 
    | --- | --- |
    | <img width="550" alt="image" src="https://github.com/user-attachments/assets/78a0afbb-c110-4a66-8ebd-0c79ef30485f" /> | <img width="550" alt="image" src="https://github.com/user-attachments/assets/500f677b-5a2b-4616-a23b-01c0c6d86860" /> | 

   - **Reorganize Indexes**: Defragments the leaf level of the index pages without dropping the index.

    > E.g `ALTER INDEX [PK__RandomDa__3214EC2723C2100E] ON [dbo].[RandomData] REORGANIZE;`
     ```sql
     ALTER INDEX [IndexName] ON [SchemaName].[TableName] REORGANIZE;
     ```

    | Before Reorganize index | After REORGANIZE| 
    | --- | --- |
    | <img width="550" alt="image" src="https://github.com/user-attachments/assets/06baace1-33eb-4b7b-b7a6-28e4afe9e232" />  | <img width="650" alt="image" src="https://github.com/user-attachments/assets/64ce01bb-adb3-4f4a-81dc-4a93b9579023" /> | 


   
<div align="center">
  <h3 style="color: #4CAF50;">Total Visitors</h3>
  <img src="https://profile-counter.glitch.me/brown9804/count.svg" alt="Visitor Count" style="border: 2px solid #4CAF50; border-radius: 5px; padding: 5px;"/>
</div>

