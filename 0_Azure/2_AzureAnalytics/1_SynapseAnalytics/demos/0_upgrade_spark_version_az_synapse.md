# Azure Synapse: Upgrading Apache Spark Pool Version - Overview

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com) 
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-01-13

----------

<details>
<summary><b>List of References </b> (Click to expand)</summary>

- [Azure Synapse runtimes](https://learn.microsoft.com/en-us/azure/synapse-analytics/spark/apache-spark-version-support)
- [How to upgrade Spark version in Synaspe?](https://learn.microsoft.com/en-us/answers/questions/1165315/how-to-upgrade-spark-version-in-synaspe)
- [Manage libraries for Apache Spark pools in Azure Synapse Analytics](https://learn.microsoft.com/en-us/azure/synapse-analytics/spark/apache-spark-manage-pool-packages)
- [Update-AzSynapseSparkPool](https://learn.microsoft.com/en-us/powershell/module/az.synapse/update-azsynapsesparkpool?view=azps-13.0.0&viewFallbackFrom=azps-10.2.0)
- [The Azure Synapse resource provider (Microsoft.Synapse) needs to be registered with the selected subscription](https://learn.microsoft.com/en-us/answers/questions/1621445/the-azure-synapse-resource-provider-%28microsoft-syn)

</details>

<details>
<summary><b>Table of Content </b> (Click to expand)</summary>

- [Overview](#overview)
- [How to create Apache Spark Pool in Azure Synapse](#how-to-create-apache-spark-pool-in-azure-synapse)
    - [Registering the Microsoft Azure Synapse Provider](#registering-the-microsoft-azure-synapse-provider)
    - [Create an Azure Synapse Workspace](#create-an-azure-synapse-workspace)
    - [Create an Apache Spark Pool](#create-an-apache-spark-pool)
- [Upgrade - Azure PowerShell](#upgrade---azure-powershell)
- [Upgrade - Azure CLI](#upgrade---azure-cli)

</details>

## Overview 

> `What is a Spark Pool?`: A Spark Pool in Azure Synapse is a collection of resources that allows you to run Apache Spark jobs. Apache Spark is an open-source, distributed computing system used for big data processing and analytics. <br/>
> `Why Upgrade?`:  Upgrading the Spark version in your Spark Pool ensures you benefit from the latest features, performance improvements, and security patches. It helps maintain compatibility with new libraries and tools, and can improve the efficiency and reliability of your data processing tasks. <br/> <br/>
> Benefits of Upgrading: <br/>
> - **Performance Improvements**: Newer versions of Spark often include optimizations that can speed up your data processing tasks. <br/>
> - **New Features**: Access to the latest features and functionalities introduced in newer Spark versions. <br/>
> - **Security Patches**: Ensures your Spark environment is protected with the latest security updates. <br/>
> - **Compatibility**: Maintains compatibility with new libraries, tools, and other components in the Azure ecosystem.

> [!IMPORTANT]
> - Testing: Before upgrading, it's advisable to test the new Spark version in a separate environment to ensure compatibility with your existing workloads. <br/>
> - Backup: Ensure you have backups of your data and configurations in case you need to roll back the upgrade. <br/>
> - Monitoring: After upgrading, monitor the performance and stability of your Spark Pool to ensure everything is functioning as expected.

| Key Points          | Details                                                                                                                                                                                                                                                                                                                                                     |
|---------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Supported Versions** | - Azure Synapse supports multiple versions of Apache Spark. <br> - It's recommended to upgrade to the latest General Availability (GA) version for optimal performance and support. <br> - You can find the list of supported versions in the [official documentation](https://learn.microsoft.com/en-us/azure/synapse-analytics/spark/apache-spark-version-support#supported-azure-synapse-runtime-releases). |
| **Upgrade Process** | - The upgrade process involves updating the Spark version used by your Spark Pool. <br> - This can be done using Azure PowerShell or Azure CLI, the `Update-AzSynapseSparkPool cmdlet` is commonly used for this purpose in PowerShell, while the `az synapse spark pool update` command is used in Azure CLI. <br> - The process typically includes connecting to your Azure account, setting the subscription context, and running the appropriate command to update the Spark version. |
| **Library Management** | - When upgrading, you might also need to update or manage the libraries associated with your Spark Pool. <br> - This ensures compatibility with the new Spark version and takes advantage of new features and improvements. <br> - Detailed instructions for managing libraries can be found in the [library management documentation](https://learn.microsoft.com/en-us/azure/synapse-analytics/spark/apache-spark-version-support). |

## How to create Apache Spark Pool in Azure Synapse

> [!IMPORTANT]
> Before setting up an Azure Synapse workspace and Apache Spark pool, please ensure that the `Microsoft Synapse resource provider` is registered in your subscription. This solve the error when attempting to create the Synapse workspace:

<img width="550" alt="image" src="https://github.com/user-attachments/assets/5a05bd12-55a0-4fc5-ade9-f66c709a6ca7">

### Registering the Microsoft Azure Synapse Provider

1. **Go to the Azure Portal**: Navigate to the Azure portal.
2. **Select Your Subscription**: In the left-hand menu, select `Subscriptions` and choose the subscription you want to use.
3. **Register the Resource Provider**:
   - In the subscription blade, select `Resource providers`.
   - In the search bar, type `Synapse` and select the `Microsoft.Synapse` resource provider.
   - Click on the `Register` button to register the resource provider with your subscription.
  
       | Before Register | After Register |
       | --- | --- | 
       | <img width="550" alt="image" src="https://github.com/user-attachments/assets/558e1828-e940-4c39-912a-d554fa4e574f"> | <img width="550" alt="image" src="https://github.com/user-attachments/assets/6a61ffb0-097b-4806-9129-a19ace1297e4"> | 

### Create an Azure Synapse Workspace

1. **Navigate to Azure Synapse Analytics**:
   - In the Azure portal, search for `Azure Synapse Analytics` and select it.
   - Click on `Add` to create a new workspace.

       <img width="550" alt="image" src="https://github.com/user-attachments/assets/814aaf53-2e37-4fca-90c9-1fe219cccf7a" />

2. **Configure the Workspace**:
   - **Basics**: Provide the necessary details such as subscription, resource group, workspace name, region, and storage account.
   - **Security**: Configure security settings, including managed virtual network and data encryption.
   - **Networking**: Configure networking settings, such as public or private endpoint.
   - **Tags**: Optionally, add tags to organize your resources.
   - **Review + Create**: Review your settings and click `Create` to deploy the workspace.

       <img width="550" alt="image" src="https://github.com/user-attachments/assets/39827191-8d0d-4439-a0c5-d84b6d280574" />

### Create an Apache Spark Pool

1. **Navigate to the Synapse Workspace**:
   - Once the workspace is created, navigate to it in the Azure portal.
   - Click on `New Apache Spark pool` under the `Apache Spark pools` section.

       <img width="550" alt="image" src="https://github.com/user-attachments/assets/7f53e836-6361-4106-bf56-0144ef3dc44d" />

2. **Configure the Spark Pool**:
   - **Basics**: Provide the pool name, node size, and number of nodes.
   - **Additional Settings**: Configure additional settings such as auto-scaling and auto-pausing.
   - **Tags**: Optionally, add tags to organize your resources.
   - **Review + Create**: Review your settings and click `Create` to deploy the Spark pool.

        <img width="550" alt="image" src="https://github.com/user-attachments/assets/be965887-04a0-4ce1-87ac-320ebdf21e1f" />

        <img width="550" alt="image" src="https://github.com/user-attachments/assets/3cb3e56a-2341-47d3-abf8-f25778c223b4" />

## Upgrade - Azure PowerShell

1. Connect to your Azure account with device authentication

      ```
      Connect-AzAccount -UseDeviceAuthentication
      ```

     <img width="550" alt="image" src="https://github.com/user-attachments/assets/0170f701-7dff-46bb-aa00-5eab38f00ce9" />

2. Set the subscription context (If it hasn't prompted you to select your subscription, please proceed to run it)

      ```
      Set-AzContext -SubscriptionId <YourSubscriptionId>
      ```

3. Upgrade the Spark Pool

      ```
      Update-AzSynapseSparkPool -ResourceGroupName <ResourceGroupName> -WorkspaceName <WorkspaceName> -Name <SparkPoolName> -SparkVersion <version_number>
      ```

      For example: 
      
      > Update-AzSynapseSparkPool -ResourceGroupName RGAzureSynapseApacheSparkPool -WorkspaceName brownsynapsetestsparkpool -Name MySparkPool -SparkVersion 3.4

     | Before the upgrade | After the upgrade |
     | --- | --- | 
     | <img width="550" alt="image" src="https://github.com/user-attachments/assets/557f224e-89c4-4c69-8599-965b86062aeb"> | <img width="550" alt="image" src="https://github.com/user-attachments/assets/3bd9d942-a289-46d7-b1d4-6b81da906d61"> | 

## Upgrade - Azure CLI

1. Log in to your Azure account

      ```
      az login
      ```

     <img width="550" alt="image" src="https://github.com/user-attachments/assets/f835a2be-af73-42ea-8870-b39ced91e34b" />

2. Set the subscription context (If it hasn't prompted you to select your subscription, please proceed to run it)

      ```
      az account set --subscription <YourSubscriptionId>
      ```

3. Upgrade the Spark Pool

      ```
      az synapse spark pool update --resource-group <ResourceGroupName> --workspace-name <WorkspaceName> --name <SparkPoolName> --spark-version <version_number>
      ```

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-354-limegreen" alt="Total views">
  <p>Refresh Date: 2025-07-17</p>
</div>
<!-- END BADGE -->
