# Microsoft Azure Fundamentals (AZ-900) --- Study Notes

> **Exam alignment:** These notes follow Microsoft's AZ-900 skills
> measured as of **July 20, 2026**. Always check the official study
> guide before booking because Microsoft can update the exam objectives.

## Exam overview

AZ-900 validates foundational knowledge of cloud computing, Azure
architecture and services, and Azure management and governance. It is a
fundamentals-level certification; prior Azure experience is not
required.


## AZ-900 Exam Structure

| Skill Area | Exam Weight |
|---|---:|
| Describe Cloud Concepts | 25–30% |
| Describe Azure Architecture and Services | 35–40% |
| Describe Azure Management and Governance | 30–35% |


Microsoft currently lists a 45-minute exam duration and a passing score
of 700 or higher. Check the exam page for current delivery details,
pricing, and policies.

------------------------------------------------------------------------

# 1. Describe cloud concepts (25--30%)

## 1.1 What is cloud computing?

Cloud computing is the delivery of computing services---such as servers,
storage, databases, networking, and software---over the internet,
usually with usage-based pricing.

**Example:** Instead of buying and maintaining a physical server in an
office, a company can create an Azure Virtual Machine and pay for the
resources it consumes.

### Benefits of cloud computing

-   **High availability:** Services are designed to remain accessible
    with minimal downtime.
-   **Scalability:** Increase or decrease resources to meet demand.
-   **Elasticity:** Automatically or quickly add and remove resources as
    demand changes.
-   **Reliability:** Cloud platforms use redundant infrastructure and
    recovery capabilities to help services continue operating.
-   **Predictability:** Monitoring, analytics, and service design help
    estimate performance and costs.
-   **Security:** Cloud providers offer security capabilities, but
    customers still have security responsibilities.
-   **Governance:** Apply policies, controls, and standards across cloud
    resources.
-   **Manageability:** Manage resources through portals, APIs,
    command-line tools, and automation.

### Scalability vs. elasticity

| Term | Meaning | Example |
|---|---|---|
| **Scalability** | The ability to handle increased or decreased workloads by adding or removing resources. | Increasing a VM's size (CPU/RAM) or adding more VM instances to handle increased traffic. |
| **Elasticity** | The ability to automatically adjust resources dynamically based on workload demand. | Automatically adding VM instances during a traffic spike and removing them when traffic decreases. |


### High availability vs. disaster recovery

-   **High availability (HA):** Minimize service downtime, often by
    using redundant components or availability zones.
-   **Disaster recovery (DR):** Restore services and data after a major
    failure or disaster, often using backups or replicated resources.

### Fault tolerance 
- **Fault tolerance:** Fault tolerance is the ability of a system to continue operating even when a component fails. It generally requires redundancy and careful
architecture.

## 1.2 Cloud expenditure models

### CapEx --- Capital Expenditure

Money spent upfront on physical assets, such as servers, networking
equipment, and data-center facilities.

**Example:** Purchasing 10 physical servers for an organization's data
center.

### OpEx --- Operational Expenditure

Ongoing operating costs, often paid as services are consumed.

**Example:** Paying an Azure bill each month based on virtual machines,
storage, and network usage.

**Remember:** Traditional on-premises infrastructure often involves
significant CapEx. Cloud services commonly shift spending toward OpEx.

## 1.3 Consumption-based model

You pay for the cloud resources you use rather than purchasing all
infrastructure in advance.

**Examples:** - Pay for VM compute while it is allocated or running,
according to the service's billing rules. - Pay for storage based on
capacity and operations. - Pay for certain serverless functions based on
executions and resource consumption.

Always check the specific service's pricing details; billing is not
identical across all Azure services.

## 1.4 Cloud deployment models

| Model | Description | Example Use Case |
|---|---|---|
| **Public Cloud** | Cloud services delivered over the provider's infrastructure and shared platform. | Hosting a public website in Microsoft Azure. |
| **Private Cloud** | A cloud environment dedicated to a single organization. | An organization requires dedicated control or needs to meet specific security and compliance requirements. |
| **Hybrid Cloud** | A combination of private/on-premises infrastructure and public cloud services. | Keeping a legacy database on-premises while hosting an application in Azure. |


**Exam tip:** Hybrid cloud connects environments. It does not simply
mean using two public-cloud providers.

## 1.5 Shared responsibility model

Security and operational responsibilities are divided between the cloud
provider and the customer. The division depends on the service model.

| Responsibility | On-Premises | IaaS | PaaS | SaaS |
|---|---|---|---|---|
| Physical Data Center | Customer | Microsoft | Microsoft | Microsoft |
| Physical Network | Customer | Microsoft | Microsoft | Microsoft |
| Physical Hosts | Customer | Microsoft | Microsoft | Microsoft |
| Operating System | Customer | Customer | Microsoft | Microsoft |
| Applications | Customer | Customer | Customer | Microsoft manages the application; customer manages its usage and configuration. |
| Data and Identities | Customer | Customer | Customer | Customer |


The table is a learning guide; exact responsibilities vary by service
and configuration. Customers remain responsible for protecting their
data, identities, access, and appropriate configuration.

## 1.6 Cloud service models

### IaaS --- Infrastructure as a Service

