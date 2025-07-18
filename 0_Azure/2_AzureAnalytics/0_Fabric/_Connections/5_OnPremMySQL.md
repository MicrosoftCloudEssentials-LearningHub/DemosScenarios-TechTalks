# Connecting Microsoft Fabric to On-Premises MySQL

Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

----------

> Securely connect your remote-hosted MySQL database to Microsoft Fabric, leveraging encryption to protect your data.

## Wiki 

- [MySQL database connector overview](https://learn.microsoft.com/en-us/fabric/data-factory/connector-mysql-database-overview)
- [Set up your MySQL database connection](https://learn.microsoft.com/en-us/fabric/data-factory/connector-mysql-database)
- [Security in Microsoft Fabric](https://learn.microsoft.com/en-us/fabric/security/security-overview)
- [Microsoft Fabric end-to-end security scenario](https://learn.microsoft.com/en-us/fabric/security/security-scenario)

## How to setup 

- Step 1: Prepare Your MySQL Database: Make sure that any prerequisites for the MySQL database are installed or set up before connecting
  1. **Ensure MySQL is Accessible**: Verify that your MySQL database is accessible from the internet. You might need to configure your firewall settings to allow connections from Microsoft Fabric's IP ranges.
  2. **Create a MySQL User for Fabric**: Create a dedicated MySQL user with the necessary permissions to access the required databases and tables.
- Step 2: Set Up the On-Premises Data Gateway: This gateway can be used by Data Factory dataflows and data pipelines to securely ingest and transform data
  1. **Download and Install the Gateway**:
     - Go to the [Microsoft Data Gateway download page](https://powerbi.microsoft.com/en-us/gateway/) and download the on-premises data gateway.
     - Install the gateway on a machine that has network access to your MySQL database.
  2. **Configure the Gateway**:
     - During installation, sign in with your Microsoft Entra ID (formerly Azure AD) account.
     - Register the gateway with your Microsoft Fabric environment.
- Step 3: Configure the MySQL Connector in Microsoft Fabric
  1. **Open Microsoft Fabric**: Navigate to the Microsoft Fabric portal and go to the Data Factory section.
     
     <img width="219" alt="image" src="https://github.com/user-attachments/assets/be07d64c-5adc-4a60-970b-76dee9020ddf">

  2. **Create a New Dataflow**: In Data Factory, create a new dataflow and select the option to add a new data source. This allows you to ingest, prepare, and transform data

       <img width="550" alt="image" src="https://github.com/user-attachments/assets/aa27c48b-6126-4a52-8d62-070c9bc1a207">

  3. **Select MySQL Connector**: Choose the MySQL connector from the list of available connectors.

       <img width="550" alt="image" src="https://github.com/user-attachments/assets/b77616f3-66c2-4635-9d6e-483235c8b535">

  4. **Enter Connection Details**:
     - Provide the server name, database name, and the credentials for the MySQL user you created earlier.
     - Ensure that the connection string includes SSL parameters to enforce encryption.
     - Secure the Connection
        1. All interactions with Microsoft Fabric are encrypted by default and authenticated using Microsoft Entra ID. Data at rest is also stored encrypted.
        2. Ensure that the communication between your MySQL database and Microsoft Fabric travels through secure channels, leveraging the encryption you already have in place between the cloud and your local network.
        3. **Verify SSL/TLS Encryption**: Ensure that your MySQL server is configured to support SSL/TLS connections. You might need to update your MySQL configuration file (`my.cnf` or `my.ini`) to enable SSL.
        4. **Test the Connection**: Use the test connection feature in Microsoft Fabric to ensure that the connection is successful and encrypted.

      <img width="550" alt="image" src="https://github.com/user-attachments/assets/e149a2b0-7559-4db9-911f-5e3902f264ff">

- Step 4: Create and Schedule Dataflows
  1. **Design Your Dataflow**: Use Power Query to design your dataflow, specifying the tables and columns you want to import from MySQL.
  2. **Transform Data as Needed**: Apply any necessary transformations to your data within the dataflow.
  3. **Schedule Data Refresh**: Set up a schedule for your dataflow to refresh the data at regular intervals.
- Step 5: Monitor and Maintain
  1. **Monitor Dataflows**: Regularly monitor the status of your dataflows to ensure they are running smoothly.
  2. **Update Gateway and Connectors**: Keep your on-premises data gateway and MySQL connectors up to date to ensure compatibility and security.

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-393-limegreen" alt="Total views">
  <p>Refresh Date: 2025-07-18</p>
</div>
<!-- END BADGE -->