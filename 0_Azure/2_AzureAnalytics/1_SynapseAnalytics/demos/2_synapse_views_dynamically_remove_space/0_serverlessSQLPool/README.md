# Serverless SQL Pool: Dynamically Remove Space

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com) 
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-01-26

----------

<details>
<summary><b>Table of Content </b> (Click to expand)</summary>

- [Content](#content)
- [Overview](#overview)
- [Demo](#demo)
   - [Set Up a Synapse Workspace](#set-up-a-synapse-workspace)
   - [Upload Sample Data to Storage Account](#upload-sample-data-to-storage-account)
   - [Create User Database](#create-user-database)
   - [Create an External Data Source and File Format](#create-an-external-data-source-and-file-format)
   - [Create an External Table](#create-an-external-table)
   - [Create Views with Modified Tables/Column Names](#create-views-with-modified-tablescolumn-names)

</details>

## Overview 

> [!IMPORTANT]
> The serverless SQL pool in Azure Synapse Analytics `does not support internal tables. It primarily supports external tables and temporary tables`.
> For `internal tables,` you would need to use a `dedicated SQL pool` in Synapse Analytics, which allows you to `create and manage internal tables with local storage`.

| **Table Type**      | **Description**                                                                                                                                                                                                 | **Use Cases**                                                                                                      |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------|
| **External Tables** | - Reference data stored in external sources like Azure Data Lake Storage, Azure Blob Storage, Azure Cosmos DB, etc. <br> - Data is not physically stored in the SQL pool. <br> - Useful for querying large datasets without loading them into the SQL pool. | - Querying large datasets stored externally. <br> - Performing data analysis on data stored in various formats.    |
| **Temporary Tables**| - Created and used within the scope of a session. <br> - Data is stored temporarily and is dropped when the session ends. <br> - Useful for intermediate data processing and transformations.                      | - Storing intermediate results during complex queries. <br> - Performing temporary data transformations and aggregations. |


## Demo

### Set Up a Synapse Workspace

1. **Sign in to the Azure Portal**: Go to the Azure Portal and sign in with your Azure account.
2. **Navigate to Your Synapse Workspace**: In the Azure Portal, search for your Synapse workspace or create a new one if you don't have one.

     <img width="550" alt="image" src="https://github.com/user-attachments/assets/92a5e451-1868-47e2-b32b-858591c306ee" />
  
     <img width="550" alt="image" src="https://github.com/user-attachments/assets/51e3b091-855d-4481-89e0-623705e3cf2a" />

     <img width="550" alt="image" src="https://github.com/user-attachments/assets/7d03bfa8-e1e3-4706-970f-a89c7b8cd904" />

3. **Launch Synapse Studio**: From the Synapse workspace overview, click on the `Open Synapse Studio` button.

     <img width="550" alt="image" src="https://github.com/user-attachments/assets/302b1fd8-49a6-427e-93dc-8e952f1667e6" />

     <img width="550" alt="image" src="https://github.com/user-attachments/assets/a368036b-c859-47fc-a1c5-d045b6910790" />

### Upload Sample Data to Storage Account 

> [!IMPORTANT]
> For this demo, `we'll be using the same storage account created with the synpase workspace`.
> `CREATE EXTERNAL DATA SOURCE is not supported in the master database of the serverless` SQL pool. Instead, you `need to create a user database and perform the operations there`.

1. Create a Container in the Storage Account:
   - Go to the Azure portal and navigate to your storage account.
   - In the left-hand menu, select `Containers`.
   - Click on `+ Container` to create a new container.
   - Enter a name for the container, such as `sample-tables-container`.
   - Set the `Public access level` to your preference (e.g., Private).
   - Click `Create`.

        <img width="550" alt="image" src="https://github.com/user-attachments/assets/3060045f-a515-4a27-a4c6-80bd2ba3d9ab" />

2. Navigate to the Container:
   - In the Azure portal, go to your storage account.
   - Select `Containers` from the left-hand menu.
   - Click on the container you created (e.g., `sample-tables-container`).
3. Upload the Sample CSV File:
   - Click on the `Upload` button.
   - In the upload blade, click on `Browse` to select the sample CSV file from your local machine.
   - Choose the file, click `Upload` to upload the file to the container.

        <img width="550" alt="image" src="https://github.com/user-attachments/assets/4fa8d1c8-e5a0-4d65-a3b5-83bf7c7118c1" />

### Create User Database

1. First, create a new database in your Synapse workspace.

     ```sql
     CREATE DATABASE {User Database Name};
     ```

     <img width="884" alt="image" src="https://github.com/user-attachments/assets/f24a4d45-6bee-46ea-bccc-b5f893044c01" />

2. Switch to the User Database: Use the newly created database.
   
### Create an External Data Source and File Format

1. Integrate this task with the previous step by establishing the external data source within the user database.

     ```sql
     USE {User Database Name};

     CREATE EXTERNAL DATA SOURCE {Data Source Name}
     WITH (
         LOCATION = 'https://<your-storage-account>.dfs.core.windows.net/<your-container>/'
     );
     ```

     <img width="550" alt="image" src="https://github.com/user-attachments/assets/13f22e3b-7c68-4ed2-8a56-2752a5033869" />


2. **Create an External File Format**: As part of the same flow, define the format of the CSV file.

     ```sql
     CREATE EXTERNAL FILE FORMAT {File Format Name}
     WITH (
         FORMAT_TYPE = DELIMITEDTEXT,
         FORMAT_OPTIONS (
             FIELD_TERMINATOR = ',',
             STRING_DELIMITER = '"',
             FIRST_ROW = 2
         )
     );
     ```

     <img width="550" alt="image" src="https://github.com/user-attachments/assets/40a4c6a2-bc51-49ba-9361-bec6eb0edb9e" />


### Create an External Table

1. Create an external table that references the sample data.

     ```sql
     CREATE EXTERNAL TABLE [Table Name] (
         [Employee ID] INT,
         [Employee Name] NVARCHAR(50),
         [Hire Date] DATE
     )
     WITH (
         LOCATION = 'employee data with spaces.csv',
         DATA_SOURCE = {Data Source Name},
         FILE_FORMAT = {File Format Name}
     );
     
     CREATE EXTERNAL TABLE [Table Name] (
         [Product ID] INT,
         [Product Name] NVARCHAR(50),
         [Release Date] DATE
     )
     WITH (
         LOCATION = 'product data with spaces.csv',
         DATA_SOURCE = {Data Source Name},
         FILE_FORMAT = {File Format Name}
     );
     ```
     
     <img width="550" alt="image" src="https://github.com/user-attachments/assets/841cc8b7-4c2d-4c9a-975c-fec4bb3326d8" />

2. Confirm the existence of the tables 
     
     ```sql 
     SELECT * FROM sys.tables 
     WHERE name IN ('Product Data', 'Employee Data');
     ```

     <img width="240" alt="image" src="https://github.com/user-attachments/assets/9eb9e379-30a7-42b8-966d-8f8c96b31395" />


3. **Query the External Table**:  You can now query the external table to see the sample data.

     ```sql
     SELECT * FROM {Table Name};
     ```

### Create Views with Modified Tables/Column Names

> This script is designed to dynamically create views for each table in a database, renaming columns to remove spaces. It starts by creating a temporary table to store the SQL statements and assigns a unique row number to each statement. The script then loops through these statements, executing each one in turn. Finally, it cleans up by dropping the temporary table.
> 1. **Temporary Table Creation**: A temporary table `#CreateViewStatements` is created to store the dynamic SQL statements and their corresponding row numbers. <br/>
> 2. **Inserting SQL Statements**: The script generates SQL statements to create views for each table in the database. It uses the `INFORMATION_SCHEMA.COLUMNS` to get the table and column names, renaming columns to remove spaces. These statements, along with a row number, are inserted into the temporary table. <br/>
> 3. **Variable Declaration**: Variables are declared to hold the current SQL statement, the current row number, and the maximum row number. <br/>
> 4. **Getting Maximum Row Number**: The script retrieves the maximum row number from the temporary table to determine how many statements need to be executed. <br/>
> 5. **Executing SQL Statements**: A loop iterates through each row in the temporary table, retrieves the SQL statement, executes it, and increments the row number until all statements are executed. <br/>
> 6. **Cleanup**: The temporary table is dropped to clean up after the script has finished executing. <br/>

```sql
-- Create a temporary table to store the dynamic SQL statements
CREATE TABLE #CreateViewStatements (SQLStatement NVARCHAR(MAX), RowNum INT);

-- Insert dynamic SQL statements for each table with a row number
INSERT INTO #CreateViewStatements (SQLStatement, RowNum)
SELECT 
    'CREATE VIEW ' + QUOTENAME(REPLACE(TABLE_NAME, ' ', '_')) + ' AS SELECT ' +
    STRING_AGG('[' + COLUMN_NAME + '] AS [' + REPLACE(COLUMN_NAME, ' ', '') + ']', ', ') +
    ' FROM ' + QUOTENAME(TABLE_NAME),
    ROW_NUMBER() OVER (ORDER BY TABLE_NAME)
FROM INFORMATION_SCHEMA.COLUMNS
GROUP BY TABLE_NAME;

-- Declare variables to hold the SQL statement and row number
DECLARE @sql NVARCHAR(MAX);
DECLARE @rowNum INT = 1;
DECLARE @maxRowNum INT;

-- Get the maximum row number
SELECT @maxRowNum = MAX(RowNum) FROM #CreateViewStatements;

-- Loop through the temporary table and execute each SQL statement
WHILE @rowNum <= @maxRowNum
BEGIN
    -- Get the next SQL statement
    SELECT @sql = SQLStatement FROM #CreateViewStatements WHERE RowNum = @rowNum;

    -- Execute the SQL statement
    EXEC sp_executesql @sql;

    -- Increment the row number
    SET @rowNum = @rowNum + 1;
END;

-- Drop the temporary table
DROP TABLE #CreateViewStatements;
```


<img width="550" alt="image" src="https://github.com/user-attachments/assets/2654dcb8-d843-4000-9b32-b36f14f2a7a8" />

<img width="550" alt="image" src="https://github.com/user-attachments/assets/6f270523-adf1-4ca3-b80c-b5decd624459" />

<img width="550" alt="image" src="https://github.com/user-attachments/assets/7a5a26ff-9a5f-4c98-a337-b64ce0cc1699" />
   
<div align="center">
  <h3 style="color: #4CAF50;">Total Visitors</h3>
  <img src="https://profile-counter.glitch.me/brown9804/count.svg" alt="Visitor Count" style="border: 2px solid #4CAF50; border-radius: 5px; padding: 5px;"/>
</div>