Provides virtualized infrastructure such as virtual machines, storage,
and networking. The customer manages the operating system, applications,
and much of the configuration.

**Azure examples:** Azure Virtual Machines, virtual networks, and
managed disks.

**Use case:** You need control over the operating system and installed
software.

### PaaS --- Platform as a Service

Provides a managed platform for building, deploying, and running
applications. The provider manages much of the underlying infrastructure
and operating system.

**Azure examples:** Azure App Service, Azure SQL Database, and Azure
Functions (serverless platform capability).

**Use case:** Developers want to deploy code without managing servers
and operating systems.

### SaaS --- Software as a Service

A ready-to-use application delivered over the internet. The provider
manages the application and underlying infrastructure.

**Examples:** Microsoft 365, Outlook.com, and Dynamics 365.

**Use case:** Users need software without installing and maintaining the
application infrastructure.

### IaaS vs. PaaS vs. SaaS

| Model | Customer Mainly Manages | Provider Mainly Manages |
|---|---|---|
| **IaaS** | Operating system, applications, data, and configuration. | Physical infrastructure and virtualization. |
| **PaaS** | Applications, data, and application configuration. | Infrastructure, operating system, runtime, and platform. |
| **SaaS** | Data, users, access, and application configuration. | Application and underlying infrastructure/platform. |


## 1.7 Serverless computing

Serverless lets developers run code or services without managing the
underlying servers. Servers still exist; the cloud provider manages
them.

**Examples:** 
- **Azure Functions:** Run event-driven code.
- **Azure Logic Apps:** Build workflows and integrate services.
- **Azure Container Apps:** Run containerized applications with managed infrastructure and scaling capabilities.

Serverless services often use consumption-based or workload-based pricing, depending on the service and plan.

------------------------------------------------------------------------

# 2. Describe Azure architecture and services (35--40%)

## 2.1 Azure global infrastructure

### Regions

A region is a geographical area containing one or more Azure datacenters
connected through a low-latency network.

**Example:** Central India, South India, and West India are Azure region
names.

Choose a region based on latency, service availability, data residency
requirements, and cost.

### Availability zones

An Availability Zone is a physically separate location within an Azure region.

Each Availability Zone has independent:
- Power supply
- Cooling system
- Networking
- Infrastructure

**Key point:** `Availability Zones` provide protection against datacenter-level failures, whereas `Availability Sets` protect against certain hardware failures within a datacenter.

### Region pairs

Some Azure regions are paired with another region in the same geography
(where possible) to support certain disaster-recovery and
platform-update strategies.

Do not assume every service automatically replicates data to the paired
region. Replication and failover behavior depend on the service and
configuration.

### Sovereign regions

Special Azure cloud environments designed for specific government,
national, or regulatory requirements. They are separate from the
standard public Azure cloud.

### Datacenters

Physical facilities that contain servers, storage, networking, power,
and cooling systems used to deliver cloud services.

## 2.2 Azure resource hierarchy

Understand this hierarchy:

``` text
Microsoft Entra tenant
└── Management Group(s)
    └── Subscription(s)
        └── Resource Group(s)
            └── Resource(s)
```

-   **Resource:** An individual Azure item, such as a VM, virtual
    network, storage account, or database.
-   **Resource group:** A logical container for resources that are
    managed together.
-   **Subscription:** A billing and management boundary. Resources
    belong to a subscription.
-   **Management group:** Organizes multiple subscriptions so governance
    policies and access controls can be applied at scale.
-   **Microsoft Entra tenant:** The identity boundary associated with an
    organization.

**Important:** A resource group belongs to one subscription. A resource
can be moved between resource groups in some supported cases, but
resource-group placement and dependencies matter.

### Resource groups --- practical example

For a three-tier application, a resource group might contain: - Web-tier
virtual machines or App Service resources - Application-tier resources -
A database resource - Supporting networking resources

You can organize resources by application, environment, department, or
lifecycle.

## 2.3 Azure compute services

Compute services provide processing power to run applications,
workloads, and code.

### Azure Virtual Machines (VMs)

An Azure VM is an on-demand virtual server.

Common use cases: 
- Hosting Windows or Linux applications
- Running custom software
- Migrating existing server workloads
- Applications requiring OS-level control

A VM commonly needs: 
- VM size (CPU and memory)
- Operating system image - Disk(s)
- Virtual network and subnet
- Network interface
- Authentication and security configuration


### Types of Azure Virtual Machines

Azure provides different types of Virtual Machines based on workload requirements, such as general-purpose applications, compute-intensive workloads, memory-intensive applications, and GPU-based processing.

| VM Type | Description | Common Use Cases |
|---|---|---|
| **General Purpose** | Provides a balanced ratio of CPU, memory, and networking resources. | Web servers, development environments, small databases, and application servers. |
| **Compute Optimized** | Provides a high CPU-to-memory ratio. | Batch processing, application servers, and compute-intensive workloads. |
| **Memory Optimized** | Provides a high memory-to-CPU ratio. | Large databases, in-memory analytics, and memory-intensive applications. |
| **Storage Optimized** | Provides high disk throughput and I/O performance. | Big data processing, data warehousing, and heavy transactional workloads. |
| **GPU Optimized** | Provides GPU capabilities for parallel processing. | AI/ML workloads, deep learning, graphics rendering, and video processing. |
| **HPC Optimized** | Designed for high-performance computing with powerful CPUs and high-speed networking. | Scientific simulations, engineering workloads, and complex computational tasks. |

