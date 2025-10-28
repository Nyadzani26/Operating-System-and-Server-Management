# AZ-800 MODULE 1: ANSWER KEY
## Windows Server 2022 - Roles, Features, and Hybrid Infrastructure

---

## SECTION A: MULTIPLE CHOICE ANSWERS [30 Marks]

### Question 1
**Answer: b) False**

**Explanation:** While Windows Server 2022 is designed as a server OS, what matters most is how it is used and the software installed on it. A user could install Windows Server 2022 and use it as a general-purpose client computer by installing office productivity software, games, and other user- or client-oriented software. The OS itself doesn't dictate the role; the configuration and usage do.

---

### Question 2
**Answer: d) File and Printer Sharing for Microsoft Networks**

**Explanation:** Only "File and Printer Sharing for Microsoft Networks" is considered network server software. Let's analyze each option:
- **a) Client for Microsoft Networks** - This is CLIENT software (sends requests)
- **b) TCP/IP** - This is a network PROTOCOL (communication rules), not server software
- **c) Network interface driver** - This is a software component that communicates with the NIC hardware
- **d) File and Printer Sharing** - This is SERVER software (receives requests and provides resources) ✓

---

### Question 3
**Answer: a) RDP**

**Explanation:** Remote Desktop Protocol (RDP) is enabled by default on a new Azure VM that runs Windows Server 2022, and it can be accessed via a public IP address. However, Microsoft recommends disabling it after initial configuration for security reasons. Other protocols:
- **SSH** - Used for Linux VMs, not Windows by default
- **HTTP** - Web protocol, not for VM console access
- **VNC** - Third-party remote access, not default

---

### Question 4
**Answer: b) A major function or service that a server performs**

**Explanation:** A server role represents a major function or service that the server provides to the network. Examples include:
- File Server (provides file sharing)
- DNS Server (provides name resolution)
- Web Server/IIS (provides web hosting)
- Active Directory Domain Services (provides authentication)

Roles are significant, comprehensive services, not minor enhancements (those are features).

---

### Question 5
**Answer: c) Server Manager**

**Explanation:** Server Manager is the centralized tool in Windows Server 2022 for:
- Installing server roles and features
- Configuring installed roles
- Removing roles and features
- Managing multiple servers
- Monitoring server health
- Accessing administrative tools

While PowerShell can also manage roles (Install-WindowsFeature), Server Manager provides the GUI interface specifically designed for this purpose.

---

### Question 6
**Answer: c) NTFS**

**Explanation:** NTFS (New Technology File System) was introduced in Windows NT in the early 1990s. Key features:
- File and folder level permissions
- Security access control lists (ACLs)
- Encryption support
- Compression
- Large file and volume support

Other file systems:
- **FAT32** - Older, no permissions support
- **exFAT** - For removable media, no permissions
- **ReFS** - Newer, but NTFS is still standard

---

### Question 7
**Answer: b) Snap-ins**

**Explanation:** MMC (Microsoft Management Console) uses snap-ins, which are administrative tools designed to perform specific tasks such as:
- Disk Management
- Event Viewer
- Services
- Device Manager
- Group Policy Management

Snap-ins can be added to create custom management consoles. The term "snap-in" refers to how they "snap into" the MMC framework.

---

### Question 8
**Answer: c) Install device drivers**

**Explanation:** Disk Management is used for storage-related tasks:
- ✓ Initialize new disks
- ✓ Configure RAID volumes
- ✓ Create and format volumes
- ✓ Monitor disk status
- ✓ Troubleshoot disk problems

Installing device drivers is done through:
- Device Manager
- Windows Update
- Manual installation from manufacturer

---

### Question 9
**Answer: b) Workgroup**

**Explanation:** A workgroup is:
- Small collection of computers (typically < 10)
- Peer-to-peer network model
- Decentralized management
- Each computer maintains own user accounts
- Simple, suitable for home/small office

Other options:
- **Domain** - Centralized management, larger scale
- **Forest** - Collection of Active Directory domains
- **Site** - Physical network location in AD

---

### Question 10
**Answer: c) Standalone server**

**Explanation:** A Windows Server that participates in a workgroup (not a domain) is called a standalone server because:
- It stands alone, not part of domain
- Manages its own security database
- Not centrally managed
- Doesn't have AD DS installed

Other terms:
- **Domain controller** - Server with AD DS in domain
- **Member server** - Server in domain without AD DS
- **Peer server** - Not a standard Windows term

---

