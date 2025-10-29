# NOSS631 - EXAMINATION MEMORANDUM
## Operating Systems & Server Management - Detailed Answer Key

**TOTAL MARKS:** 100

---

## SECTION A ANSWERS [45 MARKS]

### QUESTION 1: Matching and Processing (12 Marks)

**1.1 Segmentation vs Paging Comparison** [5]

| Aspect | Segmentation | Paging |
|--------|--------------|--------|
| **Division Method** | Logical units (code, data, stack, heap) | Fixed-size blocks (pages/frames) |
| **Size Characteristics** | Variable size (segments differ) | Fixed size (all pages same size) |
| **Fragmentation Type** | External fragmentation | Internal fragmentation (last page) |
| **Formula/Calculation** | Physical = Base + Offset (if Offset < Length) | Physical = (Frame# × PageSize) + Offset |
| **User Visibility** | Visible to programmer | Transparent to programmer |

**Explanation:**
- **Segmentation** divides memory based on logical program structure, making it visible to programmers who work with code segments, data segments, etc.
- **Paging** divides memory into uniform blocks, completely transparent to programmers.
- **Fragmentation difference:** Segmentation creates gaps between variable-sized segments (external), while paging wastes space only in the last page of each process (internal).

---

**1.2 Fragmentation Types** [4]

| Fragmentation Type | Definition | Where It Occurs | Example |
|-------------------|------------|-----------------|---------|
| **Internal Fragmentation** | Wasted space WITHIN an allocated memory block | Paging systems, fixed-size partitions | Process needs 18KB, allocated 20KB block → 2KB wasted inside the block |
| **External Fragmentation** | Wasted space BETWEEN allocated memory blocks | Segmentation, dynamic partitioning | Have 100KB free memory but scattered in 10KB chunks → Cannot allocate a single 50KB process |

**Explanation:**
- **Internal:** The waste is "internal" to the allocated block—memory is assigned but unused.
- **External:** The waste is "external"—free memory exists but is unusable due to fragmentation.
- **Key difference:** Internal = too much allocated; External = right amount available but in wrong configuration.

---

**1.3 Server Roles Matching** [3]

**Correct Answers:**
1. File Server → **D**
2. Print Server → **F**
3. Active Directory Domain Services → **A**
4. DHCP Server → **C**
5. DNS Server → **B**
6. Web Server (IIS) → **E**

**Explanation:**
- **AD DS (A):** Core authentication service providing domain controller functionality.
- **DNS (B):** Critical for AD; translates domain names to IP addresses.
- **DHCP (C):** Automates IP address assignment, reducing administrative overhead.
- **File Server (D):** Centralized storage using SMB/CIFS protocols.
- **IIS (E):** Microsoft's web server for hosting websites and web applications.
- **Print Server (F):** Centralizes print queue management and driver distribution.

---

### QUESTION 2: Fill in the Blanks (10 Marks)

**1.** A **server role** is a Windows Server role that provides major functionality, while a **server feature** is a supporting software component. [2]

**Explanation:** Roles are complete services (like AD DS, DNS), while features enhance roles (like .NET Framework, BitLocker). Think: Role = job, Feature = tools for the job.

**2.** The **NTFS** file system provides file-level security, compression, and encryption capabilities in Windows Server. [1]

**Explanation:** NTFS (New Technology File System) replaced FAT and provides enterprise features: permissions, compression, encryption (EFS), journaling, and large file support.

**3.** In Active Directory, the **domain** is the core structural unit containing OUs and objects. [1]

**Explanation:** The domain is the fundamental security and administrative boundary in AD. All user accounts, computers, and OUs exist within a domain.

**4.** The **RID Master** FSMO role is responsible for allocating RID pools to domain controllers. [1]

**Explanation:** RID (Relative Identifier) Master allocates blocks of RIDs to each DC. DCs use RIDs to create unique SIDs (Security Identifiers) for new security principals (users, groups, computers).

**5.** When a page fault occurs and all frames are occupied, the **OPT (Optimal)** algorithm replaces the page that won't be used for the longest time in the future. [1]

**Explanation:** OPT (Belady's algorithm) is theoretically optimal but impractical because it requires knowing future page references. Used as a benchmark to evaluate other algorithms.

**6.** The **fork()** system call creates a new child process in UNIX/Linux by duplicating the parent process. [1]

**Explanation:** fork() creates an exact copy of the calling process. Parent receives child's PID; child receives 0. Both continue execution after fork().

**7.** In memory management, **registers** is generally faster than cache, and cache is faster than **main memory (RAM)** or **secondary storage**. [2]

**Explanation:** Memory hierarchy by speed: Registers (fastest, most expensive) → Cache → RAM → Disk (slowest, cheapest). This hierarchy balances cost and performance.

**8.** A **Type 1** hypervisor runs directly on hardware, while a **Type 2** hypervisor runs on a host operating system. [1]

**Explanation:** Type 1 (bare metal): ESXi, Hyper-V—runs directly on hardware for maximum performance. Type 2 (hosted): VirtualBox, VMware Workstation—runs on existing OS for ease of use.

---

### QUESTION 3: Multiple Choice (5 Marks)

**1. Answer: b) Active Directory Administrative Center** [1]

**Explanation:** ADAC is built on PowerShell—every task you perform executes PowerShell cmdlets behind the scenes. You can even view the PowerShell code for operations. ADUC is the older MMC-based tool.

**2. Answer: b) RAID 1** [1]

**Explanation:** 
- **RAID 0:** Striping, no fault tolerance
- **RAID 1:** Mirroring (2 disks), survives 1 disk failure ✓
- **RAID 5:** Striping with parity (3+ disks), survives 1 disk failure
- **RAID 10:** Mirrored stripes (4+ disks), survives multiple failures

RAID 1 specifically uses mirroring (data duplicated on two disks).

**3. Answer: c) In Active Directory** [1]

**Explanation:** Domain user accounts are stored centrally in the Active Directory database on domain controllers. This enables single sign-on—users authenticate once and access all domain resources. Local accounts are stored in SAM (Security Account Manager) on individual computers.

**4. Answer: c) FIFO** [1]

**Explanation:** FIFO (First In First Out) suffers from Belady's Anomaly—counterintuitively, increasing the number of frames can increase page faults. This doesn't happen with stack-based algorithms like LRU.

**5. Answer: b) A context switch always occurs** [1]

**Explanation:** When a process makes a blocking system call (e.g., waiting for disk I/O), it cannot continue executing. The OS must switch to another process. This ALWAYS causes a context switch. Other events (like interrupts) may or may not cause context switches depending on circumstances.