### Azure VM Size Families

Azure uses VM size families to identify the hardware configuration and intended workload.

| VM Series | Category | Description |
|---|---|---|
| **A-series** | General Purpose | Entry-level VMs for development, testing, and small workloads. |
| **B-series** | General Purpose (Burstable) | Suitable for workloads with variable CPU usage that can burst when needed. |
| **D-series** | General Purpose | Balanced CPU and memory for enterprise applications and web servers. |
| **F-series** | Compute Optimized | High CPU-to-memory ratio for compute-intensive applications. |
| **E-series** | Memory Optimized | High memory-to-CPU ratio for memory-intensive workloads. |
| **L-series** | Storage Optimized | High disk throughput and I/O performance. |
| **N-series** | GPU Optimized | VMs equipped with GPUs for AI, machine learning, and graphics workloads. |
| **H-series** | HPC Optimized | Designed for high-performance computing workloads. |

### Common Azure VM Components

A VM commonly requires:

- **VM Size:** Defines the number of vCPUs, memory, and other performance characteristics.
- **Operating System Image:** Windows Server or Linux operating system.
- **OS Disk:** Stores the operating system.
- **Data Disks:** Additional disks used to store application data.
- **Virtual Network (VNet):** Provides network connectivity.
- **Subnet:** A logical subdivision of a virtual network.
- **Network Interface (NIC):** Connects the VM to a virtual network.
- **Public IP Address (Optional):** Allows connectivity from the internet when configured.
- **Network Security Group (NSG):** Controls inbound and outbound network traffic.
- **Authentication:** Uses SSH keys, passwords, or supported identity-based methods.

### Important VM Concepts for AZ-900

| Concept | Description |
|---|---|
| **vCPU** | Virtual CPU allocated to a VM. |
| **VM Size** | Determines CPU, memory, storage capabilities, and network performance. |
| **OS Disk** | Disk that contains the operating system. |
| **Data Disk** | Additional disk for application or user data. |
| **Temporary Disk** | Local storage intended for temporary data; data may be lost during certain maintenance or redeployment events. |
| **Managed Disks** | Azure-managed block storage used by virtual machines. |
| **VM Image** | Template containing an operating system and optionally preconfigured software. |

**security types**: Azure virtual machines offer three security types that determine the level of `boot and runtime protection`. Boot protection focuses on "whether the system is clean at startup," while runtime protection focuses on "whether data is safe during operation.

### VM Scale Sets

Azure Virtual Machine Scale Sets let you deploy and manage a group of
load-balanced VMs that can scale based on demand or a defined
configuration.

**Example:** Add VM instances when application traffic increases.

### Availability Sets

An Availability Set is a logical grouping of Azure VMs that helps protect them against hardware failures and planned maintenance.

Azure distributes VMs across two concepts:
- **Fault Domains (FD):** Protect against physical hardware failures. (max 3 = FD0, FD1, FD2)
- **Update Domains (UD):** Protect against planned maintenance and updates. (max 20 = UD0 UD1..)

**Important:** Availability Sets protect against certain hardware failures and planned maintenance within a datacenter. They do not protect against an entire datacenter outage.

### Azure Virtual Desktop (AVD)

A desktop and application virtualization service that provides users
access to Windows desktops and applications hosted on Azure.

### Containers

Containers package an application and its dependencies so it can run
consistently across environments.

Azure container services include: 
- **Azure Container Instances (ACI):** Run containers without managing VMs or a container orchestrator.
- **Azure Kubernetes Service (AKS):** Managed Kubernetes for orchestrating containerized applications.
- **Azure Container Apps:** Managed platform for containerized applications, with built-in scaling and application capabilities.
- **Azure Container Registry (ACR):** Store and manage container images.

### Azure Functions

A serverless compute service for event-driven code. It can execute in
response to events such as HTTP requests, timers, queue messages, or
storage events.

### Compute comparison

| Service | Best Understood As |
|---|---|
| **Azure Virtual Machines (VMs)** | Full virtual servers with OS-level control. |
| **VM Scale Sets** | Groups of VMs that can automatically scale based on demand. |
| **Azure Kubernetes Service (AKS)** | Managed Kubernetes service for container orchestration. |
| **Azure Container Instances (ACI)** | Run individual container workloads without managing an orchestrator. |
| **Azure Container Apps** | Managed application platform for running containerized applications. |
| **Azure App Service** | Managed hosting service for web applications and APIs. |
| **Azure Functions** | Serverless compute service for running event-driven code. |
| **Azure Virtual Desktop (AVD)** | Cloud-based virtual desktops and applications. |


## 2.4 Application hosting options

-   **Azure App Service:** Host web applications, REST APIs, and mobile
    back ends without managing the underlying servers.
-   **Virtual Machines:** Use when you need OS-level control or have
    legacy requirements.
-   **Containers:** Package and run applications consistently.
-   **AKS:** Use when you need Kubernetes orchestration and control over
    container workloads.
-   **Azure Functions:** Use for event-driven tasks and serverless
    execution.

## 2.5 Azure networking

### Virtual Network (VNet)

