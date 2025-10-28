# ANSWER KEY - Practice Exam

---

## SECTION A ANSWERS

### Q1: MATCHING/TABLE - FRAGMENTATION [12 Marks]

**1.1** Memory Management Comparison:

| Aspect | Fixed Partitioning | Dynamic Partitioning | Paging | Segmentation |
|--------|-------------------|---------------------|--------|--------------|
| Division method | Physical, predetermined | Physical, on-demand | Physical, uniform blocks | Logical, by program structure |
| Partition size | Fixed (equal/unequal) | Variable | Fixed (4KB typical) | Variable |
| Fragmentation type | Internal | External | Internal | External |

**1.2** Matching Strategies:
- A-2 (First-fit → first available)
- B-1 (Best-fit → smallest that fits)
- C-3 (Worst-fit → largest)
- D-4 (Next-fit → from last allocation)

**1.3** Fragmentation Solutions:

| Solution | Works for Internal? | Works for External? | Method |
|----------|-------------------|-------------------|---------|
| Compaction | No | Yes | Move processes to create contiguous space |
| Paging | Yes (eliminates) | N/A | Fixed-size blocks prevent external frag |
| Best-fit allocation | No | Reduces (doesn't eliminate) | Choose smallest suitable partition |

---

### Q2: FILL IN THE BLANKS [7 Marks]

1. **domain**
2. **PDC Emulator**
3. **Organizational Unit (OU)**
4. **New-ADUser**
5. **Type 1** (or bare-metal)
6. **Denial of Service (DoS)**
7. **-Force**

---

### Q3: MULTIPLE CHOICE [5 Marks]

3.1: **b) New-GPLink**
3.2: **b) Global**
3.3: **c) PDC Emulator** (it's domain-wide, not forest-wide)
3.4: **b) Directly on the hypervisor layer**
3.5: **c) Invoke-GPUpdate -Force** (d is also correct but PowerShell preferred)

---

### Q4: CALCULATIONS [5 Marks]

**4.1a) Logical Address Bits:**
```
Total logical space = 128 pages × 512 words = 65,536 words
Logical bits = log₂(65,536) = 16 bits
  Page bits: log₂(128) = 7 bits
  Offset bits: log₂(512) = 9 bits
Answer: 16 bits
```

**4.1b) Physical Address Bits:**
```
Total physical space = 64 frames × 512 words = 32,768 words
Physical bits = log₂(32,768) = 15 bits
  Frame bits: log₂(64) = 6 bits
  Offset bits: log₂(512) = 9 bits
Answer: 15 bits
```

**4.2) Page Table Size:**
```
256 pages × 4 bytes/entry = 1,024 bytes = 1 KB
Answer: 1 KB
```

---

### Q5: DOMAIN GROUP POLICIES [10 Marks]

**5.1** GPO Application Order for Sales OU user:
1. Local (computer's local policy)
2. Site (if any site-level GPO exists)
3. Domain (Default Domain Policy)
4. Corporate OU (Password Policy)
5. Sales OU (any GPOs linked here)

**Explanation:** LSDOU order - child OUs inherit parent GPO settings.

**5.2** With Block Inheritance on Branch OU:
Only "Desktop Restrictions" applies to BranchPCs.

**Explanation:** Block Inheritance prevents Default Domain Policy and any site policies from applying. Only GPOs directly linked to Branch OU apply (unless parent GPOs are set to "Enforced").

**5.3** PDC Emulator Purpose:
- Time synchronization across domain
- Password changes processed here first
- Acts as Windows NT PDC for legacy clients
- Processes account lockouts

**Location:** One per domain, typically on main domain controller at company.com domain level.

**5.4** PowerShell Commands:
```powershell
New-GPO -Name "Security_Settings"
New-GPLink -Name "Security_Settings" -Target "OU=IT,OU=Corporate,DC=company,DC=com"
```

---

### Q6: LRU ALGORITHM [6 Marks]

**6.1** Reference String: 1, 2, 3, 4, 1, 2, 5, 1, 2, 3, 4, 5 (4 frames)

| Step | Ref | F1 | F2 | F3 | F4 | Fault? | Replaced |
|------|-----|----|----|----|----|--------|----------|
| 1 | 1 | 1 | - | - | - | Yes | - |
| 2 | 2 | 1 | 2 | - | - | Yes | - |
| 3 | 3 | 1 | 2 | 3 | - | Yes | - |
| 4 | 4 | 1 | 2 | 3 | 4 | Yes | - |
| 5 | 1 | 1 | 2 | 3 | 4 | No | - |
| 6 | 2 | 1 | 2 | 3 | 4 | No | - |
| 7 | 5 | 1 | 2 | 5 | 4 | Yes | 3 (LRU) |
| 8 | 1 | 1 | 2 | 5 | 4 | No | - |
| 9 | 2 | 1 | 2 | 5 | 4 | No | - |
| 10 | 3 | 1 | 2 | 5 | 3 | Yes | 4 (LRU) |
| 11 | 4 | 1 | 4 | 5 | 3 | Yes | 2 (LRU) |
| 12 | 5 | 1 | 4 | 5 | 3 | No | - |

**Total Page Faults: 7**

**6.2** FIFO would likely produce different (possibly more) faults because it replaces based on arrival time, not usage recency. LRU is generally more efficient.

---

## SECTION B ANSWERS

### Q1: FNB SCENARIO [33 Marks]

**1.1a) OU Structure Diagram:**
```
company.com (Domain)
├── Domain Controllers
├── FNB_Users
│   ├── HR
│   ├── Finance
│   ├── IT
│   ├── Customer_Service
│   └── Management
├── FNB_Computers
│   ├── Workstations
│   └── Servers
└── FNB_Groups
```

