# Azure Security Groups - Overview 

Costa Rica

[![GitHub](https://badgen.net/badge/icon/github?icon=github&label)](https://github.com)
[![GitHub](https://img.shields.io/badge/--181717?logo=github&logoColor=ffffff)](https://github.com/)
[brown9804](https://github.com/brown9804)

Last updated: 2025-07-17

----------

## Wiki 

<details>
<summary><b>Table of Wiki </b> (Click to expand)</summary>

- [Network security groups](https://learn.microsoft.com/en-us/azure/virtual-network/network-security-groups-overview)
- [How network security groups filter network traffic](https://learn.microsoft.com/en-us/azure/virtual-network/network-security-group-how-it-works)
- [Create, edit, or delete a security group in the Microsoft 365 admin center](https://learn.microsoft.com/en-us/microsoft-365/admin/email/create-edit-or-delete-a-security-group?view=o365-worldwide)
- [Create, change, or delete a network security group](https://learn.microsoft.com/en-us/azure/virtual-network/manage-network-security-group?tabs=network-security-group-portal)

</details>


## Creating a Network Security Group (NSG) in Azure

> A Network Security Group (NSG) in Azure acts as a `virtual firewall to control inbound and outbound traffic to Azure resources`

| **Aspect**                        | **Description**                                                                                                                                                                                                 |
|-----------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Associations**                  | - `Subnets and Network Interfaces`: NSGs can be associated with subnets or individual network interfaces within a virtual network. This allows for granular control over traffic.<br>- `Multiple Associations`: The same NSG can be associated with multiple subnets and network interfaces. |
| **Stateful Nature**               | - `Stateful Rules`: NSGs are stateful, meaning if an inbound rule allows traffic, the response traffic is automatically allowed, and vice versa. This reduces the need for additional rules.                                                      |
| **Augmented Security Rules**      | - `Simplified Management`: Augmented rules allow for specifying multiple IP addresses, ranges, and ports in a single rule, simplifying the management of complex security policies.                                                              |
| **Service Tags and Application Security Groups** | - `Service Tags`: These represent a group of IP address prefixes from specific Azure services, reducing the complexity of managing IP addresses in security rules.<br>- `Application Security Groups`: These allow you to group VMs and define security policies based on these groups, making it easier to manage security at scale. |
| **Best Practices**                | - `Minimal Rules`: Use the least number of rules necessary to reduce complexity.<br>- `Regular Audits`: Regularly review and update NSG rules to ensure they meet current security requirements.<br>- `Effective Use of Tags`: Utilize service tags and application security groups to simplify rule management. |


1. `Sign in to the Azure Portal`: Go to [portal.azure.com](portal.azure.com) and sign in with your Azure account.
2. `Navigate to Network Security Groups`: In the search bar at the top, type `Network security groups` and select it from the results.
3. `Create a New NSG`: Click on `+ Create`.
4. `Fill in the Details`:
   - `Subscription`: Select your Azure subscription.
   - `Resource Group`: Choose an existing resource group or create a new one.
   - `Name`: Enter a name for your NSG.
   - `Region`: Select the region where you want to create the NSG.
5. `Review and Create`: Click on `Review + create`, then `Create` after validation passes.


## Adding Security Rules to the NSG


| **Aspect**                | **Description**                                                                                                                                                                                                 |
|---------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Inbound and Outbound Rules** | NSGs contain rules that allow or deny traffic based on specified criteria such as source and destination IP addresses, ports, and protocols.                                                                 |
| **Five-Tuple Information**     | Each rule is based on five pieces of information: source, source port, destination, destination port, and protocol.                                                                                           |
| **Priority**                   | Rules are processed in order of priority, with lower numbers having higher priority. Once traffic matches a rule, processing stops.                                                                           |
| **Default Rules**              | Azure provides default rules to allow or deny traffic, which can be overridden by custom rules with higher priority.                                                                                          |


1. **Select Your NSG**: After the NSG is created, go to the **Network security groups** section and select your newly created NSG.
2. **Add Inbound/Outbound Rules**:
   - Go to **Inbound security rules** or **Outbound security rules**.
   - Click on **+ Add** to create a new rule.
   - Specify the **Source**, **Source port ranges**, **Destination**, **Destination port ranges**, **Protocol**, and **Action** (Allow or Deny).
   - Click **Add** to save the rule.

## Creating a Security Group in Azure Active Directory (AAD)

> Security Groups in Azure Active Directory (AAD) are used to` manage user and device access to resources`. They simplify the `administration of permissions by grouping users and devices, allowing administrators to assign access rights to the group rather than individual users`. Security Groups can be used for various purposes, such as applying policies, assigning licenses, and managing access to applications and resources. They support dynamic membership, where users are automatically added or removed based on specific criteria, and can be integrated with Conditional Access policies to enhance security.

| **Aspect**                        | **Description**                                                                                                                                                                                                 |
|-----------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Group Types**                   | - `Security`: Used to manage member and device access to shared resources for a group of users.<br>- `Microsoft 365`: Used for collaboration between users, both inside and outside the organization. |
| **Membership Types**              | - `Assigned`: Members are manually added.<br>- `Dynamic User`: Membership is based on user attributes.<br>- `Dynamic Device`: Membership is based on device attributes. |
| **Use Cases**                     | - `Access Management`: Control access to resources like SharePoint, Teams, and applications.<br>- `License Assignment`: Assign licenses to users based on group membership.<br>- `Policy Application`: Apply policies to users or devices in the group. |
| **Integration with Conditional Access** | - `Conditional Access Policies`: Use groups as a decision signal to enforce access controls based on group membership. |
| **Dynamic Membership Rules**      | - `Automatic Updates`: Automatically add or remove users based on defined rules and user attributes. |

1. **Go to Azure Active Directory**: In the Azure portal, navigate to **Azure Active Directory**.
2. **Create a New Group**: Click on **Groups** and then **+ New group**.
3. **Fill in the Group Details**:
   - **Group Type**: Select **Security**.
   - **Group Name**: Enter a name for the group.
   - **Membership Type**: Choose the membership type (e.g., Assigned, Dynamic User, Dynamic Device).
4. **Add Members**: Select the members you want to add to the group.
5. **Create**: Click **Create** to finalize the group creation.

<!-- START BADGE -->
<div align="center">
  <img src="https://img.shields.io/badge/Total%20views-366-limegreen" alt="Total views">
  <p>Refresh Date: 2025-07-17</p>
</div>
<!-- END BADGE -->

