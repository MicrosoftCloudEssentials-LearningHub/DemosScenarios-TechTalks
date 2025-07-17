# HDAP Azure Data resources related - Overview 

> Housing and Disability Advocacy Program (HDAP)

Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-03-23

------------------------------------------

<details>
<summary><b>List of References </b> (Click to expand)</summary>

- [About keys - Key Vault](https://learn.microsoft.com/en-us/azure/key-vault/keys/about-keys)
- [Key types, algorithms, and operations - Key Vault](https://learn.microsoft.com/en-us/azure/key-vault/keys/about-keys-details)
- [Choose an Azure compute service](https://learn.microsoft.com/en-us/azure/architecture/guide/technology-choices/compute-decision-tree)
- [Introduction to Azure Blob Storage](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction)
- [Architecture best practices for Azure Blob Storage](https://learn.microsoft.com/en-us/azure/well-architected/service-guides/azure-blob-storage)
- [SSH File Transfer Protocol (SFTP) support for Azure Blob Storage](https://learn.microsoft.com/en-us/azure/storage/blobs/secure-file-transfer-protocol-support)
- [Choose an Azure compute service](https://learn.microsoft.com/en-us/azure/architecture/guide/technology-choices/compute-decision-tree)
- [Pricing calculator](https://azure.microsoft.com/en-us/pricing/calculator/?msockid=38ec3806873362243e122ce086486339)

</details>


## Azure Key Vault 

> `Azure Key Vault` is a cloud service for securely storing and accessing secrets, such as API keys, passwords, certificates, and cryptographic keys.

> [!NOTE]
> Azure Key Vault is essential for HDAP (Housing and Disability Advocacy Program) as it securely stores and manages sensitive information like API keys, passwords, and certificates. It supports different key types and protection methods, ensuring robust security. It uses Microsoft Entra ID (formerly Azure Active Directory) for authentication and role-based access control (RBAC), providing detailed logs and configurable alerts for monitoring access and usage. 

| Feature | Description |
|---------|-------------|
| **Key Management** | - Supports RSA (Rivest-Shamir-Adleman), EC (Elliptic Curve), and symmetric keys. <br/> - RSA keys can be up to 4096 bits. <br/> - EC keys support various curves like P-256, P-384, and P-521. <br/> - Keys can be software-protected or HSM (Hardware Security Module)-protected. <br/> - Managed HSMs provide single-tenant, highly available HSMs for storing high-value keys. |
| **Secrets Management** | - Securely stores secrets like passwords and connection strings. <br/> - Uses Azure Active Directory (AAD) for authentication. <br/> - Role-based access control (RBAC) to manage permissions. |
| **Certificates Management** | - Automates the creation, import, renewal, and deletion of certificates. <br/> - Integrates with Azure services and third-party certificate authorities. |
| **Monitoring and Logging** | - Provides detailed logs of key and secret usage. <br/> - Configurable alerts for monitoring access and usage. |

## Blob Storage

> **Azure Blob Storage** is an object storage solution optimized for storing large amounts of unstructured data.

| Feature | Description |
|---------|-------------|
| **Storage Tiers** | - Hot Tier for frequently accessed data. <br/> - Cool Tier for infrequently accessed data. <br/> - Archive Tier for rarely accessed data. |
| **Data Access** | - Supports HTTP/HTTPS (Hypertext Transfer Protocol/Secure). <br/> - REST (Representational State Transfer) APIs. <br/> - Azure SDKs (Software Development Kits). <br/> - Tools like AzCopy. |
| **SFTP (SSH File Transfer Protocol) Support** | - Allows secure file transfers using the SSH File Transfer Protocol (SFTP). |
| **Scalability and Performance** | - Provides redundancy options like LRS (Locally Redundant Storage), ZRS (Zone Redundant Storage), and GRS (Geo-Redundant Storage). <br/> - Optimized for high throughput and low latency. |
| **Security** | - Data is encrypted at rest and in transit. <br/> - Uses Azure Active Directory (AAD) and shared access signatures (SAS) for fine-grained access control. |

> Steps to configure it:

<img width="550" alt="image" src="https://github.com/user-attachments/assets/486369a7-df77-47bc-b2b7-d2c66c8e9e49" />

<img width="550" alt="image" src="https://github.com/user-attachments/assets/24e89de2-474c-4af2-814a-aa91af2b4e3a" />

## Azure SFTP Server

> **Azure Blob Storage** now supports SFTP (SSH File Transfer Protocol), enabling secure file transfers to and from Blob Storage.


  https://github.com/user-attachments/assets/375690b5-108f-4f85-ad9c-915ef7c40684

| Feature | Description |
|---------|-------------|
| **Hierarchical Namespace** | - Organizes objects into a hierarchy of directories and subdirectories, similar to a traditional file system. <br/> - Scales linearly without degrading performance. |
| **Authentication** | - Uses local user identities for authentication. <br/> - Users can authenticate using passwords or SSH (Secure Shell) private key credentials. <br/> - Local users can be authorized to access specific containers and directories within Blob Storage. |
| **Configuration** | - SFTP support can be enabled with a single click in the Azure portal. <br/> - Requires a standard general-purpose v2 or premium block blob storage account with hierarchical namespace enabled. <br/> - Provides REST APIs and Azure CLI (Command-Line Interface) commands for managing local users and permissions. |
| **Security** | - SFTP uses port 22 for secure file transfers. <br/> - If SFTP access is not configured, all requests will receive a disconnect from the service. <br/> - Provides logging and monitoring capabilities to track SFTP access and usage. |

## Compute Services with File Server

> **Azure Compute Services** provide virtual machines (VMs) and other compute resources to host applications and services.

<p align="center">
    <img width="550" alt="image" src="https://github.com/user-attachments/assets/ed0e7837-5428-430b-a91d-b33a58a71114">
</p>

From [Choose an Azure compute service](https://learn.microsoft.com/en-us/azure/architecture/guide/technology-choices/compute-decision-tree)

| Feature | Description |
|---------|-------------|
| **VM Types** | - Several VM sizes and types are available. <br/> - Includes general-purpose, compute-optimized, and memory-optimized VMs. |
| **Operating Systems** | - Supports Windows and Linux operating systems. |
| **File Sharing Protocols** | - Supports SMB (Server Message Block) and NFS (Network File System) for file sharing. |
| **Storage Options** | - Can use Azure Disks for persistent storage attached to VMs. |
| **Scalability and Availability** | - Azure Virtual Machine Scale Sets allow you to create and manage a group of identical VMs for high availability and scalability. <br/> - Availability Sets ensure that VMs are distributed across multiple physical servers to avoid single points of failure. |

  
<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-9-limegreen" alt="Total views">
  <p>Refresh Date: 2025-07-16</p>
</div>
<!-- END BADGE -->