---

### QUESTION 4: Operating Systems Calculations (5 Marks)

**Segment Table:**
| Segment | Base | Length |
|---------|------|--------|
| 0 | 300 | 400 |
| 1 | 1800 | 200 |
| 2 | 500 | 250 |

**Formula:** Physical Address = Base + Offset (valid only if Offset < Length)

**a) Logical Address (0, 250)** [1]
```
Segment 0: Base = 300, Length = 400
Check: 250 < 400? YES ✓
Physical Address = 300 + 250 = 450
```
**Answer: 450**

**b) Logical Address (1, 250)** [1]
```
Segment 1: Base = 1800, Length = 200
Check: 250 < 200? NO ✗
Result: INVALID - Segmentation Fault
```
**Answer: INVALID** (offset exceeds segment length)

**c) Logical Address (2, 100)** [1]
```
Segment 2: Base = 500, Length = 250
Check: 100 < 250? YES ✓
Physical Address = 500 + 100 = 600
```
**Answer: 600**

**d) Logical Address (0, 399)** [1]
```
Segment 0: Base = 300, Length = 400
Check: 399 < 400? YES ✓
Physical Address = 300 + 399 = 699
```
**Answer: 699**

**e) Logical Address (1, 50)** [1]
```
Segment 1: Base = 1800, Length = 200
Check: 50 < 200? YES ✓
Physical Address = 1800 + 50 = 1850
```
**Answer: 1850**

**Key Point:** The offset must be strictly less than the segment length. If offset ≥ length, it's invalid and causes a segmentation fault.

---

### QUESTION 5: Group Policy Activity (10 Marks)

**5.1 Password Policy Configuration** [3]

**Answer:** Configure in the **Default Domain Policy** linked to the domain object.

**Detailed Explanation:**

**Why Domain Level:**
1. **Technical Requirement:** Password policies (minimum length, complexity requirements, maximum age, account lockout) can ONLY be configured at the domain level in traditional Active Directory. OU-level password policies don't apply unless using Fine-Grained Password Policies (FGPP) in newer AD versions.

2. **Consistency:** All 500 employees need the same password requirements for security and compliance. Domain-level policy ensures uniform enforcement.

3. **Default Domain Policy:** This is the appropriate GPO for domain-wide account policies. It's automatically created and linked to the domain object during AD installation.

4. **Single Point of Management:** Centralized configuration eliminates the need to configure policies on each computer or OU separately.

**Implementation Steps:**
- Open Group Policy Management Console
- Navigate to Default Domain Policy
- Edit → Computer Configuration → Policies → Windows Settings → Security Settings → Account Policies → Password Policy
- Set: Minimum password length = 10, Password must meet complexity requirements = Enabled

---

**5.2 Group Policy Application Order (LSDOU)** [4]

**LSDOU Explanation:**