### Question 11
**Answer: b) Handle authentication and authorization**

**Explanation:** The main purpose of AD DS is to:
- **Authentication:** Verify user/computer identity (who you are)
- **Authorization:** Determine access permissions (what you can do)

Additional functions include:
- Centralized user/computer management
- Group Policy deployment
- Software distribution
- Organizational structure (OUs)

---

### Question 12
**Answer: b) Verb-Noun**

**Explanation:** PowerShell cmdlets follow the Verb-Noun naming convention:
- **Verb** - Action to perform (Get, Set, New, Remove, Start, Stop, etc.)
- **Noun** - Object to act upon (Disk, Service, Process, VM, etc.)

Examples:
- `Get-Service`
- `New-VM`
- `Set-Disk`
- `Remove-Item`

This makes cmdlets intuitive and self-documenting.

---

### Question 13
**Answer: b) Get-Disk -Number 1**

**Explanation:** The correct syntax is:
```powershell
Get-Disk -Number 1
```

PowerShell cmdlet syntax:
- Cmdlet name (Get-Disk)
- Parameter name preceded by dash (-Number)
- Parameter value (1)

Option a) `Get-Disk 1` might work due to positional parameters, but -Number is explicit and correct.

---

### Question 14
**Answer: c) |**

**Explanation:** The pipe character `|` passes output from one cmdlet to another:

```powershell
Get-Service | Where-Object {$_.Status -eq "Running"}
```

This gets all services, then filters for running ones.

Other characters:
- **>** - Redirect output to file
- **<** - Input redirection
- **&** - Run command in background

---

### Question 15
**Answer: b) A collection of technologies for abstracting how computing resources are delivered**

**Explanation:** Cloud computing abstracts:
- How applications are delivered
- How storage is provided
- How networks are configured
- How computing resources are accessed

