# Connecting Microsoft Fabric to Oracle HDI 

Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2026-01-29

----------

> Oracle Health Data Intelligence (HDI), formerly known as HealtheIntent, is a modular suite of cloud applications, services, and analytics. It enables healthcare and government stakeholders to use data from across the healthcare ecosystem to advance patient health, improve care delivery, and drive operational efficiency.

## Wiki
- [API Access and Fees and Registering an App](https://www.oracle.com/health/developer/api/)
- [Healthcare Analytics Data Integration Documentation](https://docs.oracle.com/en/industries/health-sciences/analytics-data-integration/index.html)
- [Hospital Use of APIs to Enable Data Sharing Between EHRs and Apps](https://www.healthit.gov/data/data-briefs/hospital-use-apis-enable-data-sharing-between-ehrs-and-apps)
- [Set up your Oracle database connection - Microsoft Fabric](https://learn.microsoft.com/en-us/fabric/data-factory/connector-oracle-database)
- [Oracle database connector overview - Microsoft Fabric](https://learn.microsoft.com/en-us/fabric/data-factory/connector-oracle-database-overview)
- [Step-by-Step Guide: Interconnecting Oracle Cloud](https://blogs.oracle.com/cloudmarketplace/post/step-by-step-guide-interconnecting-oracle-cloud-infrastructure-and-microsoft-azure)
- [Connecting Oracle to Microsoft fabrics - Microsoft Fabric Community](https://community.fabric.microsoft.com/t5/General-Discussion/Connecting-Oracle-to-Microsoft-fabrics/m-p/3260454)

> Prerequisites:
>  1. **Register and Set Up API Access**
>     - **Register Your Application**: Go to the Oracle Health Developer Program console and register your application. Review and accept the API Access Terms and Conditions.
>     - **Review API Documentation**: Familiarize yourself with the Oracle Health API documentation, including available FHIR API resources.
>  2. **Install Necessary Tools**
>     - **Oracle Client**: Ensure the Oracle Client is installed on the machine running the on-premises data gateway.
>     - **Microsoft Fabric**: Set up Microsoft Fabric and ensure you have the necessary permissions to create and manage data pipelines.

## How to 

> **Set Up Data Gateway**: If your Oracle database is on-premises, configure the on-premises data gateway to facilitate the connection.

1. **Setup the Data Pipeline in Microsoft Fabric**
    - **Open Data Factory**: Navigate to Microsoft Fabric's Data Factory.

      <img width="219" alt="image" src="https://github.com/user-attachments/assets/be07d64c-5adc-4a60-970b-76dee9020ddf">
      
   - **Create a Pipeline**: In Data Factory, create a new pipeline to manage the data flow from Oracle HDI to your desired destination.

       <img width="550" alt="image" src="https://github.com/user-attachments/assets/ac73aab8-dd74-45d3-b33b-a337e6321a30">

   - **Add Copy Activity**: Add a copy activity to the pipeline. 
       - In the **Source** tab of the Copy Data activity, select the Oracle linked service you created.
       - Specify the table or query to extract data from Oracle HDI.

       <img width="550" alt="image" src="https://github.com/user-attachments/assets/9e9607ba-c4a0-4c23-a91e-cc5d4d690b87">

       <img width="550" alt="image" src="https://github.com/user-attachments/assets/b055d13a-535c-42b1-9f35-474c0e5c825a">
        
       <img width="550" alt="image" src="https://github.com/user-attachments/assets/5a2365f1-88d4-4a9b-9564-043dd1f1db5d">

      - **Configure Connection**:
         - **Server Name**: Enter the Oracle server name.
         - **Database Name**: Enter the name of your Oracle HDI database.
         - **Authentication**: Choose the appropriate authentication method (e.g., Basic).
         - **Username and Password**: Enter your Oracle database credentials.
         - **Test Connection**: Click on **Test Connection** to ensure the details are correct.
           
 2. **Configure Data Compression**
     - In the **Destination** tab, choose the destination data store (e.g., Azure Blob Storage, SQL Database).
     - **Select Compression Type**: In the copy activity settings, choose the desired compression type (LZ4 or GZIP) for the data transfer.
     - **Destination Configuration**: Configure the destination settings to store the compressed data in your preferred format. Specify the file format and path where the compressed data will be stored.
  
      <img width="550" alt="image" src="https://github.com/user-attachments/assets/9fc9137a-4d7d-47ad-9a89-a1a16123c8b8">
      
      <img width="550" alt="image" src="https://github.com/user-attachments/assets/5d415334-03d2-410b-9bf6-a48c6421faba">
      
     - Ensure the destination supports the chosen compression format.

## Possible Issues and Solutions

 1. **Connection Issues**
     - **Issue**: Unable to connect to the Oracle database.
     - **Solution**: Verify the connection details, ensure the Oracle Client is correctly installed, and check network connectivity. Ensure the on-premises data gateway is properly configured and running.
 2. **Authentication Problems**
     - **Issue**: Authentication failures when connecting to the Oracle API.
     - **Solution**: Double-check the credentials and authentication method used. Ensure that the API key or token is valid and has the necessary permissions.
 3. **Data Transfer Errors**
     - **Issue**: Errors during data transfer.
     - **Solution**: Check the data pipeline logs for specific error messages. Ensure that the data format and schema are compatible between the source and destination. Adjust the query or data mapping as needed.
 4. **Compression Issues**
     - **Issue**: Data not being compressed as expected.
     - **Solution**: Verify the compression settings in the copy activity. Ensure that the destination supports the specified compression format (LZ4 or GZIP).
       
<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1535-limegreen" alt="Total views">
  <p>Refresh Date: 2026-01-29</p>
</div>
<!-- END BADGE -->