**LSDOU Stands For:**
- **L** = Local (computer's local Group Policy)
- **S** = Site (policies linked to Active Directory site)
- **D** = Domain (policies linked to domain)
- **O** = OU (policies linked to organizational units)

**Application Process:**
Policies are applied sequentially in this order: Local → Site → Domain → OU

**How It Affects Enforcement:**

1. **Last Applied Wins:** When policies conflict (both configure the same setting differently), the last policy applied takes precedence. Since OU policies apply last, they override domain policies.

2. **Accumulation:** Non-conflicting settings from all levels accumulate and apply together. Only conflicting settings follow the "last wins" rule.

3. **Not Configured:** Policies set to "Not Configured" don't change existing settings from earlier levels.

**Real-World Example for the Company:**

**Scenario:**
- **Domain Policy:** Desktop wallpaper = "company_logo.jpg"
- **Marketing OU Policy:** Desktop wallpaper = "marketing_team.jpg"
- **Finance OU:** No wallpaper policy configured

**Results:**
- Marketing Department users: Get "marketing_team.jpg" (OU overrides domain)
- Finance Department users: Get "company_logo.jpg" (domain policy applies)
- IT Department users: Get "company_logo.jpg" (domain policy applies)

**Why This Matters:**
- Allows baseline policies at domain level
- Enables customization for specific departments via OU policies
- Provides flexibility without losing central control

---

**5.3 IT Department USB Exception** [3]

**Implementation Strategy:**

**Method 1: OU-Level Override (Recommended)** [Best Practice]

1. **Create Domain/Parent-Level Block:**
   - Configure GPO at "Employees" OU level
   - Setting: Disable USB storage devices
   - Applies to Marketing, IT, and Finance OUs

2. **Create IT-Specific Allow Policy:**
   - Create new GPO: "IT USB Access"
   - Setting: Enable USB storage devices
   - Link to "IT Department" OU only

3. **Result:**
   - IT Department: USB allowed (OU policy overrides parent)
   - Marketing: USB blocked (parent OU policy applies)
   - Finance: USB blocked (parent OU policy applies)

**Why This Works:**
- Based on LSDOU principle
- IT Department OU policy applies last, overriding the Employees OU block
- Other departments don't have OU-level override, so block remains effective
- Clean, maintainable, follows AD design best practices

**Method 2: Security Filtering** [Alternative]

1. Apply USB block policy to "Employees" OU
2. Configure Security Filtering:
   - Remove "Authenticated Users"
   - Add specific groups: "Marketing Users", "Finance Users"
   - Exclude "IT Department Users" group
3. IT users aren't affected by the policy

**Verification Command:**
```powershell
gpresult /r /scope:user
# Shows which policies apply to current user
```

### QUESTION 6: LRU Calculation (6 Marks)

**Reference String:** 1, 2, 3, 4, 1, 2, 5, 1, 2, 3, 4, 5  
**Available Frames:** 3

**LRU (Least Recently Used) Algorithm Step-by-Step:**

```
Reference | Frame 1 | Frame 2 | Frame 3 | Fault? | Explanation
    1     |    1    |    -    |    -    |  Yes   | First reference, frame empty
    2     |    1    |    2    |    -    |  Yes   | Second reference, frame empty
    3     |    1    |    2    |    3    |  Yes   | Third reference, frame empty
    4     |    4    |    2    |    3    |  Yes   | Replace 1 (least recently used)
    1     |    4    |    2    |    1    |  Yes   | Replace 3 (least recently used)
    2     |    4    |    2    |    1    |  No    | HIT - page 2 already in memory
    5     |    5    |    2    |    1    |  Yes   | Replace 4 (least recently used)
    1     |    5    |    2    |    1    |  No    | HIT - page 1 already in memory
    2     |    5    |    2    |    1    |  No    | HIT - page 2 already in memory
    3     |    5    |    3    |    1    |  Yes   | Replace 2 (least recently used)
    4     |    5    |    3    |    4    |  Yes   | Replace 1 (least recently used)
    5     |    5    |    3    |    4    |  No    | HIT - page 5 already in memory
```

**Total Page Faults: 8**

**Detailed Explanation:**

**How LRU Works:**
- Tracks when each page was last accessed
- When a page fault occurs and all frames are full, replaces the page that hasn't been used for the longest time
- Based on temporal locality principle: recently used pages likely to be used again soon

**Key Steps in Solution:**
1. **References 1, 2, 3:** All cause page faults as frames initially empty (3 faults)
2. **Reference 4:** All frames full, replace page 1 (accessed earliest) → Fault
3. **Reference 1:** All frames full, replace page 3 (accessed earliest) → Fault
4. **Reference 2:** Already in memory → Hit (no fault)
5. **Reference 5:** Replace page 4 (least recently used) → Fault
6. **References 1, 2:** Both in memory → Hits
7. **Reference 3:** Replace page 2 (hasn't been accessed for longest) → Fault
8. **Reference 4:** Replace page 1 → Fault
9. **Reference 5:** Already in memory → Hit

**Marking Breakdown:**
- Correct frame tracking (showing which pages in memory): 2 marks
- Correct identification of page faults vs hits: 2 marks
- Correct final count (8 page faults): 2 marks

---

## SECTION B ANSWERS [38 MARKS]

### QUESTION 1: Standard Bank Infrastructure Scenario (33 Marks)

**Context:** Standard Bank, 15 branches, 200 employees, 50 ATMs, hybrid infrastructure needs, high security requirements.

---

**1.1a Why Domain Instead of Workgroup - Four Advantages** [4]

**1. Centralized User Management** [1]
- **Workgroup Challenge:** 200 users × 50+ computers = 10,000+ individual user accounts to manage
- **Domain Solution:** 200 user accounts stored centrally in Active Directory
- **Benefit:** Massive reduction in administrative overhead; add user once, they can access all resources

**2. Single Sign-On (SSO)** [1]
- **Workgroup Challenge:** Users need separate accounts on each computer; must remember multiple passwords
- **Domain Solution:** Users authenticate once with domain credentials, access all authorized resources
- **Benefit:** Improved productivity; better user experience; reduced password reset calls to IT

**3. Centralized Security Policies** [1]
- **Workgroup Challenge:** Must manually configure security on each of 50+ computers; inconsistent policies
- **Domain Solution:** Group Policy enforces consistent security policies automatically across all systems
- **Benefit:** Essential for banking regulatory compliance (PCI-DSS, financial regulations); ensures uniform security posture

**4. Scalability and Multi-Site Support** [1]
- **Workgroup Challenge:** Unmanageable beyond 10 computers; no multi-site support
- **Domain Solution:** Scales to thousands of users/computers; built-in replication across 15 branches
- **Benefit:** Supports Standard Bank's nationwide operations; allows for future growth

---

**1.1b OU Structure Design** [4]

**Recommended Structure:**
```
standardbank.local (Domain Root)
│
├── Domain Controllers (Default OU)
│   └── All domain controllers
│
├── Servers [Server Management]
│   ├── Database Servers (SQL Server, Oracle)
│   ├── Application Servers (Banking app servers)
│   ├── File Servers (Document storage)
│   └── Web Servers (Online banking front-end)
│
├── Branches [Geographic Organization]
│   │
│   ├── Johannesburg_Main [Main Branch]
│   │   ├── Employees
│   │   │   ├── Tellers
│   │   │   ├── Managers
│   │   │   └── Support_Staff
│   │   ├── Workstations
│   │   └── ATMs
│   │
│   ├── Cape_Town_DR [Disaster Recovery Site]
│   │   ├── Employees
│   │   ├── Workstations
│   │   └── Servers
│   │
│   └── Regional_Branches [13 Other Branches]
│       ├── Branch_Pretoria
│       ├── Branch_Durban
│       ├── Branch_Port_Elizabeth
│       └── ... (10 more branches)
│
├── Corporate [Head Office Functions]
│   │
│   ├── IT_Department
│   │   ├── Server_Administrators
│   │   ├── Network_Administrators
│   │   ├── Security_Team
│   │   └── Help_Desk
│   │
│   ├── Executive_Management
│   │   ├── C_Level (CEO, CTO, CFO)
│   │   └── Senior_Management
│   │
│   ├── Finance_Department
│   ├── HR_Department
│   └── Compliance_Team
│
└── Service_Accounts [Service & System Accounts]
    ├── SQL_Service_Accounts
    ├── Backup_Accounts
    └── Application_Service_Accounts
```

**Design Justification:** [Full marks requires explanation]

**1. Geographic Segregation:**
- Separate OUs for each branch enable location-specific policies
- Different branches may need different operating hours, local printers, regional compliance settings
- Site-based GPOs for network optimization

**2. Role-Based Organization:**
- Employees grouped by function (Tellers, Managers) for targeted Group Policies
- Tellers get restrictive policies (limited application access)
- Managers get moderate policies (access to management tools)
- Executives get flexible policies but enhanced security

**3. Security Segregation:**
- IT Department separate OU with elevated privileges
- Executives in protected OU with strict security policies
- Service accounts isolated to prevent accidental modification

**4. Device Type Separation:**
- Workstations, Servers, ATMs in different OUs
- Different security requirements (ATMs need kiosk mode, restricted access)
- Different update/maintenance schedules

**5. Scalability:**
- Structure easily accommodates new branches (just add new branch OU)
- Can delegate management (branch managers manage their branch OU)
- Clear hierarchy makes administration straightforward

---

**1.2a Three FSMO Roles and Importance** [3]

**1. PDC Emulator (Domain-wide Role)** [1]

**Purpose:**
- Acts as primary domain controller for several critical functions
- Handles password changes preferentially
- Source of time synchronization for domain
- Processes account lockouts immediately
- Provides backward compatibility with Windows NT

**Importance for Standard Bank:**
- **Transaction Timestamps:** Banking transactions require accurate, synchronized time. PDC Emulator ensures all servers use identical time, critical for audit trails and transaction ordering
- **Security:** Password changes process immediately through PDC Emulator, preventing authentication delays when employees change passwords
- **Account Lockout:** Fraud prevention requires immediate account lockouts. PDC Emulator processes lockouts instantly across all DCs
- **Compliance:** Financial regulations require precise time stamping; PDC Emulator provides authoritative time source

**2. RID Master (Domain-wide Role)** [1]

**Purpose:**
- Allocates pools of Relative Identifiers (RIDs) to each domain controller
- DCs use RIDs to create unique Security Identifiers (SIDs) for new security principals
- Prevents SID duplication across domain

**Importance for Standard Bank:**
- **User Account Creation:** As bank hires new employees (tellers, managers), RID Master ensures each user gets unique SID
- **ATM Addition:** New ATMs require computer accounts; RID Master allocates RIDs for these accounts
- **Group Creation:** Security and distribution groups need unique SIDs from RID Master
- **No Duplication:** Prevents security nightmare of duplicate SIDs which would cause access control failures

**3. Schema Master (Forest-wide Role)** [1]

**Purpose:**
- Only DC authorized to modify Active Directory schema
- Controls what object types and attributes can exist in AD
- Schema changes replicate to all DCs in forest

**Importance for Standard Bank:**
- **Application Integration:** When deploying new banking applications that extend AD schema, Schema Master processes these changes
- **Exchange/Email:** If deploying Exchange Server, schema extensions required; Schema Master manages this
- **Third-party Integration:** Identity management systems (like SSO providers) may require schema modifications
- **Controlled Changes:** Having single Schema Master prevents conflicts from simultaneous schema modifications

**Alternative Answers (also valid):**
- **Infrastructure Master:** Maintains cross-domain object references; important if multiple domains exist
- **Domain Naming Master:** Controls adding/removing domains; important for forest structure changes

---

**1.2b Domain Controller Deployment Recommendation** [3]

**Recommended Deployment Strategy:**

**Main Data Center (Johannesburg):** 3 Full Domain Controllers [1]

**Configuration:**
- **DC01:** Primary DC, holds all 5 FSMO roles, Global Catalog server
- **DC02:** Replication partner, standby for FSMO roles, Global Catalog server
- **DC03:** Additional replication partner, Global Catalog server, handles authentication load

**Justification:**
- **High Availability:** 3 DCs ensure service continues if 1-2 fail
- **Load Balancing:** Distributes authentication requests across multiple servers (200 users generate significant auth traffic)
- **FSMO Redundancy:** Can transfer FSMO roles to DC02 if DC01 fails
- **Performance:** Multiple Global Catalog servers speed up logons and directory searches

**DR Site (Cape Town):** 2 Full Domain Controllers [0.5]

**Configuration:**
- **CPTDC01 & CPTDC02:** Both Global Catalog servers, capable of holding FSMO roles

**Justification:**
- **Disaster Recovery:** If Johannesburg site lost (natural disaster, extended outage), Cape Town site can run entire domain independently
- **FSMO Transfer:** Can transfer FSMO roles to Cape Town DCs during disaster
- **Business Continuity:** Bank operations continue even if main data center fails (critical for financial institution)
- **Network Resilience:** Reduces WAN dependency for Cape Town employees

**Branch Offices:** 5 Read-Only Domain Controllers (RODCs) [0.5]

**Configuration:**
- Deploy RODCs at 5 largest branches (most employees/transactions)
- **No RODCs at small branches** (authenticate via WAN to main DCs)

**Justification:**
- **Local Authentication:** Improves logon performance at large branches (no WAN latency)
- **Security:** RODCs don't cache sensitive passwords; if stolen, limited security exposure
- **Physical Security:** Branch offices have limited physical security; RODCs minimize risk
- **Reduced Replication:** RODCs don't replicate changes outbound, reducing WAN bandwidth consumption

**Total Infrastructure:** 10 Domain Controllers
- 3 in Johannesburg + 2 in Cape Town + 5 RODCs = 10 DCs

**Cost-Benefit Analysis:** [1]
- Provides enterprise-grade availability (99.99% uptime)
- Balances cost (10 servers) with reliability needs
- Scalable (can add more RODCs as branches grow)
- Meets banking industry best practices for infrastructure resilience

---

**1.3a Three Security Group Policy Settings** [3]

**1. Password Policy (Account Policy)** [1]
- **Minimum password length:** 12 characters (banking industry standard)
- **Password complexity:** Enabled (require uppercase, lowercase, numbers, special characters)
- **Maximum password age:** 60 days (force regular password changes)
- **Password history:** 24 passwords remembered (prevent password reuse)

**Why for Banking:** Protects against brute force attacks; regulatory requirement (PCI-DSS, banking regulations mandate strong passwords)

**2. Account Lockout Policy** [1]
- **Account lockout threshold:** 5 invalid login attempts
- **Account lockout duration:** 30 minutes
- **Reset lockout counter after:** 30 minutes

**Why for Banking:** Prevents automated password cracking attempts; balances security (stops attackers) with usability (allows legitimate user errors)

**3. Screen Lock/Inactivity Policy** [1]
- **Screen saver timeout:** 10 minutes of inactivity
- **Screen saver password protection:** Enabled (require password to unlock)
- **Automatically lock workstation:** Enabled

**Why for Banking:** Bank employees handle sensitive customer data; prevents unauthorized access when employees leave desks; essential for physical security in branches

**Alternative Acceptable Answers:**
- USB storage device restrictions (prevent data exfiltration)
- BitLocker encryption requirements (protect data if laptops stolen)
- Windows Firewall configuration (network security)
- Audit logging policies (compliance requirement)
- Software restriction policies (prevent malware execution)

---

**1.3b PowerShell Command to Verify GPO Links** [2]

**Command:**
```powershell
Get-GPInheritance -Target "OU=Employees,DC=standardbank,DC=local"
```

**Explanation:**
- `Get-GPInheritance` shows all Group Policy Objects that apply to a specific OU
- Includes GPOs linked directly to the OU plus inherited GPOs from parent containers
- Shows link order (determines precedence)
- Displays enforcement status and blocking status

**Output Interpretation:**
- Lists GPOs in order of application
- Shows which OUs each GPO is linked to
- Indicates if any GPO links are enforced (can't be overridden)
- Shows if inheritance is blocked at this OU

**Alternative Commands (also acceptable):**
```powershell
# Get all GPOs in domain
Get-GPO -All

# Get specific GPO report
Get-GPOReport -Name "GPO Name" -ReportType HTML -Path C:\report.html

# For troubleshooting on client
gpresult /r /scope:computer
```

---

**1.4a Type 1 vs Type 2 Hypervisor Comparison Table** [4]

| Aspect | Type 1 (Bare Metal) | Type 2 (Hosted) |
|--------|---------------------|-----------------|
| **Architecture** | Runs directly on physical hardware | Runs as application on host OS |
| **Performance** | Excellent (near-native speed) | Good (some overhead from host OS) |
| **Latency** | Low (direct hardware access) | Higher (additional abstraction layer) |
| **Security** | More secure (minimal attack surface) | Depends on host OS security |
| **Management** | Dedicated management console | Host OS tools |
| **Cost** | Higher (requires dedicated hardware) | Lower (uses existing systems) |
| **Examples** | VMware ESXi, Microsoft Hyper-V, KVM, Citrix XenServer | VMware Workstation, Oracle VirtualBox, Parallels Desktop |
| **Use Case** | Production servers, data centers | Desktop virtualization, development/testing |

**Detailed Explanation:**

**Type 1 Advantages:**
- No host OS layer means fewer resources consumed by overhead
- Direct hardware access through hypervisor provides maximum performance
- Smaller code base reduces vulnerabilities (enhanced security)
- Designed specifically for virtualization (optimized)

**Type 2 Advantages:**
- Easier to set up (install on existing OS)
- More flexible (can run alongside other applications)
- Lower initial investment (no dedicated hardware required)
- Better for learning and development environments

---

**1.4b Recommendation for Standard Bank Production Servers** [2]

**Recommendation: Type 1 Hypervisor (Bare Metal)**

**Specifically:** Microsoft Hyper-V or VMware vSphere ESXi

**Justification:**

**1. Performance Requirements:**
- Banking transactions demand maximum performance
- ATM transactions, online banking, database queries require minimal latency
- Type 1 provides near-native hardware performance (95-98% of bare metal)
- Type 2's host OS overhead unacceptable for production banking workloads

**2. Security Demands:**
- Financial institutions are prime targets for cyberattacks
- Type 1's minimal attack surface (no host OS to exploit) provides superior security
- Smaller hypervisor code base means fewer vulnerabilities
- Banking regulations mandate highest security standards

**3. Latency Sensitivity:**
- Customer expectations: instant ATM withdrawals, real-time account balances
- Type 1's direct hardware access minimizes latency
- Additional abstraction layer in Type 2 adds unacceptable delays

**4. Availability Requirements:**
- Banks require 99.99%+ uptime (maximum 52 minutes downtime per year)
- Type 1 more stable (no host OS to crash and take down VMs)
- Better fault isolation between VMs
- Superior disaster recovery and high availability features

**5. Regulatory Compliance:**
- PCI-DSS and banking regulations require robust infrastructure
- Type 1 hypervisors meet enterprise security certifications
- Better audit logging and monitoring capabilities

---

**1.5a Page Fault Explanation and Handling Steps** [3]

**What is a Page Fault:**
A page fault occurs when a process tries to access a memory page that is not currently loaded in physical RAM. The page exists on secondary storage (disk) and must be brought into memory before the process can continue.

**Page faults are normal** in virtual memory systems—they're not errors, just events that require OS intervention.

**Four Steps in Page Fault Handling:**

**Step 1: Trap to Operating System** [0.75]
- CPU detects that requested page is not in physical memory (valid bit = 0 in page table)
- Hardware generates page fault exception/interrupt
- Control transfers to OS page fault handler
- Process is blocked (cannot continue until page loaded)

**Step 2: Locate and Validate Page** [0.75]
- OS checks page table to find page location on disk (swap space)
- Validates that memory reference was legal:
  - If valid address: proceed to load page
  - If invalid address (beyond program's address space): terminate process with segmentation fault

**Step 3: Find Free Frame** [0.75]
- OS searches for free frame in physical memory
- **If free frame available:** Use it directly
- **If all frames occupied:** Must select victim page using replacement algorithm (FIFO, LRU, etc.)
  - If victim page modified (dirty bit set), write it to disk first
  - Then reuse that frame

**Step 4: Load Page and Update Tables** [0.75]
- Initiate disk I/O operation to read page from disk into selected frame
- While I/O in progress, process remains blocked (CPU can schedule other processes)
- When I/O completes:
  - Update page table entry (frame number, valid bit = 1)
  - Mark page as present in memory
- Process unblocked and resumes execution
- Instruction that caused page fault is restarted

**Performance Impact:**
- Page faults are expensive (disk I/O is slow: milliseconds vs nanoseconds for RAM)
- Good page replacement algorithms minimize page fault frequency

---

**1.5b Page Replacement Algorithm Recommendation** [1]

**Recommendation: LRU (Least Recently Used)**

**Why LRU for Database Servers:**

**1. Temporal Locality:**
- Database servers exhibit strong temporal locality—recently accessed data likely to be accessed again soon
- Customer queries often access same tables/rows repeatedly (hot data)
- LRU keeps frequently accessed database pages resident in memory

**2. Better than FIFO:**
- FIFO blindly replaces oldest page regardless of usage
- LRU considers actual access patterns (more intelligent)
- Prevents thrashing (excessive paging) for database workloads

**3. Practical Performance:**
- Studies show LRU performs near-optimally for database access patterns
- Approximates OPT (optimal) algorithm in real-world scenarios
- Significantly fewer page faults than FIFO for databases

**4. Database Characteristics:**
- Queries often scan same indexes repeatedly
- Transaction logs accessed frequently
- Cache hit rates improve dramatically with LRU

**Alternative Answer:** LFU (Least Frequently Used) also acceptable—tracks access frequency, suitable for databases with stable access patterns.

---

**1.6a Hybrid Infrastructure Explanation** [2]

**What is Hybrid Infrastructure:**
A hybrid infrastructure combines on-premises infrastructure (physical servers in Standard Bank's Johannesburg data center) with cloud services (Microsoft Azure). Resources, data, and applications exist in both environments, with integration and orchestration between them.

**Why Hybrid Makes Sense for Standard Bank:**

**1. Regulatory Compliance and Data Sovereignty** [0.5]
- South African financial regulations may require customer banking data remain within country borders
- Hybrid allows sensitive customer data on-premises (guaranteed location)
- Non-sensitive data (marketing, HR systems) can move to cloud
- Meets compliance requirements while gaining cloud benefits

**2. Gradual Cloud Adoption** [0.5]
- Legacy banking application (possibly 10-20 years old) stays on-premises
- New applications deployed to cloud (microservices architecture)
- Reduces risk—no "big bang" migration disrupting operations
- Learn cloud technologies progressively

**3. Cost Optimization** [0.5]
- Baseline workload runs on-premises (already invested in data center)
- Variable workloads use cloud (online banking traffic spikes, month-end processing)
- Pay only for cloud resources when needed
- More economical than over-provisioning on-premises for peak capacity

**4. Disaster Recovery Strategy** [0.5]
- Azure serves as DR site (more cost-effective than second physical data center)
- Replicate critical systems to cloud automatically
- Cape Town DR site complemented by cloud DR capability
- Multiple layers of protection for business continuity

---

**1.6b Two Azure Services and Use Cases** [2]

**1. Azure Site Recovery (ASR)** [1]

**Use Case:** Disaster recovery for Standard Bank's banking application servers

**How It Works:**
- Continuous replication of on-premises VMs to Azure
- If Johannesburg data center fails, failover to Azure in minutes
- Automatic orchestration of recovery process
- Can test DR without impacting production

**Benefits for Standard Bank:**
- **Cost-effective:** No need to maintain full second data center
- **Reliability:** Azure provides enterprise-grade availability
- **Compliance:** Meets business continuity requirements
- **RPO/RTO:** Recovery Point Objective < 5 minutes, Recovery Time Objective < 30 minutes
- **Testing:** Regular DR drills without production impact

---

**2. Azure Active Directory (Azure AD)** [1]

**Use Case:** Identity management for online banking portal, mobile banking app, and hybrid integration

**How It Works:**
- Synchronize on-premises AD with Azure AD using Azure AD Connect
- Provides cloud-based authentication for customer-facing applications
- Supports modern authentication protocols (OAuth, SAML, OpenID Connect)

**Benefits for Standard Bank:**
- **Single Sign-On:** Customers access online banking, mobile app with one set of credentials
- **Multi-Factor Authentication:** Enhanced security (password + SMS/app authentication)
- **Conditional Access:** Enforce MFA when customers access from unknown locations
- **Mobile Support:** Native support for mobile devices (iOS, Android)
- **Hybrid Identity:** Seamless integration between on-premises and cloud authentication
- **Scalability:** Azure AD scales automatically for millions of customer authentication requests

**Alternative Acceptable Answers:**
- **Azure Backup:** Cloud backup for on-premises servers without tape infrastructure
- **Azure SQL Database:** Managed database service for new applications
- **Azure Virtual Machines:** Host development/test environments or scale-out capacity
- **Azure Monitor:** Centralized monitoring and alerting

---

### QUESTION 2: Process Management (5 Marks)

**2.1 Process State Diagram** [3]

**Complete Diagram with All Transitions:**

```
         ┌──────────┐
         │   New    │ (Process being created)
         └────┬─────┘
              │ 
              │ admitted (OS allocates resources)
              ↓
         ┌────────────┐                        ┌─────────────┐
    ┌───→│   Ready    │                        │   Running   │
    │    │ (Runnable) │←───────────────────────│ (Executing) │
    │    └──────┬─────┘      timeout/          └──────┬──────┘
    │           │           preemption                 │
    │           │                                      │
    │           │         dispatch                     │
    │           │     (scheduler selects)              │ exit
    │           └──────────────────────────────────────┘
    │                                                   │
    │                                                   ↓
    │                                             ┌──────────┐
    │                                             │Terminated│
    │                                             │ (Exit)   │
    │    I/O or event                             └──────────┘
    │    completion                                     
    │           ↑                                       
    │           │                                       
    │      ┌────┴──────┐                               
    └──────│  Waiting  │←──────────────────────────────┘
           │ (Blocked) │     wait for I/O or event     
           └───────────┘                                
```

**State Descriptions:**
- **New:** Process being created; OS allocating resources
- **Ready:** Process has everything needed except CPU time; waiting to be scheduled
- **Running:** Process currently executing on CPU
- **Waiting/Blocked:** Process waiting for event (I/O completion, signal)
- **Terminated:** Process finished execution; being cleaned up

**Transition Explanations:**
1. **New → Ready (admitted):** OS admits process and allocates memory, places in ready queue
2. **Ready → Running (dispatch):** Scheduler selects process to execute
3. **Running → Ready (timeout/preemption):** Time slice expires OR higher-priority process arrives
4. **Running → Waiting (wait):** Process makes blocking system call (disk I/O, network wait)
5. **Waiting → Ready (I/O complete):** Event completes; process can resume
6. **Running → Terminated (exit):** Process finishes normally or is killed

**Marking:**
- All 5 states present and labeled: 1 mark
- All transitions drawn correctly: 1 mark
- Transition labels accurate: 1 mark

---

**2.2 Involuntary Context Switch Explanation** [2]

**Definition:**
An **involuntary context switch** occurs when the operating system forcibly removes a process from the CPU without the process voluntarily giving up control. The process is preempted against its will.

**Two Examples:**

**Example 1: Time Quantum Expiration (Timer Interrupt)** [1]
- **Scenario:** Process is executing in Round-Robin scheduling with 10ms time slice
- **What Happens:** Process has been running for 10ms; timer hardware generates interrupt
- **OS Action:** Timer interrupt handler runs; scheduler preempts current process
- **Result:** Process moved to ready queue; another process dispatched
- **Why Involuntary:** Process didn't choose to stop—OS forced the context switch

**Example 2: Higher-Priority Process Becomes Ready** [1]
- **Scenario:** Low-priority process running; high-priority process was blocked waiting for disk I/O
- **What Happens:** Disk I/O completes; high-priority process becomes ready
- **OS Action:** In preemptive priority scheduling, OS immediately preempts lower-priority running process
- **Result:** High-priority process dispatched immediately
- **Why Involuntary:** Low-priority process was executing and didn't want to stop

**Contrast with Voluntary:**
- **Voluntary:** Process calls I/O operation, explicitly waits, or terminates
- **Involuntary:** OS decides to remove process from CPU

**Marking:**
- Clear explanation of involuntary context switch: 0.5 marks
- Two valid examples with explanations: 0.75 marks each

---

## SECTION C ANSWERS [17 MARKS]

### QUESTION 1: PowerShell and Group Policy Tasks (10 Marks)

**Task 1: PowerShell Commands** [6 marks]

---

**a) Install Active Directory Domain Services Role** [1]

**Command:**
```powershell
Install-WindowsFeature AD-Domain-Services -IncludeManagementTools
```

**Explanation:**
- `Install-WindowsFeature`: Cmdlet for installing Windows Server roles and features
- `AD-Domain-Services`: The role name for Active Directory Domain Services
- `-IncludeManagementTools`: Installs management tools (GUI and PowerShell modules) along with the role
- This command only installs the role; must still promote server to DC afterward

**Alternative (also correct):**
```powershell
Install-WindowsFeature -Name AD-Domain-Services -IncludeManagementTools
```

**What Happens After:**
- Server Manager shows notification to promote server
- Run `Install-ADDSForest` or use GUI wizard to complete DC promotion

---

**b) Create New Organizational Unit Named "Sales"** [2]

**Command:**
```powershell
New-ADOrganizationalUnit -Name "Sales" -Path "DC=company,DC=local"
```

**Explanation:**
- `New-ADOrganizationalUnit`: Cmdlet for creating new OUs in Active Directory
- `-Name "Sales"`: Specifies the OU name
- `-Path "DC=company,DC=local"`: Distinguished Name (DN) format specifying where to create OU
  - Creates OU directly under domain root
  - "company.local" is the domain name

**Understanding Distinguished Names:**
- DC = Domain Component
- OU = Organizational Unit
- CN = Common Name
- Format: Most specific → Least specific (right to left)

**Alternative with Protection:**
```powershell
New-ADOrganizationalUnit -Name "Sales" -Path "DC=company,DC=local" `
  -ProtectedFromAccidentalDeletion $true
```
This prevents accidental deletion (recommended for production).

**Marking:**
- Correct cmdlet (New-ADOrganizationalUnit): 0.5 marks
- Correct -Name parameter: 0.5 marks
- Correct -Path with proper DN format: 1 mark

---

**c) Create New User Account for John Smith** [2]

**Minimum Acceptable Command:**
```powershell
New-ADUser -Name "John Smith" -SamAccountName "jsmith" `
  -Department "Sales" -Path "OU=Sales,DC=company,DC=local"
```

**More Complete Command (full marks):**
```powershell
New-ADUser -Name "John Smith" `
  -GivenName "John" `
  -Surname "Smith" `
  -SamAccountName "jsmith" `
  -UserPrincipalName "jsmith@company.local" `
  -Department "Sales" `
  -Path "OU=Sales,DC=company,DC=local" `
  -AccountPassword (ConvertTo-SecureString "P@ssw0rd123!" -AsPlainText -Force) `
  -Enabled $true
```

**Explanation:**
- `New-ADUser`: Creates new Active Directory user account
- `-Name`: Display name (full name)
- `-GivenName / -Surname`: First and last name separately
- `-SamAccountName`: Pre-Windows 2000 logon name (username)
- `-UserPrincipalName`: Email-style logon name (user@domain)
- `-Department`: Department attribute (appears in AD user properties)
- `-Path`: OU where user account created
- `-AccountPassword`: Sets initial password (must use SecureString)
- `-Enabled $true`: Enables account immediately (otherwise disabled by default)

**Why ConvertTo-SecureString:**
PowerShell requires passwords as SecureString objects for security. Plain text passwords must be converted.

**Marking:**
- Correct cmdlet (New-ADUser): 0.5 marks
- Name and SamAccountName: 0.5 marks
- Department parameter: 0.5 marks
- Proper syntax and any additional parameters: 0.5 marks

---

**d) Display All Domain Controllers in Forest** [1]

**Command:**
```powershell
Get-ADDomainController -Filter *
```

**Explanation:**
- `Get-ADDomainController`: Retrieves domain controller information
- `-Filter *`: Wildcard to return all domain controllers
- Without filter, returns only the DC you're connected to

**Output Includes:**
- DC name, IP address, site name, FSMO roles held, Global Catalog status, operating system

**Alternative Commands (also acceptable):**
```powershell
# Get all DCs in current domain
Get-ADDomain | Select-Object -ExpandProperty ReplicaDirectoryServers

# Get all DCs in forest
Get-ADForest | Select-Object -ExpandProperty GlobalCatalogs

# Using older command
nltest /dclist:company.local
```

---

**Task 2: Group Policy Management** [4 marks]

---

**a) Computer Configuration vs User Configuration Nodes** [2]

**Computer Configuration:**

**What It Is:**
- Contains policies that apply to **computer objects**
- Settings apply regardless of which user logs in
- Applied during **system startup** (before any user logs in)
- Affects **all users** of that computer

**Examples:**
- Software installation for all users (install Microsoft Office on all computers)
- System-wide security settings (Windows Firewall rules, BitLocker encryption)
- Computer startup scripts (run batch file when computer boots)
- System services configuration (start/stop Windows services)
- Local administrator password policies (LAPS)

**When to Use:**
- Settings should apply to the machine itself
- Requirements don't vary based on who's logged in
- Need settings before user logon

---

**User Configuration:**

**What It Is:**
- Contains policies that apply to **user objects**
- Settings apply regardless of which computer user logs into
- Applied during **user logon** (after authentication)
- Follows the user across **any domain computer**

**Examples:**
- Network drive mappings (map H: to user's home folder)
- Desktop settings (wallpaper, screen saver)
- Folder redirection (redirect Documents to network share)
- User logon scripts (run VBScript when user logs in)
- Application settings specific to users (Outlook configuration)

**When to Use:**
- Settings should follow the user
- Requirements vary by person, not computer
- User-specific customization needed

---

**Key Differences Summary:**

| Aspect | Computer Configuration | User Configuration |
|--------|------------------------|-------------------|
| **Applies To** | Computer objects | User objects |
| **When Applied** | System startup | User logon |
| **Scope** | All users of computer | All computers user logs into |
| **Registry** | HKEY_LOCAL_MACHINE | HKEY_CURRENT_USER |
| **Example** | Install software | Map drives |

**Critical Point:** If both configure the same setting, **Computer Configuration wins** (applies first, but User Configuration can't override certain computer policies).

**Marking:**
- Clear explanation of Computer Configuration: 1 mark
- Clear explanation of User Configuration: 1 mark
- Must include when applied and scope for full marks

---

**b) Domain vs OU Policy Precedence** [2]

**Answer: The OU-level policy takes precedence and wins the conflict.**

**Detailed Explanation:**

**LSDOU Principle:**
Group Policies apply in this order:
1. **L**ocal (computer's local GPO)
2. **S**ite (policies linked to AD site)
3. **D**omain (policies linked to domain)
4. **O**U (policies linked to organizational units)

**Why OU Wins:**
- Policies apply sequentially in LSDOU order
- **Later policies override earlier policies** when settings conflict
- OU policies apply **last**, so they have final say
- This is by design—allows domain-wide baseline with OU-specific customization

**Example Scenario:**

**Setup:**
- **Domain Policy:** Minimum password length = 8 characters
- **Sales OU Policy:** Minimum password length = 12 characters (higher security required)

**Result for Users in Sales OU:**
1. Local policy applies (if any password setting)
2. Site policy applies (if any password setting)
3. Domain policy applies → password length = 8
4. Sales OU policy applies → password length = 12 ✓ **WINS**
5. Sales users must have 12-character passwords

**Result for Users in Marketing OU (no OU policy):**
- Domain policy's 8-character requirement applies (no OU override)

---

**Important Clarifications:**

**1. Only Conflicts Are Overridden:**
- If Domain sets password length = 8 and OU sets screen timeout = 10 min
- Both apply (no conflict)
- Non-conflicting settings **accumulate**

**2. Not Configured vs Disabled:**
- "Not Configured" = don't change setting (earlier policy remains)
- "Disabled" = actively turn off feature (overrides earlier "Enabled")

**3. Enforcement and Blocking:**
- **Enforced links:** Can't be overridden by child OUs
- **Block Inheritance:** OU ignores parent policies (except enforced)
- These are exceptions to normal LSDOU processing

**Practical Use:**
- Set baseline security at domain level
- Customize for specific departments at OU level
- IT Department OU might allow USB drives while domain blocks them

**Marking:**
- Correct answer (OU wins): 0.5 marks
- Explanation using LSDOU: 1 mark
- Example or additional clarification: 0.5 marks

---

### QUESTION 2: Address Translation Calculations (7 Marks)

**Given Information:**
- **Logical Address Space:** 256 pages
- **Page Size:** 4096 bytes (4 KB)
- **Physical Memory:** 128 frames
- **Frame Size:** 4096 bytes (4 KB)

**Important Notes:**
- Page size ALWAYS equals frame size
- Offset bits same in logical and physical addresses
- Only page/frame number bits differ

---

**a) How Many Bits in Logical Address?** [2]

**Method 1: Total Address Space**
```
Step 1: Calculate total logical address space
Logical Address Space = Number of Pages × Page Size
                      = 256 pages × 4096 bytes/page
                      = 1,048,576 bytes
                      = 2^20 bytes

Step 2: Calculate bits needed
Logical Address Bits = log₂(Total Address Space)
                     = log₂(2^20)
                     = 20 bits
```

**Method 2: Page Number + Offset (Preferred)**
```
Step 1: Calculate page number bits
Number of Pages = 256 = 2^8 pages
Page Number Bits = log₂(256) = 8 bits

Step 2: Calculate offset bits
Page Size = 4096 bytes = 2^12 bytes
Offset Bits = log₂(4096) = 12 bits

Step 3: Add them together
Logical Address Bits = Page Number Bits + Offset Bits
                     = 8 + 12
                     = 20 bits
```

**Answer: 20 bits**

**Logical Address Structure:**
```
| Page Number (8 bits) | Offset (12 bits) |
|---------------------|------------------|
| Identifies page     | Location in page |
```

**Marking:**
- Correct calculation method shown: 1 mark
- Correct answer (20 bits): 1 mark

---

**b) How Many Bits in Physical Address?** [2]

**Method: Frame Number + Offset**
```
Step 1: Calculate frame number bits
Number of Frames = 128 = 2^7 frames
Frame Number Bits = log₂(128) = 7 bits

Step 2: Offset bits (same as logical)
Frame Size = 4096 bytes = 2^12 bytes
Offset Bits = log₂(4096) = 12 bits

Step 3: Add them together
Physical Address Bits = Frame Number Bits + Offset Bits
                      = 7 + 12
                      = 19 bits
```

**Answer: 19 bits**

**Physical Address Structure:**
```
| Frame Number (7 bits) | Offset (12 bits) |
|----------------------|------------------|
| Identifies frame     | Location in frame|
```

**Why Physical < Logical:**
- Logical: 256 pages (8 bits)
- Physical: 128 frames (7 bits)
- Physical memory smaller than logical address space
- This is normal—virtual memory allows larger logical than physical

**Marking:**
- Correct calculation method shown: 1 mark
- Correct answer (19 bits): 1 mark

---

**c) How Many Bits for Page Number?** [1.5]