**1.1b) FSMO Roles:**

**Forest-wide (1 per forest):**
- **Schema Master:** Primary DC at headquarters
- **Domain Naming Master:** Primary DC at headquarters

**Domain-wide (1 per domain):**
- **PDC Emulator:** Primary DC (handles time sync, password changes)
- **RID Master:** Primary or secondary DC (allocates RID pools)
- **Infrastructure Master:** DC not hosting Global Catalog (tracks cross-domain references)

**Placement:** Place Schema Master and Domain Naming Master on well-protected, reliable DC. Separate Infrastructure Master from Global Catalog servers.

**1.2a) Four Security GPOs:**

1. **Password Policy:**
   - Minimum 12 characters
   - Complexity requirements enabled
   - 90-day expiration
   - 5 password history

2. **Account Lockout Policy:**
   - Lockout after 5 failed attempts
   - 30-minute lockout duration
   - Reset counter after 30 minutes

3. **Desktop Restrictions:**
   - Disable Control Panel access
   - Remove Run command
   - Disable command prompt
   - Restrict USB device installation

4. **Software Installation:**
   - Deploy antivirus automatically
   - Install approved applications only
   - Remove unauthorized software

**1.2b) GPO Inheritance:**

**Inheritance:** Child OUs inherit policies from parent OUs and domain.

**Block Inheritance:** Prevents parent GPOs from applying to specific OU. Use for OUs needing different policies (e.g., IT department).

**Enforce:** Forces GPO to apply even if child has Block Inheritance. Use for critical security policies that must apply everywhere.

**FNB Usage:**
- Enforce password policy at domain level
- Block inheritance for IT OU (admins need different restrictions)
- Regular inheritance for department OUs

**1.3a) PowerShell Script:**
```powershell
# Create 5 Finance users
$OUPath = "OU=Finance,OU=FNB_Users,DC=company,DC=com"
$Password = ConvertTo-SecureString "P@ssw0rd123" -AsPlainText -Force

for ($i = 1; $i -le 5; $i++) {
    $username = "fuser0$i"
    $displayName = "Finance User 0$i"
    
    New-ADUser -Name $displayName `
               -SamAccountName $username `
               -UserPrincipalName "$username@company.com" `
               -DisplayName $displayName `
               -Department "Finance" `
               -Path $OUPath `
               -AccountPassword $Password `
               -Enabled $true
}
```

**1.3b) Add to Group:**
```powershell
Add-ADGroupMember -Identity "Finance_Team" -Members fuser01,fuser02,fuser03,fuser04,fuser05
```

**1.3c) Disabled Accounts Report:**
```powershell
Get-ADUser -Filter {Enabled -eq $false} -Properties DisplayName,Department | 
    Select-Object Name,SamAccountName,DisplayName,Department | 
    Export-Csv C:\Reports\DisabledAccounts.csv -NoTypeInformation
```

**1.4a) Hypervisor Comparison:**

| Aspect | Type 1 (Bare Metal) | Type 2 (Hosted) |
|--------|-------------------|-----------------|
| OS Required | No | Yes |
| Performance | High (direct hardware) | Lower (OS overhead) |
| Security | Higher | Lower |
| Management | Complex | Easy |
| Cost | Higher | Lower |
| Examples | VMware ESXi, Hyper-V | VMware Workstation, VirtualBox |

**Recommendation for FNB:** **Type 1 Hypervisor**

**Reasons:**
1. Better performance for production workloads
2. Higher security (critical for banking)
3. Better resource utilization
4. Enterprise support and management tools
5. High availability features

**1.4b) Virtualization Advantages:**

1. **Cost Reduction:**
   - Fewer physical servers needed
   - Lower power and cooling costs
   - Reduced datacenter space

2. **High Availability:**
   - Quick failover between hosts
   - Live migration of VMs
   - Easy disaster recovery with snapshots

**1.5) Network Threats & Mitigations:**

1. **DoS/DDoS Attacks:**
   - **Threat:** Overwhelm servers, preventing customer access
   - **Mitigation:** DDoS protection service, rate limiting, load balancers

2. **Malware/Ransomware:**
   - **Threat:** Encrypt/corrupt banking data
   - **Mitigation:** Antivirus, regular backups, user training, patch management

3. **Phishing/Social Engineering:**
   - **Threat:** Steal credentials, unauthorized access
   - **Mitigation:** Email filtering, MFA, security awareness training

---

### Q2: INTERRUPTS & PAGE FAULTS [5 Marks]

**2.1) Four Steps of Page Fault Handling:**

1. **Trap to OS:** Hardware detects invalid page reference, generates exception
2. **Check Validity:** OS verifies address is in process's logical space (not illegal reference)
3. **Find Free Frame:** Locate available physical frame or use page replacement algorithm
4. **Swap Page In:** Load page from disk to memory, update page table, restart instruction

**2.2) LAPIC vs I/O APIC:**

**LAPIC (Local APIC):**
- One per CPU core
- Handles local interrupts (timer, thermal, performance)
- Receives inter-processor interrupts (IPI)

**I/O APIC:**
- Centralized I/O interrupt controller
- Routes external device interrupts to appropriate LAPIC
- Supports more IRQ lines than traditional PIC (24+ vs 16)

---

## SECTION C ANSWERS

### Q1: POWERSHELL TASKS [10 Marks]

**Task 1a) Create OU:**
```powershell
New-ADOrganizationalUnit -Name "Contractors" -Path "DC=company,DC=com"
```

**Task 1b) Create User:**
```powershell
$Password = ConvertTo-SecureString "P@ssw0rd123" -AsPlainText -Force
New-ADUser -Name "John Smith" `
           -SamAccountName "jsmith" `
           -UserPrincipalName "jsmith@company.com" `
           -Path "OU=Contractors,DC=company,DC=com" `
           -Description "Temporary Contractor" `
           -AccountPassword $Password `
           -ChangePasswordAtLogon $true `
           -Enabled $true
```