An Azure Virtual Network is a logically isolated network in Azure. It enables Azure resources to communicate with each other, the internet, and on-premises networks when connectivity is configured, (Maximum 1000 Vnet we can create in an account).

In all VNet, Starting 4 IPs are reserved and last one is also reserved.

- 10.0.0.0 Network ID
- 10.0.0.1 default gateway
- 10.0.0.2 dns
- 10.0.0.3 dns
- 10.0.0.255 broadcast 


### Subnet

A subnet divides a VNet into smaller IP address ranges. You can place
resources in different subnets and apply network controls,  (Maximum 3000 Subnets we can create in a VNet).

### VNet peering

Connects two Azure virtual networks so resources can communicate using
private IP addresses over the Microsoft backbone.

Peering is not the same as a VPN connection. VNet peering does not
require a VPN gateway.

### Network Security Group (NSG)

An NSG (Network Security Group) is a virtual firewall in Azure that controls inbound and outbound network traffic using security rules.

NSG (Network Security Group) can be associated at both levels:

- 1. Subnet level – Applies to network traffic for resources within that subnet.
- 2. NIC level – Applies to traffic for the specific VM's Network Interface Card.

**AWS vs Azure Networking Comparison**

| Feature | AWS Security Group | AWS NACL | Azure NSG |
|---|---|---|---|
| Allow rules | Yes | Yes | Yes |
| Deny rules | No | Yes | Yes |
| Stateful | Yes | No (Stateless) | Yes |
| Rule evaluation | Aggregated rules | Priority-based | Priority-based |
| Applied to | Network Interface (ENI) | Subnet | Subnet or Network Interface (NIC) |

**Important Difference: Stateful vs Stateless**

**AWS Security Group and Azure NSG (Stateful)**

Both AWS Security Groups and Azure NSGs are stateful.

**Example:**

- You allow inbound SSH traffic on port 22.
- The response traffic is automatically allowed.
- You don't need to create a separate outbound rule for the SSH response traffic.

**AWS NACL (Stateless)**

AWS Network ACLs are stateless.

**Example:**

- You allow inbound SSH traffic on port 22.
- You must also allow the required outbound response traffic through outbound rules.
- NACLs do not automatically allow response traffic.


### Azure DNS

Provides DNS hosting and name resolution services: 
- **Azure DNS:** Host DNS domains and manage DNS records.
- - **Azure Private DNS:** Provide name resolution within virtual networks.

### VPN Gateway

Connects Azure virtual networks to other networks through encrypted
tunnels over the internet.

Common scenarios: 
- Site-to-site VPN: Connect an on-premises network to Azure.
- Point-to-site VPN: Connect an individual client device to Azure.
- VNet-to-VNet VPN: Connect VNets using VPN gateways.

### ExpressRoute

Provides a private connection between an organization's network and
Microsoft cloud services through a connectivity provider. It does not
send traffic over the public internet in the same way as a typical VPN
connection.

**VPN vs. ExpressRoute:** VPN uses encrypted tunnels over the internet;
ExpressRoute uses private connectivity through a provider.

### Public endpoint vs. private endpoint

-   **Public endpoint:** A service is reachable through a public IP
    address or public network endpoint, subject to access controls.
-   **Private endpoint:** Uses a private IP address in your VNet through
    Azure Private Link to access a service privately.

A private endpoint does not automatically disable the service's public
network access; configure that separately when required.

------------------------------------------------------------------------

# 3. Azure storage services

Azure Storage is a cloud storage service used to store different types of data, such as files, documents, images, videos, backups, and virtual machine disks.

For the AZ-104 (Azure Administrator Associate) exam, understand storage services, redundancy options, access tiers, storage accounts, and security configurations.

## 3.1 Azure Storage Account

An Azure Storage Account is a container that provides a unique namespace for storing data in Azure.

It provides access to different Azure storage services.

### Main Storage Services

| Service | Purpose | AWS Equivalent |
|---|---|---|
| Blob Storage | Stores unstructured data | Amazon S3 |
| Azure Files | Managed file shares | Amazon EFS / FSx |
| Queue Storage | Stores messages | Amazon SQS |
| Table Storage | NoSQL key-value data | Amazon DynamoDB (conceptually) |
| Disk Storage | VM disks | Amazon EBS |

**Important Points:**
- Each storage account has a globally unique name.
- Storage account names must be lowercase.
- Storage account names must be 3–24 characters.
- Storage accounts are created in a specific Azure region.
- You can configure redundancy, networking, and security.

## 3.2 Types of Azure Storage Services

### A. Azure Blob Storage

Blob Storage is used to store unstructured data such as images, videos, documents, log files, and backups.

It is commonly used for large amounts of unstructured data.

**Blob Types:**

| Blob Type | Purpose |
|---|---|
| Block Blob | Stores text and binary data; commonly used for files and images |
| Append Blob | Optimized for append operations; useful for log files |
| Page Blob | Stores random-access data; used for Azure VM disks |

**Important Exam Points:**
- Block Blob → General file storage.
- Append Blob → Logging data.
- Page Blob → Random read/write operations, commonly used for VM disks.

### B. Azure Files

Azure Files provides fully managed file shares in the cloud.

**Supported Protocols:**
- SMB
- NFS (for supported configurations)

