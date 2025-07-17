# Parsing XML files in Power Query - Overview 

Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

----------

> Parsing an XML file and converting it into columns and rows using Microsoft Fabric's Data Factory

## Wiki 

<details>
<summary><b>List of References </b> (Click to expand)</summary>

- [XML format in Data Factory in Microsoft Fabric](https://learn.microsoft.com/en-us/fabric/data-factory/format-xml)
- [Best practices when working with Power Query](https://github.com/MicrosoftDocs/powerquery-docs/blob/main/powerquery-docs/best-practices.md#best-practices-when-working-with-power-query)

</details>


## Content 

<details>
<summary><b>Table of Contents</b> (Click to expand)</summary>

- [Wiki](#wiki)
- [Content](#content)
- [Overview](#overview)
- [Demo](#demo)
  - [Step 1: Set Up Your Data Pipeline](#step-1-set-up-your-data-pipeline)
  - [Step 2: Configure the Source Dataset Copy Data Activity](#step-2-configure-the-source-dataset-copy-data-activity)
  - [Step 3: Configure the Destination sink Dataset Lakehouse](#step-3-configure-the-destination-sink-dataset-lakehouse)
  - [Step 4: Configure the Destination sink settings Copy Data Activity](#step-4-configure-the-destination-sink-settings-copy-data-activity)
  - [Step 5: Run the Pipeline](#step-5-run-the-pipeline)
  - [Example Configuration](#example-configuration)

</details>

## Overview 

| **Technical Overview**       | **Details**                                                                                                                                                       |
|------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Data Pipeline Setup**   | - **Data Pipeline**: A data pipeline in Microsoft Fabric's Data Factory orchestrates the data flow from the source (XML file) to the destination (e.g., SQL Database, Data Lake). This involves defining the source, transformations, and destination.<br/>- **Copy Activity**: The core activity used to copy data from the XML source to the destination. It supports various transformations and data mappings, ensuring data integrity and consistency during the transfer. |
| **Source Dataset Configuration** | - **Dataset Type**: The source dataset type must be set to Xml to correctly interpret the structure and content of the XML file.<br/>- **Location**: Specifies the location of the XML file. This can be in Azure Blob Storage, Amazon S3, Azure Data Lake, etc., allowing flexibility in data storage options.<br/>- **Encoding**: Defines the encoding type used to read the XML file (e.g., UTF-8, UTF-16), ensuring the correct interpretation of character sets.<br/>- **Compression**: If the XML file is compressed, specify the compression type (e.g., gzip, bzip2) to enable proper decompression during data extraction. |
| **Destination (sink) Dataset Configuration** | - **Dataset Type**: The Destination (sink) dataset type depends on the destination (e.g., SQL Database, Data Lake), which determines how the data will be stored and accessed.<br/>- **Connection**: Configure the connection settings to the destination, including authentication and network settings to ensure secure and reliable data transfer.<br/>- **Schema Mapping**: Map the XML elements to the corresponding columns in the destination, ensuring that the data structure is preserved and correctly interpreted in the target system. |
| **Copy Activity Configuration** | `Source Settings`:<br/>  - **XmlSource**: Specifies the XML source settings, including the root node path, which defines the starting point for data extraction.<br/>  - **Compression**: Configure compression settings if the XML file is compressed, ensuring that the data is properly decompressed before processing.<br/>`Destination (sink) Settings`:<br/>  - **SqlDestination (sink)**: Specifies the SQL Destination (sink) settings or other destination settings, including table names and data types.<br/>  - **Column Mapping**: Map the XML elements to the destination columns, ensuring that each piece of data is correctly placed in the target schema. |
| **Running the Pipeline**  | - **Validation**: Validate the pipeline to ensure there are no configuration errors, checking for issues such as missing fields or incorrect data types.<br/>- **Debugging**: Debug the pipeline to test the data flow and ensure it works as expected, identifying and resolving any issues that arise during the process.<br/>- **Execution**: Run the pipeline to parse the XML file and load the data into the destination, monitoring the process to ensure successful completion and data accuracy. |

## Demo 

> [!IMPORTANT]
> Tips
> 1. **Filter Early**: Apply filters as early as possible in your query to reduce the amount of data being processed. This can significantly speed up the parsing process. <br/>
> 2. **Use `Xml.Document` Instead of `Xml.Tables`**: When loading XML data, use `Xml.Document` to get a more flexible structure that you can manipulate more efficiently. This approach can help expose all data elements for easier access. <br/>
> 3. **Avoid Nested Expansions**: Minimize the number of nested table expansions. Each expansion can add significant overhead, so try to flatten the structure as much as possible. <br/>
> 4. **Work with a Subset of Data**: If the XML file is large, consider working with a smaller subset of the data during the development phase. This can make the process faster and easier to manage. <br/>
> 5. **Optimize Data Types**: Ensure that you are using the correct data types for your columns. Incorrect data types can slow down the processing. <br/>
> 6. **Modular Approach**: Break down your query into smaller, manageable steps. This modular approach can help isolate performance issues and make the query easier to debug.


### Step 1: Set Up Your Data Pipeline

1. **Create a Data Pipeline**:
   - Go to your [Microsoft Fabric workspace](https://app.fabric.microsoft.com/home).

       <img width="550" alt="image" src="https://github.com/user-attachments/assets/b16c5a86-630a-4e73-8ffc-4445bb863a4e" />

   - Navigate to Data Factory and create a new data pipeline in your existing workspace or create new.

       <img width="550" alt="image" src="https://github.com/user-attachments/assets/73632982-e4d5-4f76-8ce5-dbcca39c268c" />

       <img width="550" alt="image" src="https://github.com/user-attachments/assets/266a7820-bc81-4048-b532-3efc1ac5b519" />

       <img width="550" alt="image" src="https://github.com/user-attachments/assets/86d7caed-893e-428e-abb4-9939d9c07a8f" />

2. **Add a Copy Activity**:
   - In the pipeline, add a Copy activity.

       <img width="550" alt="image" src="https://github.com/user-attachments/assets/cc116355-a4cc-4f4d-8ffd-1f60bda65ed7" />

### Step 2: Configure the Source Dataset (Copy Data Activity)

> [!NOTE]
> For this purpose, I already have a lakehouse with some XML files in place. Here is the input source used, few examples of [XML File: Employee Records](https://github.com/MicrosoftCloudEssentials-LearningHub/Demos-ScenariosHub/tree/main/0_Azure/2_AzureAnalytics/0_Fabric/demos/26_ParsingXMLfilesPQuery/samples) used.

<img width="550" alt="image" src="https://github.com/user-attachments/assets/e5d6b1b4-8330-47a7-8ffb-fe990d83b12b" />

1. `Connection`:
   - In the `Source` tab, select the appropriate connection from the dropdown menu (e.g., `lakehouse_data_schema`).
   - Use the `Refresh` button if needed to update the list of available connections.
   - Click `Open` to verify the connection details.
2, `Root Folder`: Choose between `Tables` and `Files`. Select `Files` if your XML files are stored in a file-based structure.
3. `File Path Type`:
   - Choose the type of file path you want to use:
      - `File path`: For a specific file.
      - `Wildcard file path`: For multiple files matching a pattern.
      - `List of files`: For a list of specific files.
   - Select `File path` for a single XML file.
4. `File Path`:
     - Enter the directory and file name of your XML file.
     - Use the `Browse` button to navigate and select the file if needed.
5. `Recursively`: Check this box if you want to include files in subdirectories.

     <img width="550" alt="image" src="https://github.com/user-attachments/assets/31f09166-7968-49ae-84f4-f11660ccfc39" />

6. `File Format`:
     - Select `XML` from the dropdown menu.
     - Click on `Settings` to configure any additional file format settings.

          <img width="550" alt="image" src="https://github.com/user-attachments/assets/2fca8a6a-a761-484d-8ffa-cbd99ab0a837" />

          <img width="550" alt="image" src="https://github.com/user-attachments/assets/fd1709de-4428-48eb-bf56-174a59839e7f" />

### Step 3: Configure the Destination (sink) Dataset (Lakehouse)

1. **Navigate to the Lakehouse**:
      - In your Microsoft Fabric workspace, go to the **Lakehouse** section.
      - Open the lakehouse where your XML files are stored.
2. **Create a New Folder for Output**: In the lakehouse, create a new folder for storing the output data. For example, create a folder named `outputXML`.

      <img width="550" alt="image" src="https://github.com/user-attachments/assets/7142268b-3495-4e79-8423-e7a4edd6d70a" />

      <img width="550" alt="image" src="https://github.com/user-attachments/assets/63d6e6db-38fb-4aeb-ad14-edf407e91f08" />

3. **Configure the Destination (sink) Path**: Note the path to the new folder. For example, `/outputXML/EmployeeRecords`.

      <img width="550" alt="image" src="https://github.com/user-attachments/assets/b4d80c29-c517-4736-844f-375b5ed5a08d" />

### Step 4: Configure the Destination (sink) settings (Copy Data Activity)

1. **Select Destination Path**:
   - In the **Destination (sink)** tab, configure the path to the output folder in your lakehouse.
   - Enter the path to the output folder, for example, `/outputXML/EmployeeRecords`.
2. **File Format**:
   - Select `DelimitedText` (CSV) from the dropdown menu.

        <img width="550" alt="image" src="https://github.com/user-attachments/assets/196bf0e6-e62d-4dee-b0dc-af4cf9d16e17" />

   - Click on **Settings** to configure any additional file format settings.
      - **Delimiter**: Specify the delimiter (e.g., comma `,`).
      - **Header**: Choose whether to include headers in the output file.
      - **Compression**: If needed, specify the compression type (e.g., gzip).
   
           <img width="550" alt="image" src="https://github.com/user-attachments/assets/ef38a2ec-19bb-4056-8dfd-4c172b92b9fd" />

3. **Copy Behavior**: Ensure that the copy behavior is set correctly to avoid the error. Since you are copying from a folder to a single file, you need to specify the correct behavior. In the Destination (sink) settings, `set the Copy behavior to PreserveHierarchy`.

      <img width="550" alt="image" src="https://github.com/user-attachments/assets/b0e12450-24dd-4c57-bf9d-49705af6ab53" />

### Step 5: Run the Pipeline

1. **Validate and Debug**:
   - Validate your pipeline to ensure there are no errors.
   - Debug the pipeline to test the data flow.

        <img width="550" alt="image" src="https://github.com/user-attachments/assets/4dbbe1e8-8736-46d6-8444-903f6bffaa0f" />

2. **Run the Pipeline**: Once validated, run the pipeline to parse the XML file and load the data into the destination.

      <img width="550" alt="image" src="https://github.com/user-attachments/assets/5570bc3d-fab7-4e92-ac92-9d10d9bb3342" />

      <img width="550" alt="image" src="https://github.com/user-attachments/assets/3377ae71-b765-4763-af6d-f4e99e01186a" />

      <img width="550" alt="image" src="https://github.com/user-attachments/assets/eb3bbefc-768b-40ae-ba3d-ef5b430d169f" />

      <img width="550" alt="image" src="https://github.com/user-attachments/assets/851dbc1a-d831-4ffb-81ae-5157ba3d0803" />

### Example Configuration

Click here to go to source of the [example of how you might configure the XML parsing in the pipeline](https://github.com/MicrosoftCloudEssentials-LearningHub/Demos-ScenariosHub/tree/main/0_Azure/2_AzureAnalytics/0_Fabric/demos/26_ParsingXMLfilesPQuery/source)

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-9-limegreen" alt="Total views">
  <p>Refresh Date: 2025-07-17</p>
</div>
<!-- END BADGE -->