**Task 1c) Create Group:**
```powershell
New-ADGroup -Name "Contractor_Access" `
            -GroupScope Global `
            -Path "OU=Contractors,DC=company,DC=com"
```

**Task 1d) Add to Group:**
```powershell
Add-ADGroupMember -Identity "Contractor_Access" -Members "jsmith"
```

**Task 2a) Create GPO:**
```powershell
New-GPO -Name "Contractor_Restrictions"
```

**Task 2b) Link GPO:**
```powershell
New-GPLink -Name "Contractor_Restrictions" -Target "OU=Contractors,DC=company,DC=com"
```

**Task 2c) Generate Report:**
```powershell
Get-GPO -All | ForEach-Object {
    Get-GPOReport -Name $_.DisplayName -ReportType HTML -Path "C:\Reports\$($_.DisplayName).html"
}

# OR for all GPOs in one report:
Get-GPOReport -All -ReportType HTML -Path "C:\Reports\GPO_Report.html"
```

---

### Q2: CMDLETS & AD [7 Marks]

**2.1a) Disable Test Users:**
```powershell
Get-ADUser -Filter {DisplayName -like "Test*"} | Disable-ADAccount
```

**2.1b) Stale Computers:**
```powershell
$Date = (Get-Date).AddDays(-90)
Get-ADComputer -Filter {LastLogonDate -lt $Date} -Properties LastLogonDate
```

**2.2a) Get-ADUser vs Get-ADGroupMember:**

**Get-ADUser:**
- Retrieves user object(s) from AD
- Can filter by user properties
- Returns user attributes
- Example: `Get-ADUser -Filter {Department -eq "IT"}`

**Get-ADGroupMember:**
- Retrieves members of a specific group
- Only works with group identity
- Returns member objects (users, groups, computers)
- Example: `Get-ADGroupMember -Identity "IT_Team"`

**2.2b) Set-ADUser vs Enable-ADAccount:**

**Set-ADUser:**
- Modifies user properties (department, title, phone, etc.)
- Cannot enable/disable account directly
- General purpose property modification
- Example: `Set-ADUser -Identity "jdoe" -Department "Sales"`

**Enable-ADAccount:**
- Specifically enables a disabled account
- Sets Enabled property to $true
- Single purpose cmdlet
- Example: `Enable-ADAccount -Identity "jdoe"`

---

## BONUS QUESTIONS ANSWERS

**Q1: Segment Table:**
- (0, 250): 250 < 500? YES → 1400 + 250 = **1650**
- (1, 130): 130 < 120? NO → **SEGMENTATION FAULT**
- (2, 400): 400 < 850? YES → 4300 + 400 = **4700**
- (3, 500): 500 < 600? YES → 3200 + 500 = **3700**

**Q10: Always Context Switch:**
- 2 (Timer interrupt in round-robin)
- 3 (System call read() - blocking)
- 5 (Fork creates new process, switch to it or continue)

**NOT always:**
- 1 (Page fault may be satisfied without switch)
- 4 (Division by zero - exception handler, not necessarily switch)

---

## KEY FORMULAS SUMMARY

```
✓ Logical Bits = log₂(pages × page_size)
✓ Physical Bits = log₂(frames × frame_size)  
✓ Page # bits = log₂(# of pages)
✓ Offset bits = log₂(page/frame size)
✓ Physical Addr (paging) = Frame# × Frame_Size + Offset
✓ Physical Addr (segment) = Base + Offset (if Offset < Length)
✓ Page Table Size = # pages × entry size
```

**Good Luck on Your Exam! 🎓**
