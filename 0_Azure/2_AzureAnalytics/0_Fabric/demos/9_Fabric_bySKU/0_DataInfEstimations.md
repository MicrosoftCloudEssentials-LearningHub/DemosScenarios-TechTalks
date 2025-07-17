# Fabric: Data Information Estimations - Overview  

Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-01-20

------------------------------------------


## Wiki 

<details>
<summary><b>Table of References </b> (Click to expand)</summary>

- [Understanding the data processing capability](https://learn.microsoft.com/en-us/data-engineering/playbook/capabilities/data-processing/)
- [SQL database in Microsoft Fabric (Preview)](https://learn.microsoft.com/en-us/fabric/database/sql/overview)
- [Microsoft Fabric features parity](https://learn.microsoft.com/en-us/fabric/enterprise/fabric-features)

</details>

## Content

<details>
<summary><b>Table of Contents </b> (Click to expand)</summary>

- [Wiki](#wiki)
- [Content](#content)
- [Total Size of Data When Compressed](#total-size-of-data-when-compressed)
- [Number of Daily Batch Cycles](#number-of-daily-batch-cycles)
- [Number of Distinct Source Entities/Tables/Data Sets](#number-of-distinct-source-entitiestablesdata-sets)
- [Number of SQL Analytics Users](#number-of-sql-analytics-users)

</details>

## Total Size of Data When Compressed

> Data compression is the process of encoding information using fewer bits than the original representation. This can be achieved through various algorithms that reduce the size of data files without changing their fundamental properties. Compression can be either lossless (no data is lost) or lossy (some data is lost to reduce size further). In the context of data storage, compressing data helps minimize the storage capacity required and reduces costs.

$$
\text{Compressed Size (GiB)} = \frac{\text{Logical Size (GiB)}}{6}
$$

> Example:

$$
\text{Logical Size} = 150 \text{ TB}
$$
$$
\text{Conversion to GiB} = 150 \times 1024 = 153,600 \text{ GiB} 
$$
$$
\text{Compressed Size} = \frac{153,600}{6} = 25,600 \text{ GiB}
$$

## Number of Daily Batch Cycles

> Batch processing refers to the execution of batch jobs where data is collected, stored, and processed in batches at scheduled intervals. This approach is efficient for handling large volumes of data and repetitive tasks. A batch cycle represents a complete run of the batch processing workflow. The number of daily batch cycles depends on how frequently the batch jobs are executed.

$$ 
\text{Number of Daily Batch Cycles} = \frac{\text{Total Minutes in a Day}}{\text{Frequency (minutes)}} 
$$


| **Scenario**       | **Frequency** | **Total Minutes in a Day** | **Number of Daily Batch Cycles** |
|--------------------|---------------|----------------------------|----------------------------------|
| High Frequency     | Every 10 minutes | 1440 minutes               | $$\frac{1440 \text{ minutes}}{10 \text{ minutes}} = 144$$        |
| Moderate Frequency | Every 30 minutes | 1440 minutes               | $$\frac{1440 \text{ minutes}}{30 \text{ minutes}} = 48$$         |
| Low Frequency      | Every 60 minutes (hourly) | 1440 minutes               | $$\frac{1440 \text{ minutes}}{60 \text{ minutes}} = 24$$         |
| Every 4 Hours      | Every 240 minutes (4 hours) | 1440 minutes               | $$\frac{1440 \text{ minutes}}{240 \text{ minutes}} = 6$$         |
| Every 6 Hours      | Every 360 minutes (6 hours) | 1440 minutes               | $$\frac{1440 \text{ minutes}}{360 \text{ minutes}} = 4$$         |
| Every 12 Hours     | Every 720 minutes (12 hours)| 1440 minutes               | $$\frac{1440 \text{ minutes}}{720 \text{ minutes}} = 2$$         |

## Number of Distinct Source Entities/Tables/Data Sets

Data Warehouse componenets: 

| **Category**       | **Description**                                                                                                                                       | **Formula**                                      | **Example**                                      |
|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------|--------------------------------------------------|
| Jobs               | Individual tasks or processes that perform specific data operations within the data warehouse. They can include ETL tasks, data validation, and data transformation. | \(\text{Jobs} \times \text{Average Tables per Job}\) | 250 jobs * 2.5 tables/job = 625 tables           |
| Packages           | Collections of related tasks executed together to achieve a specific data processing goal. They often bundle multiple ETL tasks to streamline data processing workflows. | \(\text{Packages} \times \text{Average Tables per Package}\) | 1,200 packages * 7.5 tables/package = 9,000 tables |
| Cubes              | Multidimensional data structures used for efficient querying and analysis. They allow users to perform complex queries and aggregations across multiple dimensions, such as time, geography, and product categories. | \(\text{Cubes} \times \text{Average Tables per Cube}\) | 50 cubes * 12.5 tables/cube = 625 tables         |
| Unique Databases   | Distinct databases within the data warehouse environment. Each database is considered a separate entity, containing its own set of tables and data structures. | N/A                                              | 150 unique databases                             |

## Hours for Daily Dataflow Gen2 ETL Operations

> ETL (Extract, Transform, Load) operations involve extracting data from source systems, transforming it to fit operational needs, and loading it into a target database or data warehouse. Dataflow Gen2 refers to a modern, scalable ETL tool that supports low-code data integration. The total hours for daily ETL operations represent the elapsed time during which all ETL jobs are executed, regardless of the number of jobs.

Estimation Approach:
- Identify the start and end times for all ETL jobs.
- Calculate the total elapsed time considering overlapping windows.

| **Example** | **Jobs** | **Total Elapsed Time** |
|-------------|---------------|------------------------|
| **1**       | - Data Extraction: 7:00 AM - 8:00 AM (1 hour) <br/> - Data Transformation: 8:00 AM - 9:30 AM (1.5 hours) <br/> - Data Loading: 10:00 AM - 12:00 PM (2 hours) | **7:00 AM - 12:00 PM: 5 hours** (considering overlaps) |
| **2**       | - Data Validation: 6:00 AM - 7:00 AM (1 hour) <br/> - Data Cleansing: 7:00 AM - 9:00 AM (2 hours) <br/> - Data Aggregation: 9:30 AM - 11:30 AM (2 hours) | **6:00 AM - 11:30 AM: 5.5 hours** (considering overlaps) |
| **3**       | - Report Generation: 5:00 AM - 6:00 AM (1 hour) <br/> - Data Integration: 6:00 AM - 8:00 AM (2 hours) <br/> - Data Analysis: 8:30 AM - 11:30 AM (3 hours) | **5:00 AM - 11:30 AM: 6.5 hours** (considering overlaps) |
| **4**       | - Data Backup: 4:00 AM - 5:00 AM (1 hour) <br/> - Data Archiving: 5:00 AM - 7:30 AM (2.5 hours) <br/> - Data Restoration: 8:00 AM - 12:00 PM (4 hours) | **4:00 AM - 12:00 PM: 8 hours** (considering overlaps) |

## Number of SQL Analytics Users

> SQL Analytics users are individuals who perform ad-hoc SQL queries and require access to SQL endpoints.
> These users can include data analysts, reporting analysts, and database administrators (DBAs). SQL Analytics allows
> users to interact with databases to retrieve, manipulate, and analyze data. The number of daily SQL user
> sessions represents the total number of SQL queries initiated by these users each day.

$$
\text{Total Daily Sessions} = \text{Number of Users} \times \text{Average Sessions per User}
$$

| **Example** | **Number of Users** | **Average Sessions per User** | **Total Daily Sessions** |
|--------------|---------------------|------------------------------|--------------------------|
| **1**        | 50                  | 2.5                          | $$50 \times 2.5 = 125$$  |
| **2**        | 30                  | 3                            | $$30 \times 3 = 90$$     |
| **3**        | 75                  | 1.5                          | $$75 \times 1.5 = 112.5$$|
| **4**        | 100                 | 4                            | $$100 \times 4 = 400$$   |




<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-9-limegreen" alt="Total views">
  <p>Refresh Date: 2025-07-17</p>
</div>
<!-- END BADGE -->