**Calculation:**
```
Number of Pages = 256 = 2^8 pages

Page Number Bits = log₂(Number of Pages)
                 = log₂(256)
                 = log₂(2^8)
                 = 8 bits
```

**Answer: 8 bits**

**Explanation:**
- Need 8 bits to represent 256 different pages (0-255)
- 2^8 = 256 possible values
- Page number identifies which page of the program

---

**d) How Many Bits for Offset?** [1.5]

**Calculation:**
```
Page Size = 4096 bytes = 2^12 bytes

Offset Bits = log₂(Page Size)
            = log₂(4096)
            = log₂(2^12)
            = 12 bits
```

**Answer: 12 bits**

**Explanation:**
- Need 12 bits to address 4096 bytes within a page (0-4095)
- 2^12 = 4096 possible byte locations
- Offset identifies specific byte within the page
- **Same offset in logical and physical addresses** (page and frame are same size)

---

**Summary Verification:**

**Logical Address:**
- Page Number: 8 bits
- Offset: 12 bits
- Total: 8 + 12 = 20 bits ✓

**Physical Address:**
- Frame Number: 7 bits
- Offset: 12 bits
- Total: 7 + 12 = 19 bits ✓

**Address Translation Example:**
```
Logical Address:  |01001010| |110011001100|
                   Page 74    Offset 3276

→ (Look up in page table: Page 74 → Frame 45)

Physical Address: |0101101| |110011001100|
                   Frame 45   Offset 3276
```