**Use Cases:**
- Shared files between multiple virtual machines.
- Migrating on-premises file servers to Azure.
- Sharing files between applications.

**Important Exam Points:**
- Supports SMB and NFS.
- Can be mounted by multiple VMs.
- Supports hybrid access using Azure File Sync.
- Azure File Sync synchronizes on-premises Windows Server file shares with Azure Files.

**AWS Equivalent:** Amazon EFS (conceptually; Azure Files also supports SMB workloads).

### C. Azure Queue Storage

Queue Storage stores messages that applications can process asynchronously.

**Example:**
1. Application sends a message to a queue.
2. Queue stores the message.
3. Another application reads the message.
4. The application processes the task.

**Use Cases:**
- Background processing.
- Decoupling application components.
- Asynchronous communication.

**AWS Equivalent:** Amazon SQS.

### D. Azure Table Storage

Azure Table Storage is a NoSQL key-value storage service used to store structured, non-relational data.

**Important Points:**
- Does not require a fixed relational database schema.
- Stores data as entities.
- Uses PartitionKey and RowKey to identify entities.
- Suitable for large amounts of semi-structured data.

**AWS Equivalent:** Amazon DynamoDB (conceptually).

### E. Azure Managed Disks

Managed Disks provide block-level storage for Azure Virtual Machines.

**Important Points:**
- Used as OS disks and data disks.
- Azure manages the underlying storage infrastructure.
- Supports different performance tiers.
- Can create snapshots and disk backups.

**AWS Equivalent:** Amazon EBS.

## 3.3 Azure Blob Storage Access Tiers

Access tiers help optimize storage costs based on how frequently data is accessed.

| Tier | Usage | Storage Cost | Access Cost |
|---|---|---|---|
| Hot | Frequently accessed data | Higher | Lower |
| Cool | Infrequently accessed data | Lower | Higher |
| Cold | Rarely accessed data | Even lower | Higher |
| Archive | Rarely accessed, long-term data | Lowest | Highest |

**Important Exam Points:**
- Hot → Frequently accessed data.
- Cool → Infrequently accessed data; minimum 30-day retention.
- Cold → Rarely accessed data; minimum 90-day retention.
- Archive → Long-term storage; minimum 180-day retention.
- Archive data is offline and must be rehydrated before reading.
- Rehydration can take hours depending on priority and data size.

**Examples:**
- Website images accessed frequently → Hot.
- Monthly reports → Cool.
- Old business records → Cold.
- Long-term compliance backups → Archive.

## 3.4 Storage Redundancy

| Type | Description |
|---|---|
| LRS | 3 copies in one data center |
| ZRS | 3 copies across availability zones |
| GRS | LRS + secondary region |
| GZRS | ZRS + secondary region |

**Additional Options:**
- RA-GRS → Read access to secondary region.
- RA-GZRS → Read access to secondary region.

**Remember:**
- LRS = Local
- ZRS = Zones
- GRS = Regions
- GZRS = Zones + Regions

## 3.5 Performance Tiers

| Type | Description |
|---|---|
| Standard | General-purpose storage |
| Premium | SSD-based, high performance |

## 3.6 Storage Account Types

| Type | Purpose |
|---|---|
| Standard GPv2 | Blob, Files, Queue, Table |
| Premium Block Blobs | High-performance blobs |
| Premium File Shares | High-performance files |
| Premium Page Blobs | High-performance page blobs |

## 3.7 Storage Security

**Access Methods:**
- Access Keys → Two keys providing broad storage account access.
- SAS → Temporary, restricted access to storage resources.
- Entra ID / RBAC → Identity-based access.

### SAS Types

- User Delegation SAS → Entra ID.
- Service SAS → Specific storage resource.
- Account SAS → Multiple supported storage services.

### RBAC Roles

- Reader → Read blob data.
- Contributor → Read, write, delete.
- Owner → Full blob data control.

**Additional Security Features:**
- Encryption → Enabled by default; supports customer-managed keys.
- Network Security → Firewall, VNet rules, Private Endpoint.

## 3.8 Lifecycle Management

Automatically moves or deletes blobs based on rules.

**Example:** Hot → Cool → Archive → Delete.

**Purpose:** Reduce storage costs.

## 3.9 Azure File Sync

Synchronizes on-premises Windows Server files with Azure Files.

**Important Components:**
- Cloud Endpoint → Azure file share.
- Server Endpoint → On-premises folder.
- Sync Group → Synchronization relationship.
- Cloud Tiering → Keeps frequently used files locally.

## 3.10 Quick Service Comparison

| Requirement | Service |
|---|---|
| Images, videos, documents | Blob Storage |
| Shared files | Azure Files |
| Messages | Queue Storage |
| NoSQL data | Table Storage |
| VM disks | Managed Disks |
| File synchronization | Azure File Sync |
| Temporary access | SAS |
| Identity-based access | RBAC |
| Automatic blob movement | Lifecycle Management |
| Zone protection | ZRS |
| Regional protection | GRS |
| Zone + regional protection | GZRS |
| Secondary region read access | RA-GRS / RA-GZRS |





------------------------------------------------------------------------

# 4. Azure identity, access, and security

## 4.1 Microsoft Entra ID

Microsoft Entra ID (formerly Azure Active Directory) is Microsoft's
cloud identity and access management service.

