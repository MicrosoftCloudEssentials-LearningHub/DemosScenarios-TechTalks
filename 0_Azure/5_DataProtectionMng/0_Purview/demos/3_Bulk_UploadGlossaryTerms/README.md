# Purview: Bulk Upload of Glossary Terms into new Unified Catalog

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com) 
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2026-01-29

----------

> Bulk upload glossary terms from the classic Purview to the new Unified Catalog


<details>
<summary><b>Table of References </b> (Click to expand)</summary>

- [Learn about the new Microsoft Purview portal](https://learn.microsoft.com/en-us/purview/purview-portal)
- [Microsoft Purview setup guides](https://learn.microsoft.com/en-us/purview/purview-fast-track-setup-guides)
- [Microsoft Purview (formerly Azure Purview) deployment checklist](https://learn.microsoft.com/en-us/purview/legacy/tutorial-azure-purview-checklist)
- [Import and export glossary terms](https://learn.microsoft.com/en-us/purview/legacy/how-to-import-export-glossary)
- [Get ready for the next enhancement in Microsoft Purview governance](https://learn.microsoft.com/en-us/purview/new-governance-experience)
- If you're a `new Microsoft Purview customer`, [read about the new governance experience here](https://learn.microsoft.com/en-us/purview/purview-portal#new-experience-for-new-customers).
- If you're an `existing Microsoft Purview customer`, [read about the new governance experience here](https://learn.microsoft.com/en-us/purview/purview-portal#new-experience-for-existing-data-governance-customers).
- [Purview Roadmap](https://learn.microsoft.com/en-us/purview/whats-new)
  
</details>


<details>
<summary><b>Table of Content </b> (Click to expand)</summary>

- [Prerequisites](#prerequisites)
- [Create a Microsoft Purview Account](#create-a-microsoft-purview-account)
- [Uploading Glossary Terms - Classic Purview](#uploading-glossary-terms---classic-purview)
- [Downloading Glossary Terms - Classic Purview](#downloading-glossary-terms---classic-purview)
- [How to transition data to - new Microsoft Purview portal](#how-to-transition-data-to---new-microsoft-purview-portal)

</details>

## Prerequisites
1. **Microsoft Entra Tenant**:
   - Ensure you have a Microsoft Entra tenant associated with your subscription.
   - Required roles: Information Protection Administrator, Power BI Administrator (if scanning Power BI tenants).
2. **Azure Subscription**: You need an active Azure subscription. If you don't have one, create a free subscription.
3. **Resource Providers**: Register the following resource providers in your Azure subscription:
     - `Microsoft.Storage`
     - `Microsoft.EventHub` (optional)
     - `Microsoft.Purview`

        <img width="550" alt="image" src="https://github.com/user-attachments/assets/89697e6d-464b-4ec9-be5e-7539807cc26b" />

        <img width="550" alt="image" src="https://github.com/user-attachments/assets/7603bd96-6b6a-40b2-9d4f-4fdffba15681" />

## Create a Microsoft Purview Account
1. **Navigate to Azure Portal**: Go to the Azure portal and search for `Microsoft Purview`.

     <img width="550" alt="image" src="https://github.com/user-attachments/assets/9ebaf4cb-38cb-4285-8786-f286107a983b" />

2. **Create Purview Account**: Click on "Create" and fill in the required details.
    - Subscription
    - Resource Group
    - Purview Account Name
    - Region
    
        <img width="550" alt="image" src="https://github.com/user-attachments/assets/0ab094df-3040-493e-9912-affb635371fe" />

3. **Configure Event Hub (Optional)**: If you plan to use an existing Event Hubs namespace, configure it during account creation.

## Uploading Glossary Terms - (Classic Purview)

1. **Open Microsoft Purview Data Catalog**: If you're using the `classic Microsoft Purview` portal, select `Glossary`.

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/354d43ab-16be-4a02-a230-4a4efccc0dfa" />

2. **Select/Create the Glossary** where you want to import terms.

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/0b013cd2-7785-497a-9f49-20977bcf1a63">

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/cdbd1296-2ab4-4bac-a1f3-029b1080ac56" />

3. Select `Import terms`, and upload your filled CSV file. 

    <img width="550" alt="image" src="https://github.com/user-attachments/assets/df5dbe5b-b3f1-46e4-ac91-381fa39e242f" />

    - You can use `System Default Template` or `Create New Template`:

       | **Feature**                  | **System Default Template**                                      | **Create New Template**                                      |
       |------------------------------|------------------------------------------------------------------|--------------------------------------------------------------|
       | **Customization**            | Limited to predefined fields (e.g., Term, Definition)            | Highly customizable; add fields like Synonyms, Categories, etc. |
       | **Ease of Use**              | Simple and quick to use with basic fields                        | Requires initial setup to define custom fields               |
       | **Consistency**              | Standardized format with basic fields                           | Ensures consistency with custom fields tailored to your needs |
       | **Flexibility**              | Less flexible; limited to default fields                        | Highly flexible; adapt to changing requirements              |
       | **Metadata Inclusion**       | Basic metadata (Term, Definition)                               | Include additional metadata (e.g., Synonyms, Related Terms)  |
       | **Setup Time**               | Minimal setup time                                              | Requires more time to create and define custom fields        |
       | **Use Case**                 | Suitable for simple glossaries with basic terms and definitions | Ideal for complex glossaries with detailed information       |

       <img width="550" alt="image" src="https://github.com/user-attachments/assets/79ee1f04-5bff-4680-9b44-0c6c76457cf8">

       <img width="550" alt="image" src="https://github.com/user-attachments/assets/886fec2b-918b-4d52-bfa3-dca5d2442895" />

       <img width="550" alt="image" src="https://github.com/user-attachments/assets/0258f41f-52fc-494b-bd0c-87239a5c41b8" />

## Downloading Glossary Terms - (Classic Purview)

1. **Open Microsoft Purview Data Catalog**: Navigate to the glossary where your terms are stored.
2. **Select the Terms** you want to export.

      <img width="550" alt="image" src="https://github.com/user-attachments/assets/fd15d234-bb0c-498f-981b-318af80f947b" />

3. **Export Terms**:
   - Once you've selected the terms, the `Export terms` button will be enabled.
     
        <img width="550" alt="image" src="https://github.com/user-attachments/assets/01757369-d79c-4a3d-954d-6eebc91f45b6" />

   - Click on it to download the terms in a CSV file.

      <img width="550" alt="image" src="https://github.com/user-attachments/assets/8d184813-ae63-4ba1-a42e-aa496d6c7f38" />

## How to transition data to - (new Microsoft Purview portal)

> [!IMPORTANT]
> The `data appears to have migrated seamlessly`. Please follow the steps below to `locate the glossary terms you created in the classic Purview portal within this new portal`. 

1. Switch to new portal:

      <img width="550" alt="image" src="https://github.com/user-attachments/assets/4aed6fb8-8db9-45c5-874a-aaf62db5103d" />

2. Go to `Unified Catalog`:

      <img width="550" alt="image" src="https://github.com/user-attachments/assets/a3b8c440-56d8-4369-bddf-817d6b8575ea" />

3. Under `Discovery`, go to `Data assets`. There, you will find your glossary terms.

      <img width="550" alt="image" src="https://github.com/user-attachments/assets/ce5a2a73-1e8f-4ffb-9936-94d41cf4638d" />

4. Search for `glossary`:

      <img width="550" alt="image" src="https://github.com/user-attachments/assets/9f9fc5b2-13af-4531-a421-5f0ae5d16c1d" />
      
5. You can click on the terms and perform all related actions with these glossary terms. Therefore, there is no need to migrate them as they are already reflected.

      <img width="550" alt="image" src="https://github.com/user-attachments/assets/1a037ed1-e10a-4f78-97c4-0d55836f1b3e" />

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1535-limegreen" alt="Total views">
  <p>Refresh Date: 2026-01-29</p>
</div>
<!-- END BADGE -->
