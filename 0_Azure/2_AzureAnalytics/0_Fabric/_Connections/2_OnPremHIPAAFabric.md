# Integrating On-Premises Data into Microsoft Fabric

Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

----------

## Wiki 

- [How to access on-premises data sources in Data Factory/Microsoft Fabric](https://learn.microsoft.com/en-us/fabric/data-factory/how-to-access-on-premises-data)
- [Integrating On-Premises Data into Microsoft Fabric Using Data Pipelines - Blog](https://blog.fabric.microsoft.com/en-us/blog/integrating-on-premises-data-into-microsoft-fabric-using-data-pipelines-in-data-factory?ft=All)

## HIPAA Audit Requirements

`HIPAA -> Health Insurance Portability and Accountability Act of 1996`

Ensuring HIPAA compliance when connecting on-premises data to Microsoft Fabric is crucial for protecting sensitive health information. Here are some steps and considerations to meet HIPAA requirements:

| **Category**                | **Details**                                                                                                                                       |
|-----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| **Data Encryption**         | - **In Transit:** Use TLS (Transport Layer Security) to encrypt data as it moves between your on-premises environment and Microsoft Fabric.  <br/> - **At Rest:** Ensure that data stored in Microsoft Fabric is encrypted using strong encryption methods.                                            |
| **Access Controls**         | - **Role-Based Access Control (RBAC):** Implement RBAC to restrict access to sensitive data based on user roles and responsibilities.       <br/> - **Multi-Factor Authentication (MFA):** Use MFA to add an extra layer of security for accessing data and systems.                                  |
| **Audit Logs**              | - **Logging and Monitoring:** Enable detailed logging and monitoring to track access and changes to sensitive data. This helps in detecting and responding to potential security incidents. <br/> - **Regular Audits:** Conduct regular audits to ensure compliance with HIPAA requirements and to identify any potential vulnerabilities.            |
| **Data Minimization**       | - **Limit Data Collection:** Only collect and transfer the minimum necessary data required for your purposes.   <br/> - **Data Anonymization:** Where possible, anonymize or de-identify data to reduce the risk of exposure.                                             |
| **Business Associate Agreement (BAA)** | **Sign a BAA with Microsoft:** Ensure that you have a signed Business Associate Agreement with Microsoft, which outlines their responsibilities in protecting your data. |
| **Training and Awareness**  | - **Staff Training:** Provide regular training to your staff on HIPAA compliance and data protection best practices.   <br/> - **Awareness Programs:** Implement awareness programs to keep staff informed about the importance of data security and compliance.                 |

## How to connect 

> General Considerations: <br/>
> - **Business Associate Agreement (BAA)**: Have a signed BAA with Microsoft to ensure they are also compliant with HIPAA requirements. <br/>
> - **Regular Audits**: Conduct regular audits to ensure compliance to maintain compliance across the method. <br/>
> - **Training and Awareness**: Provide staff training and implement awareness programs. 

There are a few methods to connect on-premises data to Microsoft Fabric:

| **Method**                  | **Considerations for HIPAA Compliance**                                                                                                                                                                                                 |
|-----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **On-Premises Data Gateway**| - **Encryption**: Ensure data is encrypted in transit and at rest. <br> - **Access Controls**: Implement RBAC and MFA. <br> - **Audit Logs**: Enable detailed logging and monitoring.                                                   |
| **VPN Gateway**             | - **Secure Network Connection**: Use site-to-site VPN for secure data transfer. <br> - **Encryption**: Ensure data is encrypted in transit.                                                                                              |
| **Azure Data Factory**      | - **Self-hosted Integration Runtime**: Securely connect to on-premises data sources with encryption and access controls. <br> - **Pipeline Security**: Ensure data pipelines are secure and monitored.                                    |
| **Azure ExpressRoute**      | - **Private Connection**: Provides a secure, private connection that bypasses the public internet. <br> - **Encryption**: Ensure data is encrypted in transit.                                                                           |
| **Azure Data Box**          | - **Physical Security**: Ensure the physical device is securely handled and shipped. <br> - **Encryption**: Data on the device should be encrypted.                                                                                      |

### On-Premises Data Gateway

> To connect your on-premises data to Microsoft Fabric, you can use the On-Premises Data Gateway. Enabling seamless data flow between your local environment and the cloud.

1. **Install the On-Premises Data Gateway**: Download and install the gateway on a local machine within your network. You can find detailed instructions on how to do this [here](https://learn.microsoft.com/en-us/fabric/data-factory/how-to-access-on-premises-data).
2. **Configure the Gateway**:
    - Sign In: After installation, sign in with your Microsoft account.
    - Register Gateway: Register the gateway with your Microsoft Fabric account. This will link the gateway to your Fabric environment.
    - Network Configuration: Ensure the gateway is configured to only allow connections from specific internal IP addresses for added security.
3. **Create a Connection for Your On-Premises Data Source**:
   - Navigate to the admin portal in Microsoft Fabric.
   - Select the settings icon (gear icon) at the top right of the page.
   - Choose "Manage connections and gateways" from the dropdown menu.
     
        <img width="550" alt="image" src="https://github.com/user-attachments/assets/0acdb168-c806-45f2-8f77-6562f9ec258b">

   - In the New connection dialog, select "On-premises" and provide your gateway cluster, resource type, and relevant information.

        <img width="550" alt="image" src="https://github.com/user-attachments/assets/d0d4fe16-e3cf-4c47-b7d6-a5ffb9cae60b">

3. **Connect Your On-Premises Data Source to a Dataflow Gen2**:
   - Go to your workspace and create a Dataflow Gen2.

       <img width="550" alt="image" src="https://github.com/user-attachments/assets/aa27c48b-6126-4a52-8d62-070c9bc1a207">

   - Add a new source to the dataflow and select the connection you established in the previous step.

       <img width="550" alt="image" src="https://github.com/user-attachments/assets/b77616f3-66c2-4635-9d6e-483235c8b535">

   - Perform any necessary data transformations and add a destination for your data.
4. **Using On-Premises Data in a Pipeline**:
   - Create a Data Pipeline in your workspace.
   - Add a new source to the pipeline copy activity and select the connection established earlier.
   - Choose a destination for your data from the on-premises source and run the pipeline.

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-9-limegreen" alt="Total views">
  <p>Refresh Date: 2025-07-17</p>
</div>
<!-- END BADGE -->