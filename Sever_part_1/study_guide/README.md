# AZ-800 MODULE 1: STUDY GUIDE
## Windows Server Hybrid Core Infrastructure Foundations

---

## TABLE OF CONTENTS
1. [Server Roles and Features](#server-roles-and-features)
2. [Server Manager](#server-manager)
3. [NTFS File System](#ntfs-file-system)
4. [Microsoft Management Console](#microsoft-management-console-mmc)
5. [Disk Management](#disk-management)
6. [File Sharing and Management](#file-sharing-and-management)
7. [Networking Models](#networking-models-workgroups-vs-domains)
8. [Network Components](#network-components)
9. [Active Directory Fundamentals](#active-directory-fundamentals)
10. [PowerShell Introduction](#powershell-introduction)
11. [Virtualization Concepts](#virtualization-concepts)
12. [Cloud Computing Models](#cloud-computing-models)
13. [Storage Spaces](#storage-spaces)
14. [Hybrid Infrastructure](#hybrid-infrastructure)
15. [Azure Integration](#azure-integration)
16. [Summary and Key Takeaways](#summary-and-key-takeaways)

---

## SERVER ROLES AND FEATURES

### Understanding Server Roles

A **server role** represents a major function or service that a server performs. Think of it as the server's primary job—when you install the Active Directory Domain Services role, that server becomes a domain controller. When you install the File Server role, it becomes a centralized file storage system.

**Common Server Roles:**
- **Active Directory Domain Services (AD DS):** Domain controller for authentication and authorization
- **DNS Server:** Name resolution services
- **DHCP Server:** Automatic IP address assignment
- **File Server:** File storage and sharing
- **Web Server (IIS):** Hosts websites and applications
- **Print Server:** Manages network printers

### Understanding Server Features

A **server feature** is a supporting software component that enhances server roles or the operating system but isn't a complete service itself. Features provide functionality that roles need to operate effectively.

**Common Server Features:**
- **.NET Framework:** Application runtime environment
- **BitLocker Drive Encryption:** Disk encryption
- **Failover Clustering:** High availability
- **Windows PowerShell:** Automation and scripting
- **Telnet Client:** Remote terminal access

### Key Distinction

**Server Role = Primary Service** (what the server does)  
**Server Feature = Supporting Component** (what helps roles function)

---

## SERVER MANAGER

**Server Manager** is the centralized management console for installing, configuring, and managing server roles and features. It provides a single interface for managing multiple servers, viewing status, and deploying configurations consistently.

**Key Functions:**
- **Dashboard:** At-a-glance status of all managed servers
- **Role/Feature Installation:** "Add Roles and Features Wizard" with automatic dependency resolution
- **Remote Management:** Manage multiple servers from one location
- **Server Groups:** Organize servers logically for easier management
- **Monitoring:** View events, performance, and service status

**Why it matters:** Server Manager reduces administrative overhead by centralizing management, improving efficiency, and providing consistent interfaces across all servers.

---

## NTFS FILE SYSTEM

**NTFS (New Technology File System)** is Windows' modern file system, designed for multi-user server environments with security, reliability, and advanced features.

### Core Features

**File and Folder Permissions:**
Granular access control—every file/folder can have different permissions for different users or groups. Integrates with Windows security for precise control.

**File Compression:**
Transparent compression/decompression saves disk space without manual zip/unzip operations.

**Disk Quotas:**
Limit disk space per user to prevent any single user from filling the disk. Can be enforced (hard limit) or tracked (soft limit with warnings).

**Encryption (EFS):**
Encrypts files using user credentials—even with physical disk access, encrypted files cannot be read without encryption keys.

**Large File Support:**
Supports extremely large files (up to 16 exabytes) and volumes (256 terabytes), suitable for modern data requirements.

**Reliability:**
- **Journaling:** Logs file system changes for quick recovery after crashes
- **Bad Sector Remapping:** Automatically remaps bad sectors to spare sectors
- **Self-Healing:** Detects and repairs certain corruption automatically

**Why NTFS is essential:** It transforms file storage into a secure, reliable, manageable resource with enterprise-grade capabilities.

---

## MICROSOFT MANAGEMENT CONSOLE (MMC)

**MMC** is a framework providing standardized interfaces for administrative tools called **snap-ins**. Like a web browser displays websites, MMC hosts administrative tools with consistent navigation and menus.

**Key Components:**
- **Console Tree:** Hierarchical navigation (left pane)
- **Details Pane:** Displays contents of selected items (right pane)
- **Actions Pane:** Shows available actions for selected items

**Common Snap-ins:**
- Disk Management
- Computer Management
- Active Directory Users and Computers
- Group Policy Management
- Event Viewer
- Services
- Device Manager

**Custom Consoles:** Create custom MMC consoles with only the snap-ins needed for specific administrative tasks.

**Why MMC matters:** Provides consistency across diverse Windows administration tools, reducing training time and improving efficiency.

---

## DISK MANAGEMENT

### Storage Fundamentals

**Physical Disks** are actual hard drives/SSDs. **Volumes** are usable storage units (C:, D:, etc.) created on those disks.

**Disk Types:**
- **Basic Disks:** Simple, traditional partitions—adequate for basic storage
- **Dynamic Disks:** Advanced features like RAID, volume spanning, and fault tolerance

### RAID Levels

**RAID 0 (Striping):**
- Data split across multiple disks
- **Benefit:** Improved performance
- **Drawback:** No fault tolerance—one disk failure = data loss
- **Use:** Non-critical data needing maximum speed

**RAID 1 (Mirroring):**
- Data duplicated on two disks
- **Benefit:** Fault tolerance (survives one disk failure)
- **Drawback:** 50% storage efficiency
- **Use:** Critical data requiring high availability

**RAID 5 (Striping with Parity):**
- Data and parity across 3+ disks
- **Benefit:** Fault tolerance with better storage efficiency
- **Drawback:** Write performance penalty
- **Use:** File servers, general storage

**RAID 10 (Mirrored Stripes):**
- Combines mirroring and striping
- **Benefit:** Excellent performance and fault tolerance
- **Drawback:** 50% efficiency, requires 4+ disks
- **Use:** High-performance databases

---

## FILE SHARING AND MANAGEMENT

### Shadow Copies

**Shadow Copies** automatically create point-in-time snapshots of files/folders. Users can restore previous versions themselves without IT support—like automatic backups users can access directly.

**Implementation:** Configure per volume, set schedule (default: twice daily), allocate storage space.

### Disk Quotas

Limit disk space per user to prevent storage monopolization.

**Types:**
- **Hard Quotas:** Strictly enforced limits
- **Soft Quotas:** Warnings only

**Configuration:** Set default quotas, individual user quotas, warning levels, and event logging.

### Distributed File System (DFS)

Creates unified namespace for file shares across multiple servers, making file locations transparent to users.

**Benefits:**
- Location transparency
- Redundancy through DFS Replication
- Load balancing across multiple servers
- Simplified management

**Example:** Users access `\\company\files\finance` regardless of which physical server hosts the data.

---

## NETWORKING MODELS: WORKGROUPS VS DOMAINS

### Workgroup Model

Peer-to-peer network where each computer maintains its own user accounts and security database—no centralized management.

**Characteristics:**
- Local user accounts on each computer
- Authentication local to each computer
- Users need separate accounts per computer
- No centralized policy enforcement
- Simple setup, minimal infrastructure

**Best for:** Small offices (≤10 computers) with minimal security requirements.

### Domain Model

Centralized network with Active Directory providing unified management, authentication, and authorization.

**Characteristics:**
- Centralized user account database (Active Directory)
- Single sign-on across all resources
- Centralized management via Group Policy
- Hierarchical structure (OUs, groups)
- Enhanced security through domain-wide policies

**Best for:** Organizations with 10+ computers, centralized management needs, compliance requirements.

### Why Domains Scale Better

Workgroups become unmanageable as organizations grow—imagine managing 200 users × 200 computers = 40,000 accounts! Domains provide one account per user, centralized policies, and simplified administration.

---

## NETWORK COMPONENTS

### Server and Client Services

Windows computers run both **Server** and **Workstation** services simultaneously, enabling peer-to-peer resource sharing.

**Server Service:**
- Enables resource sharing (files, printers)
- Listens for incoming connections
- Manages shared resources

**Workstation Service:**
- Enables accessing shared resources on other computers
- Initiates connections to remote shares
- Handles network authentication

**Example:** When you share a folder, your Server service handles connections. When you access a file server, your Workstation service initiates that connection.

### Network Protocols

**TCP/IP** is the foundational protocol suite for modern networks, defining addressing (IP addresses), data packaging (packets), connections (TCP), and data flow.

---

## ACTIVE DIRECTORY FUNDAMENTALS

**Active Directory Domain Services (AD DS)** is Microsoft's directory service storing information about network resources and providing authentication/authorization services.

### Authentication vs Authorization

**Authentication:** "Who are you?" Verifying identity through username/password.

**Authorization:** "What can you do?" Determining resource access and permitted actions through permissions.

**Example:** Logging into the network verifies your identity (authentication). Trying to open a file checks your permissions (authorization).

### Why Active Directory Matters

Transforms Windows networks into managed, secure infrastructures with:
- Single sign-on
- Centralized management
- Enforced security policies
- Scalability from small business to enterprise
- Flexible hierarchical structure

---

## POWERSHELL INTRODUCTION

**PowerShell** is a command-line shell and scripting language built on .NET, designed for system administration. Unlike older CLIs working with text, PowerShell works with objects—structured data with properties and methods.

### Why PowerShell Matters

- **Automation:** Automate repetitive tasks—what takes hours manually takes minutes with scripts
- **Consistency:** Eliminate human error through automated execution
- **Scalability:** Script configuring 5 servers works equally well for 500 servers
- **Integration:** Deep integration with Windows and Microsoft products

### PowerShell Basics

**Cmdlet Structure:** Consistent "Verb-Noun" naming:
- `Get-Service` - Retrieves service information
- `Stop-Service` - Stops a service
- `Set-Location` - Changes directory
- `New-Item` - Creates new items

**Common Verbs:**
- **Get:** Retrieve information
- **Set:** Change properties
- **New:** Create items
- **Remove:** Delete items
- **Start/Stop:** Control services
- **Enable/Disable:** Activate/deactivate features

**Example Commands:**
```powershell
# Get running services
Get-Service | Where-Object {$_.Status -eq "Running"}

# Get disk information
Get-Disk

# Install Windows Feature
Install-WindowsFeature -Name Web-Server
```

### Objects vs Text

Traditional CLIs output text for humans. PowerShell outputs objects with accessible properties for programmatic manipulation—vastly more powerful for automation.

---

## VIRTUALIZATION CONCEPTS

**Virtualization** creates virtual machines (VMs) that behave like physical computers but run as software on a physical host. Each VM has virtual hardware, OS, and applications while sharing the host's physical hardware.

### The Problem with Physical Servers

Traditional IT dedicates one physical server per service, wasting resources. Most servers use only 10-20% of capacity while requiring physical space, power, cooling, and maintenance.

### How Virtualization Solves This

**Server consolidation**—running multiple VMs on fewer physical hosts. Instead of 10 servers at 15% utilization, run 10 VMs on 2 hosts at 75% utilization.

**Benefits:**
- Resource efficiency and better hardware utilization
- Cost savings (less hardware, power, cooling, space)
- Flexibility (deploy VMs in minutes)
- Isolation (VM problems don't affect others)
- Portability (VMs are files—easily copied, moved, backed up)
- Quick test/development environments

### Hyper-V Overview

Microsoft's virtualization platform built into Windows Server. Type 1 (bare-metal) hypervisor running directly on hardware for maximum performance.

**Key Features:** Windows/Linux guest support, Live Migration, virtual networking, Dynamic Memory, integration with Azure.

---

## CLOUD COMPUTING MODELS

Cloud computing delivers computing services over the Internet, eliminating the need to own and maintain physical infrastructure.

### Infrastructure as a Service (IaaS)

Provides virtual infrastructure (VMs, storage, networking) that you manage.

**You Control:** OS, applications, configuration, security, patching  
**Provider Controls:** Physical hardware, virtualization, data center facilities

**Example:** Rent Azure VM—you install software and manage configuration, but don't manage physical hardware.

**Use Cases:** Dev/test environments, custom applications, disaster recovery, temporary capacity.

### Platform as a Service (PaaS)

Provides platform for developing/deploying applications without managing infrastructure.

**You Control:** Application code, configuration, data  
**Provider Controls:** OS, runtime environment, web server, middleware, hardware

**Example:** Azure App Service—upload your code, Azure handles infrastructure, scaling, load balancing.

**Use Cases:** Web apps, APIs, mobile backends, applications needing auto-scaling.

### Software as a Service (SaaS)

Delivers complete applications over the Internet.

**You Control:** Your data, user permissions, configuration options  
**Provider Controls:** Application software, infrastructure, security, updates

**Examples:** Microsoft 365, Salesforce, Zoom, Dropbox

**Use Cases:** Standard business applications, quick deployment, no customization needed.

### Comparison

| Aspect | IaaS | PaaS | SaaS |
|--------|------|------|------|
| Control | Maximum | Medium | Minimal |
| Flexibility | High | Moderate | Limited |
| Management | You manage most | Provider manages most | Provider manages all |
| Examples | Azure VMs | Azure App Service | Microsoft 365 |

**Principle:** More control = more management responsibility.

---

## STORAGE SPACES

**Storage Spaces** is Windows Server storage virtualization—pools physical disks into storage pools, then creates virtual disks with software-defined resilience.

### Why Storage Spaces Exists

Traditional RAID depends on expensive hardware controllers that can fail and lock you into specific vendors. Storage Spaces provides **software-defined storage** using Windows rather than hardware.

**Advantages:**
- Works with any disks (SATA, SAS, SSD, NVMe)
- No proprietary hardware dependency
- Flexible configuration
- Simpler management
- Better Windows integration

### Resiliency Types

**Simple:** No redundancy, maximum capacity (100%), use for non-critical data

**Mirror:** Data duplicated, 50% efficiency (2-way) or 33% (3-way), best performance, use for databases

**Parity:** Data + parity information, ~66-80% efficiency (single) or ~50-75% (dual), use for file servers

### Storage Tiers

Combines SSDs and HDDs—hot data automatically migrates to fast SSD storage, cold data stays on cheaper HDDs. Provides SSD performance at near-HDD cost.

---

## HYBRID INFRASTRUCTURE

**Hybrid infrastructure** combines on-premises servers with cloud services, using each where it makes most sense.

### Why Hybrid Makes Sense

- **Flexibility:** Use on-premises for low latency/data sovereignty, cloud for scalability/DR
- **Gradual Migration:** Move to cloud incrementally
- **Compliance:** Keep regulated data on-premises, use cloud for other purposes
- **Cost Optimization:** On-premises for steady workloads, cloud for variable workloads
- **Disaster Recovery:** Use cloud as DR site without second data center

### Example Scenario

**Retail Company:**
- **On-Premises:** Point-of-sale systems (low latency), financial systems (data sovereignty)
- **Azure:** E-commerce (scalable for traffic spikes), backup/DR, dev/test
- **Integration:** Azure AD Connect synchronizes identities for SSO across environments

---

## AZURE INTEGRATION

Microsoft Azure integrates deeply with on-premises Windows Server, enabling hybrid scenarios.

### Key Azure Services

**Azure Virtual Machines:** Run Windows Server VMs in cloud for temporary workloads, DR, or permanent hosting.

**Azure Site Recovery:** Replicate on-premises VMs to Azure for disaster recovery with minimal RTO/RPO.

**Azure Backup:** Cloud-based backup for on-premises servers without tape drives or separate infrastructure.

**Azure Active Directory:** Cloud identity service synchronizing with on-premises AD for hybrid identity and SSO.

**Azure Files:** SMB file shares in cloud, accessible anywhere.

**Azure Arc:** Extends Azure management to on-premises servers—manage using Azure tools and policies.

### Deployment Considerations

- **Network connectivity:** VPN or ExpressRoute for hybrid scenarios
- **Identity synchronization:** Azure AD Connect for unified identity
- **Security:** Encryption, access controls, compliance requirements
- **Cost management:** Monitor and optimize Azure resource usage

---

## SUMMARY AND KEY TAKEAWAYS

### Foundation Concepts

Module 1 establishes the foundational knowledge for Windows Server administration. Understanding these concepts is crucial because everything else builds upon them.

### Server Roles vs Features

Remember: **Roles are primary services, Features are supporting components.** Roles define what a server does for others; Features enhance how it does it. This distinction appears throughout Windows Server management.

### Centralization Theme

A consistent theme emerges: **centralization improves management.** Server Manager centralizes server administration. Domains centralize account management. Active Directory centralizes authentication. PowerShell centralizes automation. This centralization reduces overhead, improves consistency, and enables scalability.

### Workgroups vs Domains

The shift from workgroup to domain represents a fundamental change in network architecture—from peer-to-peer to centralized management. Domains introduce complexity but provide massive benefits at scale: single sign-on, centralized policies, simplified administration. Most organizations with more than 10 computers benefit from domains.

### PowerShell's Importance

PowerShell isn't just another command line—it's the future of Windows administration. As environments grow, manual configuration becomes impossible. PowerShell enables automation that's essential for modern IT operations. Many Windows Server features can only be fully configured via PowerShell.

### Physical vs Virtual

Virtualization fundamentally changed IT infrastructure. The ability to run multiple servers on one physical host improves resource utilization, reduces costs, and increases flexibility. Understanding virtualization is essential for modern server administration.

### Cloud Integration

The distinction between on-premises and cloud is blurring. Modern infrastructures are hybrid—some workloads on-premises, others in cloud, with integration between them. Understanding cloud models (IaaS, PaaS, SaaS) and when to use each is crucial for infrastructure decisions.

### Storage Evolution

Storage has evolved from simple disks to sophisticated software-defined systems. Storage Spaces, RAID, and cloud storage each have appropriate use cases. Understanding these technologies enables informed decisions about data protection, performance, and cost.

---

## Quick Reference Tables

### Server Roles vs Features

| Aspect | Server Role | Server Feature |
|--------|-------------|----------------|
| Purpose | Major service function | Enhances/supports roles |
| Examples | AD DS, DNS, DHCP, IIS | .NET Framework, BitLocker |
| Installation | Via "Add Roles and Features Wizard" | Same wizard |

### Workgroup vs Domain

| Aspect | Workgroup | Domain |
|--------|-----------|--------|
| Management | Decentralized | Centralized (AD DS) |
| User accounts | Local to each computer | Centralized in AD |
| Best for | ≤10 computers | 10+ computers |
| Authentication | Local | Centralized |
| Policies | Local only | Group Policy |

### RAID Levels

| RAID | Disks | Fault Tolerance | Efficiency | Use Case |
|------|-------|-----------------|------------|----------|
| **0** | 2+ | None | 100% | Speed, non-critical data |
| **1** | 2 | Yes (1 disk) | 50% | Critical data, high availability |
| **5** | 3+ | Yes (1 disk) | 67-90% | File servers, general storage |
| **10** | 4+ | Yes (varies) | 50% | High-performance databases |

### Cloud Service Models

| Model | Control | Examples | Use Case |
|-------|---------|----------|----------|
| **SaaS** | Least | Office 365, Gmail | Ready-to-use applications |
| **PaaS** | Medium | Azure App Service | Application development |
| **IaaS** | Most | Azure VMs | Full infrastructure control |

### PowerShell Verbs

| Verb | Purpose | Example |
|------|---------|---------|
| **Get** | Retrieve information | Get-Disk, Get-Service |
| **Set** | Change properties | Set-Location, Set-Service |
| **New** | Create items | New-Item, New-VM |
| **Remove** | Delete items | Remove-Item |
| **Start/Stop** | Control services | Start-Service, Stop-VM |
| **Install** | Install features | Install-WindowsFeature |

### Key PowerShell Commands

```powershell
# Get system information
Get-ComputerInfo

# Install Windows Feature
Install-WindowsFeature -Name FeatureName -IncludeManagementTools

# Get disk information
Get-Disk
Get-Volume

# Service management
Get-Service
Start-Service -Name ServiceName
Stop-Service -Name ServiceName

# VM management (Hyper-V)
Get-VM
Start-VM -Name VMName
Stop-VM -Name VMName
```

---

**This module provides the conceptual foundation for Windows Server administration. Later modules dive deeper into specific technologies, but all build on these fundamentals. Understanding WHY things work the way they do helps you make good decisions in your own infrastructure.**

**Continue to practice questions to test your understanding!**