It helps manage: - Users and groups - Application identities -
Authentication - Single sign-on - Conditional Access - Identity
protection capabilities

It is not simply a traditional Windows Server Active Directory domain
controller hosted in the cloud.

## 4.2 Microsoft Entra Domain Services

Provides managed domain services such as domain join, Group Policy,
LDAP, and Kerberos/NTLM authentication for compatible workloads, without
requiring you to deploy and manage domain controllers yourself.

## 4.3 Authentication concepts

-   **Authentication:** Proves who a user or workload is.
-   **Authorization:** Determines what that identity is allowed to do.
-   **Single sign-on (SSO):** Sign in once and access multiple
    applications without repeatedly entering credentials.
-   **Multifactor authentication (MFA):** Requires more than one
    verification factor.
-   **Passwordless authentication:** Uses methods such as passkeys,
    security keys, or biometrics rather than a conventional password.
-   **External identities:** Enables people outside your organization to
    access resources under controlled identity arrangements.

## 4.4 Conditional Access

Microsoft Entra Conditional Access evaluates signals---such as user,
location, device, and risk---and applies access policies.

**Example:** Require MFA when an employee signs in from an unfamiliar
location.

Conditional Access is commonly described as an identity-based policy
engine.

## 4.5 Azure role-based access control (Azure RBAC)

Azure RBAC controls who can perform which actions on Azure resources and
at what scope.

Key concepts: - **Security principal:** User, group, service principal,
or managed identity receiving access. - **Role definition:** Collection
of allowed actions. - **Scope:** Where the access applies (management
group, subscription, resource group, or resource). - **Role
assignment:** Associates a principal with a role at a scope.

Common built-in roles: - **Owner:** Full access, including the ability
to assign roles. - **Contributor:** Create and manage resources, but
cannot grant access to others. - **Reader:** View resources without
making changes. - **User Access Administrator:** Manage user access to
Azure resources.

**Least privilege:** Give identities only the permissions they need.

## 4.6 Zero Trust

Zero Trust is a security approach based on: 1. Verify explicitly. 2. Use
least-privilege access. 3. Assume breach.

Do not automatically trust a user or device just because it is inside a
corporate network.

## 4.7 Defense in depth

Uses multiple security layers so that if one control fails, other
controls can still help protect the environment.

Typical layers include: - Physical security - Identity and access -
Perimeter/network - Compute - Application - Data

## 4.8 Microsoft Defender for Cloud

A cloud security posture management and workload protection service that
helps assess security posture, identify recommendations, and protect
supported workloads across cloud environments.

It can help identify misconfigurations and security risks. It does not
replace good identity, network, patching, or application security
practices.

------------------------------------------------------------------------

# 5. Describe Azure management and governance (30--35%)

## 5.1 Azure cost management

Azure costs can be affected by: - Resource type and size - Region -
Usage duration - Storage capacity and access tier - Network data
transfer - Licensing - Pricing model - Redundancy and availability
choices

### Azure Pricing Calculator

Use the Pricing Calculator to estimate the expected cost of Azure
services before deployment.

It is useful for planning and comparing configurations. It is an
estimate, not a guarantee of the final bill.

### Azure Cost Management

Use Cost Management capabilities to analyze, monitor, and manage cloud
spending.

Common capabilities include: - Cost analysis - Budgets - Alerts - Cost
recommendations - Cost exports and reporting

### Azure tags

Tags are key-value pairs applied to resources to help organize and
report on them.


**Example:** Azure Resource Tags

| Tag | Value |
|---|---|
| **Environment** | Production |
| **Department** | Finance |
| **Owner** | PlatformTeam |
| **Application** | OnlineStore |


Tags can help with cost allocation, ownership, and automation. Tags do
not automatically reduce costs or enforce governance by themselves.

## 5.2 Governance and compliance

### Microsoft Purview

A family of data governance, risk, and compliance capabilities that
helps organizations discover, understand, govern, and protect data
across supported environments.

For AZ-900, remember its purpose at a high level: data governance and
compliance.

### Azure Policy

Helps create, assign, and manage rules that enforce organizational
standards and assess compliance.

**Example:** Require resources to be deployed only in approved Azure
regions.

Policy can audit, deny, or deploy related configuration depending on the
policy effect and scenario.

### Resource locks

Help prevent accidental deletion or modification of Azure resources.

-   **CanNotDelete:** Authorized users can read and modify the resource,
    but cannot delete it while the lock applies.
-   **ReadOnly:** Authorized users can read the resource but cannot
    modify or delete it while the lock applies.

Locks do not replace RBAC. A lock and permissions solve different
problems.

## 5.3 Managing and deploying Azure resources

### Azure portal

A web-based graphical interface for creating, configuring, monitoring,
and managing Azure resources.

### Azure Cloud Shell

A browser-accessible shell for managing Azure resources. It supports
Azure CLI and Azure PowerShell and provides an authenticated
environment.

### Azure CLI

A cross-platform command-line tool for managing Azure resources.
Commands commonly begin with `az`.

Example:

``` bash
az login
az group list
az vm list
```

### Azure PowerShell

A PowerShell-based set of modules for managing Azure resources.

Example:

``` powershell
Connect-AzAccount
Get-AzResourceGroup
Get-AzVM
```