It's not just about:
- Storing files (too narrow)
- Only VMs (includes many services)
- Internet connectivity (that's just the medium)

Cloud computing provides on-demand, scalable, abstracted resources.

---

## SECTION B: TRUE/FALSE ANSWERS [15 Marks]

### Question 16: **FALSE**
A server can be configured for **multiple roles** simultaneously. For example:
- File Server + Print Server
- DNS Server + DHCP Server
- Web Server + Database Server

Single-role servers are recommended for large enterprises, but multiple roles are common in small/medium businesses.

---

### Question 17: **TRUE**
Server features can add standalone functionality without requiring a specific role. Examples:
- **.NET Framework** - Standalone development framework
- **BitLocker** - Disk encryption feature
- **Telnet Client** - Network tool
- **Windows PowerShell** - Scripting environment

Features enhance the server but don't necessarily depend on a specific role.

---

### Question 18: **FALSE**
Server Manager **CAN manage remote servers**. This is one of its key capabilities:
- Add remote servers to Server Manager
- Manage all servers from single console
- Install roles/features remotely
- Monitor health of multiple servers
- Centralized management across network

---

### Question 19: **TRUE**
NTFS allows permissions on **both files and folders** individually:
- Set permissions on specific files
- Different permissions for different users
- Read, Write, Modify, Full Control at file level
- Inheritance can be customized

This is a major advantage over older file systems like FAT32.

---

### Question 20: **TRUE**
MMC snap-ins support **remote server management**:
- Connect to remote computers
- Manage services remotely
- Configure disks on other servers
- View event logs from other systems
- No need to sign in at server console

---

### Question 21: **TRUE**
File and Storage Services role includes Storage Spaces functionality:
- Create storage pools from multiple disks
- Configure virtual disks
- Set up thin provisioning
- Manage storage tiers
- Monitor storage health

---

### Question 22: **FALSE**
Shadow copies, disk quotas, and DFS are **ADVANCED** features, not basic:
- **Shadow Copies** - Previous versions/snapshots
- **Disk Quotas** - Limit user storage
- **DFS** - Distributed File System (organize shares across servers)

Basic features include simple file sharing and printer sharing.

---

### Question 23: **FALSE**
In a Windows domain, user accounts are stored in a **centralized database** (Active Directory):
- Single user account database on domain controllers
- Users sign in once, access all domain resources (SSO)
- Centralized password policies
- Consistent user management

Workgroups have separate user accounts on each computer.

---

### Question 24: **TRUE**
A domain controller is defined as:
- Windows Server with **AD DS role installed**
- Stores Active Directory database
- Handles authentication requests
- Replicates with other domain controllers
- Manages domain security

---

### Question 25: **TRUE**
The two main protocols administrators work with are:
- **TCP/IPv4** - Current standard (32-bit addresses like 192.168.1.1)
- **TCP/IPv6** - Next generation (128-bit addresses)

Other protocols (IPX/SPX, NetBEUI) are legacy and rarely used.

---

### Question 26: **TRUE**
PowerShell variables use the **$ symbol**:
```powershell
$computerName = "Server01"
$services = Get-Service
$count = 10
```

The $ indicates a variable, distinguishing it from cmdlets and strings.

---

### Question 27: **FALSE**
A VM is **NOT aware** it's running in a virtual environment:
- Guest OS thinks it's on physical hardware
- Sees virtual CPU, RAM, disk, network as real
- Complete abstraction from physical layer
- No modification needed to guest OS

This is a key benefit of virtualization.

---

### Question 28: **TRUE**
The hypervisor is the core virtualization component that:
- Creates virtual hardware environment
- Monitors VM resource usage
- Allocates physical resources to VMs
- Manages VM lifecycle
- Provides isolation between VMs

Examples: Hyper-V, VMware ESXi, VirtualBox

---

### Question 29: **FALSE**
Thin provisioning means disk space is **NOT allocated immediately**:
- Space allocated **only when actually needed**
- Volume may show 1TB size but use only 100GB physically
- Efficient use of storage
- Can oversubscribe physical storage

Traditional provisioning allocates all space upfront.

---

### Question 30: **TRUE**
Microsoft recommends **disabling RDP** after initial setup:
- RDP exposed to internet is security risk
- Brute force attacks common
- Use Azure Bastion or VPN instead
- Or restrict RDP to specific IP addresses
- Or use Just-In-Time VM access

---

## SECTION C: FILL IN THE BLANKS ANSWERS [15 Marks]

### Question 31
**Answer: Role services**

Role services add functions to the main server role, extending or customizing capabilities.

---

### Question 32
**Answer: Dashboard**

The Dashboard view shows tasks, installed roles, and servers to manage in a summary format.

---

### Question 33
**Answer: Permissions** (or **Access Control**)

NTFS permissions allow granular control over who can access files and folders.

---

### Question 34
**Answer: File and Storage Services** (or **File and Storage Services role**)

These are the two main disk management tools in Windows Server 2022.

---

### Question 35
**Answer: Client for Microsoft Networks**

This is the built-in Windows network client software.

---

### Question 36
**Answer: domain** (or **Windows domain**)

A domain provides centralized management and security.

---

### Question 37
**Answer: centralized**

Active Directory uses a centralized database stored on domain controllers.

---

### Question 38
**Answer: Get-Help** (or **Get-Help cmdletname**)

Example: `Get-Help Get-Disk`

---

### Question 39
**Answer: virtual machine** (or **VM**)

A VM emulates physical hardware in software.

---

### Question 40
**Answer: host** (or **host computer**)

The host runs the hypervisor and provides physical resources.

---

### Question 41
**Answer: Hyper-V**

Hyper-V is Microsoft's virtualization platform for Windows Server.

---

### Question 42
**Answer: public**

Public cloud services are provided by third-party vendors like Microsoft, Amazon, Google.

---

### Question 43
**Answer: VDI** (or **Virtual Desktop Infrastructure**)

VDI allows users to access virtual desktops from anywhere.

---

### Question 44
**Answer: thin provisioning**

Thin provisioning allocates space on-demand, not upfront.

---

### Question 45
**Answer: Hybrid**

Windows Server Hybrid Infrastructure combines on-premises and cloud.

---

## SECTION D: MATCHING ANSWERS [10 Marks]

### Question 46-55

**Correct Matches:**

- **A. SaaS** → **8.** Customer pays for use of applications on provider's network
- **B. PaaS** → **9.** Customer develops applications with provider's tools
- **C. IaaS** → **10.** Companies use provider's computing power, storage, and infrastructure
- **D. Guest OS** → **6.** Operating system running in a virtual machine
- **E. Hypervisor** → **7.** Virtualization software component that creates virtual hardware
- **F. Workgroup** → **1.** Small collection of computers in peer-to-peer network
- **G. Domain Controller** → **2.** Server with Active Directory Domain Services role installed
- **H. Snap-in** → **5.** MMC tool designed for specific administrative tasks
- **I. NTFS** → **4.** File system that supports file and folder permissions
- **J. Cmdlet** → **3.** PowerShell command with Verb-Noun structure

---

## SECTION E: SHORT ANSWER ANSWERS [30 Marks]

### Question 56
**THREE capabilities of Disk Management:**

1. **Initialize new disks** - Prepare new disks for use by creating partition tables
2. **Create and format volumes** - Create partitions and format them with file systems (NTFS, ReFS)
3. **Configure RAID volumes** - Set up redundant storage (mirrored, striped, RAID-5)

**Other acceptable answers:**
- Monitor disk and volume status
- Troubleshoot disk problems
- Extend or shrink volumes
- Change drive letters
- Convert between disk types (basic/dynamic)

---

### Question 57
**Workgroup vs Domain:**

**Workgroup:**
- Small collection of computers (peer-to-peer network)
- Decentralized management
- Each computer maintains its own user account database
- Suitable for home or small office (< 10 computers)
- Server in workgroup = standalone server
- Simple to set up but harder to manage at scale

**Domain:**
- Group of computers with centralized management
- Rules and policies defined by administrator
- Centralized user account database (Active Directory)
- Suitable for medium to large organizations
- Server with AD DS = domain controller
- More complex but easier to manage at scale
- Single sign-on (SSO) for users

---

### Question 58
**THREE cloud service categories:**

**1. Software as a Service (SaaS):**
- Customer pays for use of applications
- Applications run on service provider's infrastructure
- Examples: Microsoft 365, Gmail, Salesforce
- No installation or maintenance required
- Access via web browser

**2. Platform as a Service (PaaS):**
- Customer develops applications using provider's tools and infrastructure
- Provider manages underlying infrastructure
- Examples: Azure App Service, Google App Engine
- Focus on development, not infrastructure management

**3. Infrastructure as a Service (IaaS):**
- Companies use provider's computing power, storage, and network infrastructure
- Customer controls operating systems and applications
- Provider manages physical hardware
- Examples: Azure Virtual Machines, Amazon EC2
- **Primary focus of Microsoft Azure**
- Most flexibility and control

---

### Question 59
**Server role definition and examples:**

**Server Role:**
A major function or service that a server performs for network clients.

**THREE Examples:**

1. **Active Directory Domain Services (AD DS):**
   - Provides authentication and authorization
   - Manages user and computer accounts
   - Implements security policies

2. **DNS Server:**
   - Resolves domain names to IP addresses
   - Essential for network name resolution
   - Required for Active Directory

3. **File Server:**
   - Provides centralized file storage
   - Manages shared folders and permissions
   - Supports shadow copies and quotas

**Other acceptable examples:**
- DHCP Server (assigns IP addresses)
- Web Server/IIS (hosts websites and web applications)
- Print Server (manages network printers)

---

### Question 60
**AD DS purpose and tasks:**

**Purpose:**
Active Directory Domain Services handles authentication (verifying identity) and authorization (determining access rights) for users and computers in a Windows domain environment.

**THREE tasks it helps achieve:**

1. **Deploying user and computer policies** - Use Group Policy to configure settings across the domain

2. **Installing software** - Centrally deploy applications to domain computers

3. **Applying patches and updates** - Push security updates and patches to all domain systems

**Other acceptable tasks:**
- Centralized user account management
- Single sign-on (SSO) for network resources
- Organizational structure with OUs
- Security group management
- Resource access control

---

### Question 61
**PowerShell cmdlet structure:**

**Structure:**
```
Verb-Noun -ParameterName ParameterValue
```

**Components:**
- **Verb:** Action to perform (Get, Set, New, Remove, Start, Stop, etc.)
- **Noun:** Object being acted upon (Disk, Service, VM, User, etc.)
- **Parameter:** Modifies the command (optional, preceded by dash)
- **Value:** Input for the parameter

**Example:**
```powershell
Get-Disk -Number 1
```
- **Verb:** Get (retrieve information)
- **Noun:** Disk (storage disk object)
- **Parameter:** -Number (specifies which disk)
- **Value:** 1 (disk number 1)

---

### Question 62
**Virtual Machine vs Host Computer:**

**Virtual Machine (VM):**
- Virtual environment that emulates a physical computer
- Has virtual hardware (CPU, RAM, disk, network)
- Runs a guest operating system
- Isolated from other VMs
- Multiple VMs can run on one host

**Host Computer:**
- Physical computer with actual hardware
- Runs virtualization software (hypervisor)
- Provides physical resources to VMs
- One host can support multiple VMs
- Runs the host operating system (or bare-metal hypervisor)

**Key Difference:**
The host is the physical machine providing resources; VMs are virtual machines running on that host.

---

### Question 63
**THREE attributes of cloud computing (hybrid infrastructure):**

1. **Scalable:**
   - Add or remove resources as needed
   - No large upfront hardware investment
   - Handle traffic spikes efficiently
   - Pay for what you use

2. **Agile:**
   - Quick deployment of new resources
   - Rapid response to business needs
   - Fast disaster recovery
   - Flexibility in testing and development

3. **Current:**
   - Always updated infrastructure
   - Latest security patches applied automatically
   - New features available immediately
   - Reduced maintenance burden

---

## SECTION F: SCENARIO-BASED ANSWERS [20 Marks]

### Question 64
**Workgroup or Domain - Recommendation:**

**Recommendation: Workgroup** (for 25 employees)

**Justification:**
- **Small size:** 25 employees is manageable with workgroup
- **Cost-effective:** No need for dedicated domain controller hardware
- **Simplicity:** Easier to set up and maintain for small business
- **Lower complexity:** No AD DS expertise required
- **Sufficient security:** File-level permissions with NTFS

**However, Domain would be better if:**
- Company expects significant growth
- Centralized management desired
- Advanced security policies needed
- Budget allows for domain controller

**Alternative Answer: Domain** (also acceptable with proper justification)
- Better for centralized management
- Single sign-on for users
- Centralized backup and policies
- Scalability for future growth
- Professional business environment

---

### Question 65
**Server roles to install:**

1. **File Services** (or File Server role)
2. **Print and Document Services** (or Print Server role)

These roles provide the core functionality needed for file and printer sharing.

---

### Question 66
**File system choice:**

**File System: NTFS**

**Reasons:**
- **Permissions:** Supports file and folder level permissions for security
- **Quotas:** Can limit storage per user
- **Reliability:** Journaling file system, better recovery from errors
- **Features:** Supports encryption, compression, shadow copies
- **Standard:** Default and recommended for Windows Server
- **Security:** Essential for business environment with 25 users

---

### Question 67
**Type of infrastructure:**

**Answer: Hybrid Infrastructure** (or Hybrid Cloud)

This creates a Windows Server Hybrid Infrastructure - the marriage of on-premises Windows Server and Microsoft Azure cloud services.

---

### Question 68
**TWO advantages of hybrid approach:**

1. **Flexibility and Scalability:**
   - Keep sensitive data on-premises for compliance/security
   - Use cloud for scalable resources (handle traffic spikes)
   - Best of both worlds approach
   - Gradually migrate workloads at own pace

2. **Cost Optimization:**
   - No need to replace all on-premises infrastructure immediately
   - Pay for cloud resources only when needed
   - Leverage existing on-premises investment
   - Reduce capital expenditure for new hardware

**Other acceptable advantages:**
- Disaster recovery (cloud backup for on-premises)
- Business continuity (redundancy across locations)
- Agility (quick deployment of new services in cloud)
- Current technology (always updated cloud services)

---

### Question 69
**Azure VM default protocol and security:**

**Default Protocol: RDP (Remote Desktop Protocol)**

**Security Recommendation:**
Disable RDP after initial configuration, or restrict access:
- Disable public RDP access
- Use Azure Bastion for secure browser-based access
- Implement Just-In-Time (JIT) VM access
- Restrict RDP to specific IP addresses via Network Security Groups
- Use VPN for remote access instead

**Reason:** RDP exposed to the internet is a common attack vector for brute force attacks.

---

### Question 70
**PowerShell command:**

```powershell
Get-Command *VM*
```

This lists all cmdlets with "VM" anywhere in the name (Get-VM, New-VM, Start-VM, etc.).

**Alternative:**
```powershell
Get-Command *VM* -Module Hyper-V
```
(More specific, shows only Hyper-V VM cmdlets)

---

### Question 71
**PowerShell help command:**

```powershell
Get-Help Get-VM -Examples
```

**Alternative commands:**
```powershell
Get-Help Get-VM -Detailed
Get-Help Get-VM -Full
Get-Help Get-VM -ShowWindow
```

---

### Question 72
**Pipe character explanation:**

**What it does:**
The pipe character `|` takes the output of one cmdlet and passes it as input to another cmdlet.

**Example:**
```powershell
Get-Service | Where-Object {$_.Status -eq "Running"}
```

**Explanation:**
- `Get-Service` retrieves all services
- `|` pipes the output (all services)
- `Where-Object` filters for only running services
- Result: List of only running services

**Another example:**
```powershell
Get-VM | Start-VM
```
Gets all VMs and starts them.

---

## SECTION G: ADVANCED ANSWERS [10 Marks]

### Question 73
**Thin provisioning vs traditional allocation:**

**Traditional Disk Allocation:**
- Physical disk space allocated immediately when volume created
- If you create 1TB volume, 1TB is reserved immediately
- Space unavailable for other uses even if not used
- Inefficient use of storage resources

**Thin Provisioning (Storage Spaces):**
- Physical disk space allocated only when actually needed
- Create 1TB volume but only use physical space for actual data
- If volume contains 100GB data, only 100GB physical space used
- Can oversubscribe (create more virtual capacity than physical)

**Advantage:**
- **Efficient resource utilization:** Don't waste space on empty volumes
- **Cost savings:** Buy storage only when needed
- **Flexibility:** Provision large volumes without immediate physical capacity
- **Simplified management:** Add physical storage as virtual volumes grow

**Example:**
Create 10 volumes of 1TB each (10TB total virtual) on 2TB physical storage. As volumes fill, add more physical disks to the pool.

---

### Question 74
**Client for Microsoft Networks vs File and Printer Sharing:**

**Client for Microsoft Networks:**
- **Type:** Network client software
- **Function:** Sends requests to servers for shared resources
- **Role:** Requestor/consumer of resources
- **Example:** User accessing shared folder on server
- **Direction:** Client → Server (requests)
- **Installed on:** All Windows computers (clients and servers)

**File and Printer Sharing for Microsoft Networks:**
- **Type:** Network server software
- **Function:** Receives requests and provides shared resources
- **Role:** Provider of resources
- **Example:** Server hosting shared folders for users
- **Direction:** Server → Client (responses, providing resources)
- **Installed on:** Computers sharing resources

**Key Difference:**
- **Client software** = Makes requests (consumer)
- **Server software** = Fulfills requests (provider)

**Note:** Both can be installed on the same computer, allowing it to both share resources (server) and access other shares (client).

---

### Question 75
**Server Manager for multiple servers:**

**How it works:**
Server Manager can manage multiple servers by:
- Adding remote servers to the server pool
- Connecting to remote servers via WinRM (Windows Remote Management)
- Displaying aggregated information from all managed servers
- Allowing role/feature installation on remote servers
- Providing centralized monitoring and management

**Benefits:**

1. **Centralized Management:**
   - Manage all servers from single console
   - No need to RDP into each server
   - Consistent interface across servers
   - Single pane of glass for entire infrastructure

2. **Efficiency:**
   - Save time switching between servers
   - Deploy roles/features to multiple servers simultaneously
   - Bulk operations possible
   - Reduced administrative overhead

3. **Improved Monitoring:**
   - View health of all servers at a glance
   - Consolidated alerts and events
   - Dashboard view of entire environment
   - Proactive problem detection

**Use Case:**
Administrator at workstation can install File Server role on 10 remote servers simultaneously without leaving their desk.

---

## BONUS QUESTION ANSWERS

### Bonus 1
**MMC stands for:** Microsoft Management Console

**Primary purpose:**
Create a centralized, consistent management interface for administrators using snap-ins (administrative tools).

---

### Bonus 2
**THREE advanced file sharing features:**

1. **Shadow Copies** - Previous versions of files for user recovery
2. **Disk Quotas** - Limit storage space per user
3. **Distributed File System (DFS)** - Organize shared folders across multiple servers

---

### Bonus 3
**Virtual Desktop Infrastructure (VDI):**

VDI is a technology where users access virtual desktops hosted in a private cloud instead of local desktops.

**How users access:**
- Web browser
- Client software (thin client or desktop)
- From any device with internet connection
- Credentials authenticate to access personal virtual desktop

---

### Bonus 4
**Public vs Private Cloud:**

**Public Cloud:**
- Provided by third-party vendor (Microsoft, Amazon, Google)
- Shared infrastructure (multi-tenant)
- Accessible via internet
- Examples: Azure, AWS, Google Cloud, OneDrive

**Private Cloud:**
- Provided by internal IT department
- Dedicated infrastructure (single organization)
- Greater control and security
- Examples: On-premises VDI, internal storage services

---

### Bonus 5
**PowerShell command:**

```powershell
Get-Command Get-*
```

This lists all cmdlets starting with "Get".

---

**STUDY TIP:** Review incorrect answers carefully. Understand WHY the correct answer is right, not just what it is. Focus on concepts, not memorization.

**Good luck with your studies! 🎓**
