# SQL Management Tools - Overview 

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com) 
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2024-11-19

----------

<details>
<summary><b>List of References</b> (Click to expand)</summary>

- [Try Azure SQL Managed Instance for free (preview)](https://learn.microsoft.com/en-us/azure/azure-sql/managed-instance/free-offer?view=azuresql)
- [Try the Next-gen GP Azure SQL Managed Instance for free](https://techcommunity.microsoft.com/t5/azure-sql-blog/try-the-next-gen-gp-azure-sql-managed-instance-for-free/ba-p/4136933)
- [SSMS components and configuration - SQL Server Management Studio](https://learn.microsoft.com/en-us/sql/ssms/tutorials/ssms-configuration?view=sql-server-ver16)
- [How to Download and Install DBeaver on Windows](https://www.youtube.com/watch?v=BMGdkmWOvNY)
- [HeidiSQL with MariaDB and MySQL](https://www.youtube.com/watch?v=11vhRYEfHNE)
- [How to install Adminer (Database Administration Tool) on Ubuntu 22.04](https://www.youtube.com/watch?v=r4keak825B4)

</details>

| **Category**           | **Tool**                         | **Company**        | **Description**| **Key Features**| **When to Use**|
|----------|-----------|----------------------------------|--------------------------------------|-------------------------|-------------------------|
| **On-Premises**        | - SQL Server Management Studio (SSMS) <br/> - DBeaver | - MS <br/> - DBeaver Corp | - Comprehensive tool for managing Microsoft SQL Server components. <br/> - Universal database management tool supporting various databases with a user-friendly interface. | - Full GUI support, rich script editors for T-SQL, integration with Azure, performance monitoring tools <br/> - Supports multiple databases, advanced SQL editor, data visualization tools | - Ideal for managing SQL Server environments on-premises. <br/> - Suitable for managing multiple types of databases with a consistent interface. |
| **Third-Party Clouds** | - Adminer <br/> - HeidiSQL       | - Adminer <br/> - HeidiSQL Project | - Lightweight, full-featured database management tool deployable as a single PHP file. <br/> - Open-source tool for managing MySQL, MariaDB, and SQL Server databases. | - Simple deployment, supports multiple databases, user-friendly interface <br/> - Easy-to-use interface, advanced query editor, data export/import capabilities | - Best for quick, lightweight database management tasks. <br/> - Ideal for managing MySQL, MariaDB, and SQL Server databases with a free, open-source tool. |
| **Azure**              | - Azure Data Studio <br/> - Azure SQL Managed Instance | Microsoft | - Cross-platform database tool with modern editor experience and integrated terminal. <br/> - Fully managed PaaS database offering with a free trial for 12 months. | - Supports SQL Server and Azure SQL Database, integrated terminal, extensions, built-in charting <br/> - Automated backups, high compatibility with SQL Server, high availability, scalable performance | - Perfect for cross-platform environments needing a modern, extensible tool. <br/> - Best for migrating SQL Server workloads to the cloud with minimal changes and benefiting from PaaS. |

> [!NOTE]
> Make sure you have configured the network access, adding your IP as part of the whitelist.
     
<img width="600" alt="image" src="https://github.com/user-attachments/assets/68429f6f-9793-4f2d-9e7f-8c5db6f0621d">

## On-Premises Tools

### SQL Server Management Studio (SSMS)

>  A comprehensive tool for managing Microsoft SQL Server components.

1. **Download and Install:**
   - Go to the [SQL Server Management Studio download page](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms).
   - Click on the download link and run the installer.
   - Follow the installation prompts to complete the setup.
  
   <img width="700" height="370" alt="image" src="https://github.com/user-attachments/assets/c5908fc0-30d7-4146-ae20-ab62d8694d1f">
  
2. **Connect to a Server:**   
   - Open SSMS and click on`Connect` in the Object Explorer.
   - Enter your server name and authentication details.

      <img width="700" height="370" alt="image" src="https://github.com/user-attachments/assets/f39b6c01-40e6-4fa5-92c6-70e4ae41d914">

4. **Manage Databases:**
   - Use the Object Explorer to navigate and manage your databases.
   - Right-click on databases to create new ones, run queries, or perform other management tasks.

      <img width="700" height="370" alt="image" src="https://github.com/user-attachments/assets/17b25f48-ca70-4c95-8cdc-870d6a19f80d">

### **DBeaver**

> A universal database management tool supporting various databases with a user-friendly interface.

1. **Download and Install:**
   - Visit the [DBeaver download page](https://dbeaver.io/download/).
   - Choose the appropriate version for your operating system and install it.
2. **Create a Database Connection:**
   - Open DBeaver and click on`New Database Connection.`
   - Select your database type and enter the connection details.
3. **Run SQL Queries:**
   - Use the SQL Editor to write and execute queries.
   - View results in the results pane.

## Third-Party Clouds

### **Adminer**

> A lightweight, full-featured database management tool deployable as a single PHP file.

1. **Download Adminer:**
   - Download the latest version from the [Adminer website](https://www.adminer.org/).
2. **Deploy Adminer:**
   - Upload the PHP file to your web server.
   - Access it via your web browser.
3. **Connect to a Database:**
   - Enter your database connection details on the Adminer login page.
   - Manage your database through the Adminer interface.

### **HeidiSQL**
>  An open-source tool for managing MySQL, MariaDB, and SQL Server databases.

1. **Download and Install:**
   - Go to the [HeidiSQL download page](https://www.heidisql.com/download.php).
   - Download and run the installer.
2. **Create a New Session:**
   - Open HeidiSQL and click on`New` to create a new session.
   - Enter your database connection details.
3. **Manage Databases:**
   - Use the interface to browse, query, and manage your databases.

## Azure Tools

### **Azure Data Studio**
>  A cross-platform database tool with a modern editor experience and integrated terminal.

1. **Download and Install:**
   - Download Azure Data Studio from the [official website](https://docs.microsoft.com/en-us/sql/azure-data-studio/download-azure-data-studio).
   - Follow the installation instructions for your operating system.

      <img width="700" height="370" alt="image" src="https://github.com/user-attachments/assets/4a08ee70-9fd2-441e-a501-c50eedabc87a">

2. **Connect to a Database:**
   - Open Azure Data Studio and click on `New Connection.`
   - Enter your database connection details.
  
      <img width="700" height="370" alt="image" src="https://github.com/user-attachments/assets/f8bc7b1e-890c-44b0-a7ee-197dc390130b">

3. **Use the Editor:**
   - Write and execute SQL queries in the editor.
   - View results and manage your database.

      <img width="700" height="370" alt="image" src="https://github.com/user-attachments/assets/423390f0-60e0-466d-8250-1b71183aa4e7">

### **Azure SQL Managed Instance**

> A fully managed PaaS database offering with a free trial for 12 months.

1. **Create an Azure Account:**
   - Sign up for a free Azure account at [Azure Free Account](https://azure.microsoft.com/en-us/free/).
2. **Create a SQL Managed Instance:**
   - Go to the Azure portal and navigate to `SQL Managed Instances.`
   - Click on `Create` and follow the prompts to set up your instance.
     
      <img width="550"  alt="image" src="https://github.com/user-attachments/assets/c7e60ee0-b0e4-4f23-9aa7-c10349071474">

3. **Connect and Manage:**
   - Use Azure Data Studio or SSMS to connect to your managed instance.
   - Perform database management tasks as needed.

<div align="center">
  <h3 style="color: #4CAF50;">Total Visitors</h3>
  <img src="https://profile-counter.glitch.me/brown9804/count.svg" alt="Visitor Count" style="border: 2px solid #4CAF50; border-radius: 5px; padding: 5px;"/>
</div>