### Azure Arc

Extends Azure management and governance capabilities to resources
outside Azure, including on-premises and supported multicloud
environments.

**Example:** Apply governance and monitoring approaches to servers that
are not hosted in Azure.

### Infrastructure as Code (IaC)

IaC means defining infrastructure through code or declarative
configuration files instead of creating every resource manually.

Benefits: - Repeatable deployments - Version control - Consistency -
Automation - Easier review and collaboration

### Azure Resource Manager (ARM)

Azure Resource Manager is the deployment and management service for
Azure. It provides a consistent management layer for creating, updating,
and deleting resources.

### ARM templates

JSON files that declaratively describe Azure infrastructure and
configuration to deploy.

**Exam distinction:** ARM is the management/deployment layer; ARM
templates are files that describe the resources to deploy.

------------------------------------------------------------------------

# 6. Azure monitoring tools

## 6.1 Azure Advisor

Provides personalized recommendations to help improve Azure environments
across areas such as: - Reliability - Security - Performance -
Operational excellence - Cost

**Example:** Advisor may recommend resizing an underutilized VM to
reduce cost.

## 6.2 Azure Service Health

Provides information about Azure service issues, planned maintenance,
and health advisories that may affect your resources.

It helps answer: "Is an Azure platform issue affecting my services?"

## 6.3 Azure Monitor

A monitoring service for collecting, analyzing, and acting on telemetry
from Azure and supported environments.

It includes metrics, logs, alerts, and related monitoring capabilities.

### Metrics

Numerical measurements collected over time, such as CPU percentage,
network throughput, and request count.

### Logs and Log Analytics

Logs contain records and events that can be queried and analyzed. Log
Analytics workspaces store log data for analysis using Kusto Query
Language (KQL).

### Azure Monitor alerts

Notify or trigger actions when a monitored condition is met.

**Example:** Create an alert when VM CPU usage remains above a defined
threshold.

### Application Insights

An application performance monitoring (APM) feature of Azure Monitor. It
helps monitor application availability, performance, failures,
dependencies, and user-related telemetry.

### Monitoring tools --- quick comparison

| Tool | Main Purpose |
|---|---|
| **Azure Monitor** | Collects, analyzes, and monitors telemetry data from Azure resources and applications. |
| **Log Analytics** | Queries and analyzes log data using Kusto Query Language (KQL). |
| **Azure Monitor Alerts** | Sends notifications or triggers automated actions when defined conditions are met. |
| **Application Insights** | Monitors application performance, availability, dependencies, and failures. |
| **Azure Advisor** | Provides personalized recommendations for cost, security, reliability, performance, and operational excellence. |
| **Azure Service Health** | Provides information about Azure service incidents, planned maintenance, and health advisories. |


------------------------------------------------------------------------

# 7. High-value exam comparisons

  
# 7. High-Value Exam Comparisons

| Compare | Key Difference |
|---|---|
| **Region vs. Availability Zone** | A Region is a geographical area containing Azure datacenters, while an Availability Zone is a physically separate location within a region. |
| **Availability Set vs. Availability Zone** | Availability Sets distribute VMs across fault and update domains, while Availability Zones provide datacenter-level separation. |
| **Scalability vs. Elasticity** | Scalability means increasing or decreasing capacity, while elasticity automatically adjusts capacity based on demand. |
| **High Availability (HA) vs. Disaster Recovery (DR)** | HA minimizes service downtime, while DR focuses on restoring services after a major disruption. |
| **IaaS vs. PaaS vs. SaaS** | Provider management increases from IaaS to SaaS, while customer infrastructure management decreases. |
| **VNet Peering vs. VPN Gateway** | VNet Peering connects VNets over Microsoft's backbone, while VPN Gateway connects networks using encrypted VPN tunnels. |
| **VPN Gateway vs. ExpressRoute** | VPN Gateway uses encrypted tunnels over the internet, while ExpressRoute provides private connectivity through a connectivity provider. |
| **Public Endpoint vs. Private Endpoint** | A Public Endpoint uses a public network endpoint, while a Private Endpoint uses a private IP address through Azure Private Link. |
| **Blob Storage vs. Azure Files** | Blob Storage is object storage for unstructured data, while Azure Files provides managed file shares. |
| **Azure Migrate vs. Azure Data Box** | Azure Migrate helps assess and migrate workloads to Azure, while Data Box transfers large amounts of data using physical devices. |
| **Microsoft Entra ID vs. Entra Domain Services** | Entra ID provides cloud identity and access management, while Entra Domain Services provides managed domain capabilities such as LDAP, Kerberos, and Group Policy. |
| **Authentication vs. Authorization** | Authentication verifies identity, while Authorization determines what an identity is allowed to access or do. |
| **Azure RBAC vs. Azure Policy** | Azure RBAC controls who can perform actions on resources, while Azure Policy enforces and evaluates organizational standards. |
| **Resource Lock vs. RBAC** | Resource Locks help prevent accidental deletion or modification, while RBAC controls user permissions. |
| **Azure Advisor vs. Azure Service Health** | Azure Advisor provides personalized recommendations, while Service Health provides information about Azure service incidents and planned maintenance. |
| **Azure Monitor vs. Application Insights** | Azure Monitor provides broad monitoring capabilities, while Application Insights focuses on application performance, availability, and failures. |