---

**END OF EXAMINATION MEMORANDUM**

**Total: 100 Marks**

---

## SUMMARY OF KEY CONCEPTS

**Section A (45 marks):**
- Segmentation vs Paging differences
- Fragmentation types and examples
- Server roles identification
- NTFS, FSMO roles, memory hierarchy
- LRU algorithm calculations

**Section B (38 marks):**
- Domain advantages over workgroup
- OU structure design principles
- FSMO roles and DC deployment
- Group Policy implementation
- Hypervisor types and recommendations
- Page fault handling steps
- Hybrid infrastructure benefits
- Azure services for banking
- Process state diagrams
- Context switching concepts

**Section C (17 marks):**
- PowerShell cmdlets for AD management
- Computer vs User Configuration in GPOs
- LSDOU policy precedence
- Address translation calculations
- Bit calculations for paging systems

---

**Study Tips for Using This Memo:**
1. Don't just memorize answers—understand the reasoning
2. Practice calculations until automatic
3. Draw diagrams (process states, OU structures) repeatedly
4. Test yourself on PowerShell syntax
5. Understand LSDOU and FSMO roles thoroughly
6. Know when to use LRU vs FIFO vs OPT
7. Compare Type 1 vs Type 2 hypervisors in real scenarios

**Good luck with your exam! 🎓**
