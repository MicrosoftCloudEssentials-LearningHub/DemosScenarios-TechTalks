# Azure Data Storage Overview 

Costa Rica

[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

----------

## Products 

These products are designed to store, retrieve and manage data. They can handle various types of data such as files, images, videos, etc.

```mermaid
graph TB
    A[Azure Storage Platform]
    B[Azure Blobs]
    C[Azure Files]
    D[Azure Elastic SAN]
    E[Azure Queues]
    F[Azure Tables]
    G[Azure managed Disks]
    H[Azure Container Storage ]
    I[Includes support for big data analytics through Data Lake Storage Gen2]
    A --> B
    A --> C
    A --> D
    A --> E
    A --> F
    A --> G
    A --> H
    B --> I
```

| Product | Description | Use Cases | Related Products (tendency used with) |
| --- | --- | --- | --- |
| **Azure Disk Storage** | High-performance, durable block storage for business-critical applications [1](https://azure.microsoft.com/en-us/services/storage/disks/). | Used for structured data [1](https://azure.microsoft.com/en-us/services/storage/disks/). | Works with VMs and applications [1](https://azure.microsoft.com/en-us/services/storage/disks/). |
| **Azure Blob Storage** | Massively scalable and secure object storage for cloud-native workloads, archives, data lakes, high-performance computing, and machine learning [2](https://azure.microsoft.com/en-us/services/storage/blobs/). | Used for unstructured data [2](https://azure.microsoft.com/en-us/services/storage/blobs/). Ideal for backing up or archiving data, hosting and streaming of multimedia content, big data analytics, caching and content delivery for websites [3](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction). | Can be integrated with Azure Machine Learning and Azure Content Delivery Network [3](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction). |
| **Azure Data Lake Storage** | Massively scalable and secure data lake for your high-performance analytics workloads [4](https://learn.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction). | Used for big data analytics [4](https://learn.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction). Ideal for storing massive amounts of data in any format for analytic workloads [5](https://learn.microsoft.com/en-us/azure/storage/files/storage-files-introduction). | Built on Azure Blob Storage [4](https://learn.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction). |
| **Azure Files** | Simple, secure, and serverless enterprise-grade cloud file shares [6](https://azure.microsoft.com/en-us/products/storage/files/). | Used for file sharing, home directories, databases, high-performance computing [6](https://azure.microsoft.com/en-us/products/storage/files/). Ideal for shared file storage for collaboration across a geographically dispersed area, lift-and-shift to the cloud of applications that use native APIs and SMB, replacing or supplementing on-prem file servers [3](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction). | Can be cached on Windows servers with Azure File Sync for fast access [6](https://azure.microsoft.com/en-us/products/storage/files/). |
| **Azure Elastic SAN** | A cloud-native Storage Area Network (SAN) service built on Azure [15](https://azure.microsoft.com/en-us/products/storage/elastic-san/). | Used for general purpose databases, streaming and messaging services, CD/CI environments, and other tier 1/tier 2 workloads [15](https://azure.microsoft.com/en-us/products/storage/elastic-san/). | Works with Azure Virtual Machines, Azure VMware Solutions, and Azure Kubernetes Service [16](https://learn.microsoft.com/en-us/azure/storage/elastic-san/elastic-san-introduction). |
| **Azure Container Storage** | Manage persistent storage volumes for stateful container applications [17](https://azure.microsoft.com/en-us/products/container-storage/). | Used for running high scale stateful workloads on containers [17](https://azure.microsoft.com/en-us/products/container-storage/). Ideal for running business-critical, enterprise-grade applications on Kubernetes in the cloud  [18](https://learn.microsoft.com/en-us/azure/storage/container-storage/container-storage-introduction). | Works with Azure Kubernetes Service, Azure VMware Solution [17](https://azure.microsoft.com/en-us/products/container-storage/). |
| **Microsoft OneDrive** | A personal cloud storage service from Microsoft that allows users to store files and personal data like Windows settings or BitLocker recovery keys in the cloud. | Used for personal data storage. | Works with Microsoft products. |
| **Azure NetApp Files** | Enterprise-grade Azure file shares, powered by NetApp [7](https://learn.microsoft.com/en-us/azure/azure-netapp-files/azure-netapp-files-introduction). | Used for file sharing, home directories, databases, high-performance computing [8](https://azure.microsoft.com/en-us/products/netapp/). Ideal for running high scale stateful workloads on containers [7](https://learn.microsoft.com/en-us/azure/azure-netapp-files/azure-netapp-files-introduction). | Works with multiple types of compute resources such as Azure Virtual Machines, Azure VMware Solutions, and Azure Kubernetes Service [8](https://azure.microsoft.com/en-us/products/netapp/). |
| **Azure File Sync** | Hybrid cloud file shares for caching your on-premises data [9](https://learn.microsoft.com/en-us/azure/storage/file-sync/file-sync-introduction). | Used for file sharing, home directories, databases, high-performance computing [8](https://azure.microsoft.com/en-us/products/netapp/). Ideal for improving server recovery times and giving employees the ability to work without interruptions [10](https://learn.microsoft.com/en-us/azure/storage/file-sync/file-sync-deployment-guide). | SMB Azure file shares can be cached on Windows servers [9](https://learn.microsoft.com/en-us/azure/storage/file-sync/file-sync-introduction). |
| **Azure Stack Edge** | Cloud storage gateway to transfer data efficiently and easily between the cloud and the edge [11](https://azure.microsoft.com/en-us/products/azure-stack/edge/). | Used for machine learning at the edge, edge and IoT solutions, network data transfer from edge to cloud [12](https://learn.microsoft.com/en-us/azure/databox-online/azure-stack-edge-deploy-aks-on-azure-stack-edge). | Works with Azure Kubernetes Service, Azure Batch, and Azure Machine Learning [11](https://azure.microsoft.com/en-us/products/azure-stack/edge/). |
| **Azure Data Box** | Appliances and solutions for transferring data into and out of Azure quickly and cost-effectively [13](https://azure.microsoft.com/en-us/products/databox/). | Used for onetime migration, initial bulk transfer, periodic uploads [14](https://learn.microsoft.com/en-us/azure/databox/data-box-overview). | Works with Azure Storage [13](https://azure.microsoft.com/en-us/products/databox/). |

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-1532-limegreen" alt="Total views">
  <p>Refresh Date: 2025-10-23</p>
</div>
<!-- END BADGE -->