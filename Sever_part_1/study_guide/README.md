# AZ-800 MODULE 1: STUDY GUIDE
## Windows Server 2022 - Roles, Features, and Hybrid Infrastructure

---

## TABLE OF CONTENTS
1. [Windows Server Roles and Features](#windows-server-roles-and-features)
2. [Core Technologies](#core-technologies)
3. [Windows Networking Concepts](#windows-networking-concepts)
4. [Virtualization and Cloud Computing](#virtualization-and-cloud-computing)
5. [Windows Server Hybrid Infrastructure](#windows-server-hybrid-infrastructure)
6. [Microsoft Azure](#microsoft-azure)
7. [Quick Reference](#quick-reference)

---

## WINDOWS SERVER ROLES AND FEATURES

### Key Concepts

**Server Role:**
- A major function or service that a server performs
- Examples: File Server, DNS Server, Web Server (IIS), Active Directory Domain Services
- Installed via Server Manager → Manage → Add Roles and Features

**Role Services:**
- Add functions to the main role
- Extend or customize the capabilities of a role
- Example: Web Server (IIS) role has role services like ASP.NET, FTP Server

**Server Features:**
- Provide functions that enhance or support an installed role
- Can add stand-alone functionality
- Examples: .NET Framework, BitLocker, Telnet Client

**Important Notes:**
- A server can be configured for a **single role** or **several roles**
- Not all servers must perform server functions - Windows Server 2022 can be used as a client workstation (though not recommended)
- Role installation is managed through **Server Manager**

---

## CORE TECHNOLOGIES

### 1. Server Manager

**Purpose:**
- Single interface for installing, configuring, and removing server roles and features
- Centralized management tool for multiple servers
- Diagnostics and troubleshooting capabilities

**Key Features:**
- **Dashboard view:** Shows installed roles, server status, and management tasks
- **Remote management:** Manage all servers in your network from one location
- **Role-based organization:** Group management tasks by role
- **Task-based management:** Quick access to common administrative tasks

**Access:** Automatically launches on server startup (can be disabled)

---

### 2. NTFS (New Technology File System)

**History:**
- Introduced in Windows NT (early 1990s)
- Replaced FAT (File Allocation Table) file system
- Standard file system for Windows Server environments

**Key Features:**
- **Permissions:** Set user and group permissions on both folders and files
- **Security:** Specify which users can access files and what they can do
- **Granular control:** Read, Write, Modify, Full Control permissions
- **Inheritance:** Permissions can be inherited from parent folders

**Benefits:**
- Increased security in server environments
- Access control at file level (not just folder level)
- Supports large volumes and files
- Journaling for reliability

---

### 3. Microsoft Management Console (MMC)

**Purpose:**
- Creates centralized management interface for administrators
- Provides consistent interface for different administrative tools

**Key Concepts:**
- **Snap-ins:** Tools designed to perform specific administrative tasks
  - Examples: Disk Management, Event Viewer, Services, Group Policy
- **Custom consoles:** Administrators can create custom MMCs with specific snap-ins
- **Remote management:** Connect to and manage remote servers
- **.msc files:** Saved console configurations

**Advantages:**
- Install management tools on Windows 11 workstation
- Manage Windows Server 2022 without signing in at server console
- Create role-based management consoles
- Consistent interface across different tools

---

### 4. Disk Management

**Tools Available:**
- **Disk Management snap-in** (traditional MMC tool)
- **File and Storage Services role** (newer, more advanced)

**Capabilities:**
- Monitor status of disks and volumes
- Initialize new disks
- Create and format new volumes
- Troubleshoot disk problems
- Configure RAID (Redundant Array of Independent Disks)
- Create storage pools for Storage Spaces

**Volume Types:**
- Simple volumes
- Spanned volumes
- Striped volumes (RAID 0)
- Mirrored volumes (RAID 1)
- RAID 5 volumes

---

### 5. File and Printer Sharing

**Basic Features:**
- Share folders and printers over network
- Set share permissions
- Manage shared resources

**Advanced Features:**
- **Shadow Copies:** Previous versions of files for recovery
- **Disk Quotas:** Limit storage space per user
- **Distributed File System (DFS):** Organize shared folders across multiple servers
- **Version control:** Track file changes
- **User storage restrictions:** Enforce storage limits

**Benefits:**
- Centralized file storage
- Simplified backup management
- Collaboration capabilities
- Resource sharing efficiency

---

### 6. Windows Networking

**Network Security Models:**

**1. Windows Workgroup:**
- Small collection of computers (typically < 10)
- Also called **peer-to-peer network**
- Decentralized management
- Each computer maintains its own user accounts
- Server in workgroup = **Standalone Server**

**2. Windows Domain:**
- Group of computers with centralized management
- Rules defined by administrator
- Centralized user authentication
- Server with AD DS role = **Domain Controller**

---

### 7. Windows Networking Components

**A. Network Connection:**
- Collection of networking components working together
- Configured in Network Connections window

**B. Network Interface:**
- **Hardware:** Network Interface Card (NIC)
- **Software:** Device driver
- Configured in Network Connections window

**C. Network Protocol:**
- Specifies rules and format of communication
- **TCP/IPv4:** Current standard (32-bit addresses)
- **TCP/IPv6:** Next generation (128-bit addresses)
- Configure via Properties button in network connection

**D. Network Client:**
- OS component that sends requests to server
- Windows: **Client for Microsoft Networks**
- Requests access to shared resources

**E. Network Server Software:**
- Receives requests for shared resources
- Makes resources available to clients
- Windows: **File and Printer Sharing for Microsoft Networks**

---

### 8. Active Directory Domain Services (AD DS)

**Purpose:**
- Turns Windows Server 2022 into a Domain Controller
- Handles authentication and authorization
- Centralized database for network objects

**Main Functions:**
- **Authentication:** Verify user/computer identity
- **Authorization:** Determine access permissions
- **Centralized management:** Single point of control

**Capabilities:**
- Deploy user and computer policies (Group Policy)
- Install software across domain
- Apply patches and updates to domain computers
- Organize users, computers, groups in hierarchical structure
- Single sign-on (SSO) for domain resources

**Benefits:**
- Reduced administrative overhead
- Consistent security policies
- Simplified user management
- Scalability for large networks

---

### 9. PowerShell

**Purpose:**
- Command-line interactive scripting environment
- Management and automation of Windows Server
- More powerful than traditional Command Prompt

**Cmdlet Structure:**
```powershell
Verb-Noun -Parameter Value
```

**Example:**
```powershell
Get-Disk -Number 1
```

**Components:**
- **Verb:** Action to perform (Get, Set, New, Remove, etc.)
- **Noun:** Object to act upon (Disk, User, Service, etc.)
- **Parameter:** Modifier for the command (-Number, -Name, -Path, etc.)
- **Value:** Input for the parameter

**Variables:**
```powershell
$variable = "value"
$disks = Get-Disk
```

**Useful Tips:**

1. **List all cmdlets starting with Get:**
```powershell
Get-Command Get-*
```

2. **Find cmdlets with specific word:**
```powershell
Get-Command *disk*
```

3. **Get help on a cmdlet:**
```powershell
Get-Help Get-Disk
Get-Help Get-Disk -Examples
Get-Help Get-Disk -Full
```

4. **Piping (pass output to another cmdlet):**
```powershell
Get-Service | Where-Object {$_.Status -eq "Running"}
```

---

### 10. Hyper-V and Virtualization

**Key Concepts:**

**Cloud Computing:**
- Collection of technologies abstracting resource delivery
- Provides on-demand access to computing resources
- Scalable and flexible infrastructure

**Virtualization:**
- Use software to emulate multiple hardware environments
- Multiple operating systems on same physical server
- Efficient resource utilization

**Virtual Machine (VM):**
- Virtual environment emulating physical computer
- Has virtual hardware (CPU, RAM, disk, network)
- Isolated from host and other VMs

**Guest Operating System:**
- OS running inside a VM
- Can be Windows, Linux, or other OS
- Unaware it's running in virtual environment

**Host Computer:**
- Physical computer running virtualization software
- Provides hardware resources to VMs
- Runs hypervisor software

**Virtualization Software:**
- Creates and manages VMs
- Allocates resources to VMs
- Examples: Hyper-V, VMware, VirtualBox

**Hypervisor:**
- Core component of virtualization software
- Creates and monitors virtual hardware
- Two types: Type 1 (bare-metal) and Type 2 (hosted)

**Hyper-V:**
- Microsoft's virtualization platform
- Server role in Windows Server 2022
- Creates and manages VMs
- Supports Windows and Linux guests

---

### 11. Cloud Computing Models

**Public Cloud:**
- Services provided by third-party vendor
- Accessible over internet
- Shared infrastructure
- Examples: DropBox, OneDrive, Google Apps, Microsoft Azure

**Private Cloud:**
- Services provided by internal IT department
- Dedicated to single organization
- Greater control and security
- Typical services: Virtual desktops, storage, applications

**Virtual Desktop Infrastructure (VDI):**
- Users connect to virtual desktops in private cloud
- Access via web browser or client software
- Desktop available from any internet connection
- Centralized management and security

**Hybrid Cloud:**
- Combination of public and private cloud
- On-premises infrastructure + cloud services
- Best of both worlds approach
- Focus of Windows Server Hybrid Infrastructure

---

### 12. Storage Spaces

**Purpose:**
- Virtual drive management tool
- Create volumes from storage pools
- Dynamic expansion and fault tolerance

**Key Features:**
- **Multiple drive types:** USB, SATA, SAS
- **Flexible configuration:** Internal or external drives
- **RAID without same-sized disks:** Unlike traditional RAID
- **Thin provisioning:** Allocate space only when needed
- **Fault tolerance:** Protect against drive failures
- **Dynamic expansion:** Add capacity without downtime

**Benefits:**
- Cost-effective redundancy
- Simplified storage management
- Efficient space utilization
- Scalability

---

## WINDOWS SERVER HYBRID INFRASTRUCTURE

### What is Hybrid Infrastructure?

**Definition:**
- Marriage of on-premises Windows Server and Microsoft Azure cloud
- Seamless integration between local and cloud resources
- Unified management experience

**Attributes:**

**1. Scalable:**
- Add or remove resources as needed
- No large upfront investment in hardware
- Pay for what you use
- Handle traffic spikes efficiently

**2. Agile:**
- Quick deployment of new resources
- Rapid response to business needs
- Test and development flexibility
- Fast disaster recovery

**3. Current:**
- Always updated infrastructure
- Latest security patches
- New features automatically available
- Reduced maintenance burden

---

### Cloud Service Models

**1. Software as a Service (SaaS):**
- Customer pays for application usage
- Applications run on provider's infrastructure
- Examples: Microsoft 365, Salesforce, Gmail
- No software installation or maintenance

**2. Platform as a Service (PaaS):**
- Customer develops applications using provider's tools
- Provider manages infrastructure
- Examples: Azure App Service, Google App Engine
- Focus on development, not infrastructure

**3. Infrastructure as a Service (IaaS):**
- **Primary focus of Microsoft Azure**
- Customer uses provider's computing resources
- Provider supplies: Computing power, storage, networking
- Customer controls: OS, applications, data
- Maximum flexibility and control

---

## MICROSOFT AZURE

### Getting Started

**Azure Account:**
- Required to access Azure services
- Can start with free tier
- Credit card needed for verification

**Azure Portal:**
- Web-based management interface
- Accessible from any browser
- Unified console for all Azure services

**Quickstart Center:**
- Create new services quickly
- Deploy VMs, web apps, databases
- Access common tasks

**Common Azure Services:**
- Azure Virtual Machines
- Azure Active Directory
- Azure DNS
- Azure File Services
- Azure Storage
- Azure Networking

---

### Creating an Azure Virtual Machine

**Deployment Steps:**

1. Go to Quickstart Center
2. Click "Deploy a virtual machine"
3. Configure VM settings:
   - **Basics:** Name, region, size, OS
   - **Disks:** OS disk, data disks
   - **Networking:** Virtual network, subnet, public IP
   - **Management:** Monitoring, backup, updates
   - **Advanced:** Extensions, cloud-init
4. Review and create
5. Wait for deployment (few minutes)

**Default Configuration:**
- **RDP enabled** (Remote Desktop Protocol)
- **Public IP address** assigned
- **Accessible from internet**
- **Security recommendation:** Disable RDP after initial setup

---

### Accessing Azure Virtual Machine

**Access Methods:**

**1. Remote Desktop Protocol (RDP):**
```
1. Click VM name in Azure Portal
2. Click "Connect"
3. Click "RDP"
4. Download RDP file
5. Open RDP file
6. Enter credentials
7. Access Windows Server desktop
```

**2. Azure Bastion:**
- Secure browser-based access
- No public IP needed
- Enhanced security

**3. SSH (for Linux VMs):**
- Command-line access
- Key-based authentication

**Capabilities:**
- Same functionality as physical/local VM
- Install roles and features
- Configure settings
- Run applications
- Manage resources

---

## QUICK REFERENCE

### Server Roles vs Features

| Aspect | Server Role | Server Feature |
|--------|-------------|----------------|
| Purpose | Major service function | Enhances/supports roles |
| Examples | AD DS, DNS, DHCP, IIS | .NET Framework, BitLocker |
| Standalone | Can be primary function | Usually supports other services |
| Complexity | More complex | Simpler, focused |

### Workgroup vs Domain

| Aspect | Workgroup | Domain |
|--------|-----------|--------|
| Size | Small (< 10 computers) | Scalable (thousands) |
| Management | Decentralized | Centralized |
| User accounts | Local to each computer | Centralized in AD |
| Security | Basic | Advanced (GPO, policies) |
| Server type | Standalone server | Domain controller |

### Cloud Service Models

| Model | Control | Examples | Use Case |
|-------|---------|----------|----------|
| **SaaS** | Least | Office 365, Gmail | Ready-to-use applications |
| **PaaS** | Medium | Azure App Service | Application development |
| **IaaS** | Most | Azure VMs, Storage | Full infrastructure control |

### PowerShell Common Verbs

| Verb | Purpose | Example |
|------|---------|---------|
| Get | Retrieve information | Get-Disk, Get-Service |
| Set | Modify settings | Set-Service, Set-Disk |
| New | Create object | New-VM, New-ADUser |
| Remove | Delete object | Remove-Item, Remove-VM |
| Start | Start service/process | Start-Service, Start-VM |
| Stop | Stop service/process | Stop-Service, Stop-VM |
| Enable | Enable feature | Enable-WindowsFeature |
| Disable | Disable feature | Disable-WindowsFeature |

### Networking Components

| Component | Windows Name | Purpose |
|-----------|--------------|---------|
| Network Client | Client for Microsoft Networks | Request shared resources |
| Network Server | File and Printer Sharing for Microsoft Networks | Provide shared resources |
| Protocol | TCP/IPv4, TCP/IPv6 | Communication rules |
| Interface | NIC + Driver | Physical/logical connection |

---

## KEY TERMS TO MEMORIZE

- **Server Role:** Major function or service (e.g., DNS, DHCP, AD DS)
- **Role Service:** Adds functionality to main role
- **Server Feature:** Enhances roles or adds standalone function
- **Standalone Server:** Server in workgroup (not domain)
- **Domain Controller:** Server with AD DS role installed
- **MMC:** Microsoft Management Console (centralized admin interface)
- **Snap-in:** Administrative tool within MMC
- **NTFS:** New Technology File System (supports permissions)
- **Cmdlet:** PowerShell command (Verb-Noun structure)
- **Hypervisor:** Software creating virtual hardware environment
- **VM:** Virtual Machine (emulated computer)
- **Guest OS:** Operating system running in VM
- **Host Computer:** Physical computer running VMs
- **Public Cloud:** Third-party cloud services (Azure, AWS)
- **Private Cloud:** Internal IT department cloud services
- **Hybrid Cloud:** On-premises + public cloud
- **SaaS:** Software as a Service (applications)
- **PaaS:** Platform as a Service (development platform)
- **IaaS:** Infrastructure as a Service (Azure VMs, storage)
- **VDI:** Virtual Desktop Infrastructure (virtual desktops)
- **Storage Spaces:** Virtual drive management with thin provisioning
- **Thin Provisioning:** Allocate disk space only when needed
- **RDP:** Remote Desktop Protocol (remote access to Windows)

---

## EXAM TIPS

### High-Priority Topics

1. **Difference between roles and features**
2. **Server Manager functions**
3. **Workgroup vs Domain**
4. **Network components** (client, server software, protocol)
5. **PowerShell cmdlet structure**
6. **Cloud service models** (SaaS, PaaS, IaaS)
7. **Virtualization terminology** (VM, hypervisor, guest OS, host)
8. **Azure VM access** (RDP by default)
9. **AD DS purpose** (authentication and authorization)
10. **Storage Spaces features** (thin provisioning, dynamic expansion)

### Common Mistakes to Avoid

- ❌ Confusing roles with features
- ❌ Thinking Windows Server must always be a server (can be client)
- ❌ Confusing Client for Microsoft Networks (client) with File and Printer Sharing (server)
- ❌ Not knowing RDP is default on Azure VMs
- ❌ Mixing up cloud service models (SaaS, PaaS, IaaS)
- ❌ Forgetting NTFS supports file-level permissions (not just folders)

### Study Strategies

1. **Understand, don't memorize:** Focus on concepts, not rote learning
2. **Draw diagrams:** Visualize workgroup vs domain, network components
3. **Practice PowerShell:** Run cmdlets in practice environment
4. **Create comparison tables:** Roles vs features, workgroup vs domain
5. **Use acronyms:** Remember NTFS features, cloud models

---

**Good luck with your studies! 🎓**
