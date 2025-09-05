# Connecting Microsoft Fabric to Azure HDI Platform

Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

----------

## Wiki 

- [Transform data by running an Azure HDInsight activity](https://learn.microsoft.com/en-us/fabric/data-factory/azure-hdinsight-activity)

> Prerequisites: 
>  1. **Install On-Premises Data Gateway**: Ensure you have an on-premises data gateway installed and configured. <br/>
>  2. **Install HDI Client**: Ensure the HDI client is installed on the machine running the on-premises data gateway. 

## How to

```mermaid
graph LR
    A[Install On-Premises Data Gateway] --> B[Install HDI Client]
    B --> C[Configure HDI Client]
    C --> D[Open Data Factory in Microsoft Fabric]
    D --> E[Connect Data Source]
    E --> F[Specify Connection Details]
    F --> G[Set Authentication]
    F --> H[Select Data Gateway]
```

### Set Up HDI Connection
1. **Install HDI Client**: Ensure the HDI client is installed on the machine running the on-premises data gateway.
2. **Configure HDI Client**: Follow the HDI platform's documentation to configure the client.

### Configure Connection in Data Pipeline
1. **Open Data Factory**: Go to the Data Factory pipeline in Microsoft Fabric.

   <img width="200" alt="image" src="https://github.com/user-attachments/assets/c722730e-b104-4577-ad44-d6e595026e0b">

2. **Create a New Data Pipeline**:
    - Click on the “Create pipeline” button.
      
      <img width="400" alt="image" src="https://github.com/user-attachments/assets/8f5048f1-4ffc-43af-8150-caa768afd620"> <br/>

      <img width="400" alt="image" src="https://github.com/user-attachments/assets/69d3c597-77f3-461b-97e6-7a4078fb4642">

    - Add activities to your pipeline, such as **Pipeline activity**, to define the data transformation and movement.
      
      <img width="400" alt="image" src="https://github.com/user-attachments/assets/5b24ad77-2a8e-4aa7-a783-d42f3957da6f">

3. Select the `HDInsight` connector:

    <img width="400" alt="image" src="https://github.com/user-attachments/assets/23006761-4968-473a-9c23-5351024d3f1f">

4. Select the `HDI Cluster` tab to create or select an existing connection

   <img width="461" alt="image" src="https://github.com/user-attachments/assets/d82138d4-e953-42bd-b56c-33909eb57185">

5. **Specify Connection Details**:
    - Create new connection or select the existing one:
      
        <img width="461" alt="image" src="https://github.com/user-attachments/assets/2c4963bd-e974-4d7b-a3ae-935af8c23c50"> <br/>

        <img width="461" alt="image" src="https://github.com/user-attachments/assets/c19998e9-087c-45bf-aba9-5c12f54d5372">

   - **Server**: Enter the HDI platform server details.
   - **Connection Name**: Provide a name for your connection.
   - **Data Gateway**: Select your on-premises data gateway.

        <img width="461" alt="image" src="https://github.com/user-attachments/assets/1477d5be-1782-477c-89d5-06ecfc0723a2">

6. Make sure to fill out the `Settings` tab:

   <img width="461" alt="image" src="https://github.com/user-attachments/assets/6fc14f0b-3031-488c-9217-8ebee7184f55">

7. Set Authentication
    - **Authentication Kind**: Choose the appropriate authentication type.
    - **Credentials**: Enter your HDI platform credentials.

## Possible Connection Issues and Solutions

```mermaid
graph TD
    A[Client Configuration Issues]
    A1[Check HDI client setup]
    A --> A1

    B[Authentication Errors]
    B1[Verify credentials]
    B --> B1

    C[Data Gateway Issues]
    C1[Ensure data gateway is running]
    C --> C1
```


1. Client Configuration Issues
    - **Issue**: HDI client is not properly configured.
    - **Solution**: Follow the HDI platform's documentation to ensure correct configuration.
2. Authentication Errors
    - **Issue**: Incorrect authentication type or credentials.
    - **Solution**: Verify the authentication type and credentials.
3. Data Gateway Issues
    - **Issue**: On-premises data gateway is not running or not configured correctly.
    - **Solution**: Ensure the data gateway is installed, running, and properly configured.

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1443-limegreen" alt="Total views">
  <p>Refresh Date: 2025-09-05</p>
</div>
<!-- END BADGE -->