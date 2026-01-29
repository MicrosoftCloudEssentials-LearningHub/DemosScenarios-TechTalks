# Move files from a SharePoint site to Azure File Storage

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com)
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2026-01-29

----------

There might be few ways to do it:

- Using Az Copy
- Using Data Factory
- Using Logic App

## Wiki 

- [Tutorial: Migrate on-premises data to cloud storage with AzCopy](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-migrate-on-premises-data?tabs=windows)
- [Move files from a SharePoint site to Azure File Storage](https://learn.microsoft.com/en-us/answers/questions/1382373/move-files-from-a-sharepoint-site-to-azure-file-st)
- [Copy data from SharePoint Online List by using Azure Data Factory or Azure Synapse Analytics](https://learn.microsoft.com/en-us/azure/data-factory/connector-sharepoint-online-list?tabs=data-factory)
  
## Using AzCopy

1. **Set Up Azure Storage**:
   - Create a storage account in Azure if you don't have one.
   - Create a container within the storage account to store your files.
2. **Authenticate with Microsoft Entra ID**:
   - Download and install AzCopy, a command-line tool for copying data to Azure Storage.
   - Authenticate using Microsoft Entra ID with the command:

     ```bash
     azcopy login --tenant-id <your-tenant-id>
     ```

3. **Move Files from SharePoint to Azure Storage**:
   - Sync the SharePoint files to your local PC.
   - Use AzCopy to copy the files from your local PC to the Azure Storage container:

     ```bash
     azcopy copy "C:\path\to\your\folder" "https://<your-account>.blob.core.windows.net/<your-container>" --recursive
     ```

4. **Automation**: You can create scripts or use tools like Power Automate to automate the file copying process.

## Using Data Factory

Initial Setup:

1. **Register an Application in Azure AD**:
   - Go to the Azure portal and navigate to `Azure Active Directory`.
   - Register a new application and note down the `Application ID` and `Client Secret`.
2. **Configure Permissions in SharePoint**: Grant the registered application permissions to access SharePoint files.

Create a Pipeline in Azure Data Factory: 

1. **Create a Linked Service for SharePoint**:
   - In Azure Data Factory, go to the `Manage` section and select `Linked Services`.
   - Create a new Linked Service for SharePoint Online List and configure the connection details using the Application ID and Client Secret.
2. **Create a Linked Service for Azure Blob Storage**: Create another Linked Service for your Azure Blob Storage account.
3. **Configure the Pipeline**:
   - Create a new pipeline and add a `Web Activity` to get an access token from SharePoint.
   - Add another `Web Activity` to get the metadata of the SharePoint folder.
   - Use a `ForEach Activity` to iterate over the files obtained.
   - Inside the ForEach, add a `Copy Data Activity` to copy the files from SharePoint to Azure Blob Storage.

Configuration Details

- **Web Activity to Get the Token**:

  ```json
  {
    "url": "https://accounts.accesscontrol.windows.net/<tenant-id>/tokens/OAuth/2",
    "method": "POST",
    "headers": {
      "Content-Type": "application/x-www-form-urlencoded"
    },
    "body": "grant_type=client_credentials&client_id=<client-id>&client_secret=<client-secret>&resource=https://<sharepoint-site>"
  }
  ```

- **Web Activity to Get Metadata**:

  ```json
  {
    "url": "https://<sharepoint-site>/_api/web/GetFolderByServerRelativeUrl('<folder-path>')/Files",
    "method": "GET",
    "headers": {
      "Authorization": "Bearer <access-token>"
    }
  }
  ```

- **Copy Data Activity**:
  - Configure the source as SharePoint and the destination as Azure Blob Storage.
  - Map the necessary fields to copy the files.

Testing and Automation:
- **Test the Pipeline**: Run the pipeline to ensure the files are copied correctly.
- **Automate**: Schedule the pipeline to run at regular intervals or in response to specific events.




## Using Azure Logic Apps

1. **Create a Logic App**:
   - In the Azure portal, create a new Logic App.
   - Choose a blank template to start from scratch.
2. **Configure the Trigger**:
   - Add a SharePoint trigger, such as `When a file is created in a folder`.
   - Connect to your SharePoint site and select the folder you want to monitor.
3. **Add an Action to Copy Files**:
   - Add an Azure Blob Storage action, such as `Create blob`.
   - Connect to your Azure Storage account and select the destination container.
4. **Map the Data**: Map the file data from SharePoint to the corresponding fields in Azure Blob Storage.
5. **Save and Test**: Save the Logic App and test it by creating a file in the SharePoint folder to ensure it gets copied to Azure Storage.

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1535-limegreen" alt="Total views">
  <p>Refresh Date: 2026-01-29</p>
</div>
<!-- END BADGE -->