------------------------------------------------------------------------

# 8. Scenario-based practice questions

1.  **A company wants to run a custom Linux server and install its own
    packages. Which service?**\
    Azure Virtual Machines (IaaS).

2.  **A developer wants to deploy a web application without managing the
    operating system. Which service?**\
    Azure App Service (PaaS).

3.  **A company wants code to execute when a queue message arrives,
    without managing servers. Which service?**\
    Azure Functions.

4.  **A company wants to connect its office network to Azure over an
    encrypted internet connection. Which service?**\
    VPN Gateway.

5.  **A company needs private, dedicated connectivity to Microsoft cloud
    services through a connectivity provider. Which service?**\
    ExpressRoute.

6.  **Two Azure VNets need private connectivity over the Microsoft
    backbone. Which feature?**\
    VNet peering.

7.  **A company wants to restrict deployments to approved regions. Which
    service?**\
    Azure Policy.

8.  **An administrator wants to prevent accidental deletion of a
    production database. Which feature?**\
    A `CanNotDelete` resource lock, together with appropriate RBAC
    permissions.

9.  **A company wants recommendations to reduce Azure spending. Which
    service?**\
    Azure Advisor, especially its cost recommendations.

10. **An application team wants to investigate failed requests and slow
    dependencies. Which service?**\
    Application Insights.

11. **A company wants to analyze log records using queries. Which
    service?**\
    Log Analytics.

12. **A company wants to transfer a very large dataset using a physical
    device. Which service?**\
    Azure Data Box.

13. **A company wants to assess and migrate on-premises servers to
    Azure. Which service?**\
    Azure Migrate.

14. **A company wants to manage servers in on-premises and multicloud
    environments through Azure. Which service?**\
    Azure Arc.

15. **A company wants to group subscriptions and apply governance across
    them. Which feature?**\
    Management groups.

------------------------------------------------------------------------

# 9. Short revision checklist

Before taking the exam, make sure you can explain:

-   [ ] Public, private, and hybrid cloud
-   [ ] CapEx, OpEx, and consumption-based pricing
-   [ ] IaaS, PaaS, SaaS, and serverless
-   [ ] Shared responsibility model
-   [ ] Scalability, elasticity, availability, reliability, and disaster
    recovery
-   [ ] Regions, region pairs, availability zones, and sovereign regions
-   [ ] Management groups, subscriptions, resource groups, and resources
-   [ ] VMs, VM Scale Sets, Availability Sets, AVD, containers, AKS, App
    Service, and Functions
-   [ ] VNets, subnets, peering, NSGs, DNS, VPN Gateway, ExpressRoute,
    and endpoints
-   [ ] Blob, Files, Queue, Table, and managed disks
-   [ ] Hot, Cool, Cold, and Archive tiers
-   [ ] LRS, ZRS, GRS, GZRS, RA-GRS, and RA-GZRS
-   [ ] AzCopy, Storage Explorer, Azure File Sync, Azure Migrate, and
    Data Box
-   [ ] Microsoft Entra ID, Entra Domain Services, SSO, MFA, Conditional
    Access, and external identities
-   [ ] Azure RBAC, Zero Trust, defense in depth, and Defender for Cloud
-   [ ] Pricing Calculator, Cost Management, budgets, and tags
-   [ ] Microsoft Purview, Azure Policy, and resource locks
-   [ ] Azure portal, Cloud Shell, CLI, PowerShell, Arc, IaC, ARM, and
    ARM templates
-   [ ] Azure Advisor, Service Health, Monitor, Log Analytics, alerts,
    and Application Insights

------------------------------------------------------------------------

# 10. Suggested study plan

A practical 7-day revision plan:

  -----------------------------------------------------------------------
  Day                                 Focus
  ----------------------------------- -----------------------------------
  1                                   Cloud concepts, deployment models,
                                      service models, shared
                                      responsibility

  2                                   Azure global infrastructure and
                                      resource hierarchy

  3                                   Compute and networking

  4                                   Storage and migration tools

  5                                   Identity, access, and security

  6                                   Cost management, governance,
                                      deployment, and monitoring

  7                                   Revise comparisons, take a practice
                                      assessment, and review weak areas
  -----------------------------------------------------------------------

Try to create a few resources in the Azure portal if you have access to
an Azure subscription. Set a budget and delete test resources when
finished to avoid unexpected charges.

------------------------------------------------------------------------

# Official Microsoft resources

-   [AZ-900 official exam
    page](https://learn.microsoft.com/credentials/certifications/exams/az-900/)
-   [Official AZ-900 study guide and skills
    measured](https://learn.microsoft.com/credentials/certifications/resources/study-guides/az-900)
-   [Microsoft Learn: Introduction to Cloud
    Infrastructure](https://learn.microsoft.com/training/paths/microsoft-azure-fundamentals-describe-cloud-concepts/)
-   [Azure Pricing
    Calculator](https://azure.microsoft.com/pricing/calculator/)
-   [Azure free account](https://azure.microsoft.com/free/)

> **Study advice:** AZ-900 is a fundamentals exam. Focus on
> understanding what each service does, when to use it, and how it
> differs from similar services. Do not spend most of your preparation
> time memorizing command syntax.
