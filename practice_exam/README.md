# PRACTICE EXAM - Operating System & Server Management
## NOSS631 - 100 MARKS - 2 HOURS

**INSTRUCTIONS:**
- Answer ALL questions
- Show all calculations
- Section A: 45 marks
- Section B: 38 marks  
- Section C: 17 marks

---

# SECTION A [45 MARKS]

## QUESTION 1: MATCHING/TABLE - FRAGMENTATION [12 Marks]

**1.1** Complete Table 1 comparing different memory management aspects:

| Aspect | Fixed Partitioning | Dynamic Partitioning | Paging | Segmentation |
|--------|-------------------|---------------------|--------|--------------|
| Division method | | | | |
| Partition size | | | | |
| Fragmentation type | | | | |

[4 Marks]

**1.2** Match the memory allocation strategy with its description:

| Strategy | Description |
|----------|-------------|
| A. First-fit | 1. Allocate smallest partition that fits |
| B. Best-fit | 2. Allocate first available partition that fits |
| C. Worst-fit | 3. Allocate largest available partition |
| D. Next-fit | 4. Like first-fit but starts from last allocation |

[4 Marks]

**1.3** Complete the table comparing fragmentation solutions:

| Solution | Works for Internal? | Works for External? | Method |
|----------|-------------------|-------------------|---------|
| Compaction | | | |
| Paging | | | |
| Best-fit allocation | | | |

[4 Marks]

---

## QUESTION 2: FILL IN THE BLANKS - SERVER FOCUSED [7 Marks]

Complete each statement with the correct term:

1. In Active Directory, a __________ is a logical group of network objects that share the same directory database. [1]

2. The __________ role in FSMO is responsible for ensuring that time synchronization is maintained across the domain. [1]

3. Group Policy Objects are applied in the following order: Local, Site, Domain, and __________. [1]

4. In Windows Server, the cmdlet __________ is used to create a new user account in Active Directory. [1]

5. A __________ hypervisor runs directly on the hardware without requiring a host operating system. [1]

6. The security threat that prevents authorized users from accessing network resources is called __________. [1]

7. In PowerShell, the parameter __________ is commonly used to skip confirmation prompts when removing objects. [1]

---

## QUESTION 3: MULTIPLE CHOICE - SERVER FOCUSED [5 Marks]

**3.1** Which PowerShell cmdlet would you use to link a Group Policy Object to an Organizational Unit? [1]
- a) Link-GPO
- b) New-GPLink  
- c) Set-GPLink
- d) Add-GPO

**3.2** What is the default scope for a new Active Directory group? [1]
- a) Universal
- b) Global
- c) Domain Local
- d) Local

**3.3** Which of the following is NOT a forest-wide FSMO role? [1]
- a) Schema Master
- b) Domain Naming Master
- c) PDC Emulator
- d) All of the above are forest-wide

**3.4** In a Type 1 hypervisor architecture, where do virtual machines run? [1]
- a) On top of the host operating system
- b) Directly on the hypervisor layer
- c) Inside containers
- d) On separate physical servers

**3.5** Which command would force a Group Policy update on a client computer? [1]
- a) Update-GPO -Force
- b) Refresh-GroupPolicy
- c) Invoke-GPUpdate -Force
- d) gpupdate /force

---

## QUESTION 4: CALCULATIONS [5 Marks]

**4.1** Consider a logical address space of 128 pages with 512 words per page, mapped onto a physical memory of 64 frames.

a) How many bits are in the logical address? [2]

b) How many bits are in the physical address? [2]

**4.2** If a page table entry is 4 bytes and there are 256 pages, what is the total size of the page table? [1]

---

## QUESTION 5: DOMAIN GROUP POLICIES [10 Marks]

Study Figure 1 showing the Active Directory structure:

```
Forest: company.com
├── Domain: company.com
│   ├── OU: Corporate
│   │   ├── OU: Sales
│   │   │   └── Users: SalesTeam
│   │   └── OU: IT
│   │       └── Users: ITTeam
│   └── OU: Branch
│       └── Computers: BranchPCs
└── GPOs:
    - Default Domain Policy (linked to Domain)
    - Password Policy (linked to Corporate OU)
    - Desktop Restrictions (linked to Branch OU)
```

**5.1** Explain the order in which Group Policies will be applied to a user in the Sales OU. [3]

**5.2** If the Branch OU has "Block Inheritance" enabled, which GPOs will apply to computers in BranchPCs? Explain. [3]

**5.3** Describe the purpose of the PDC Emulator role and where it would be located in this structure. [2]

**5.4** Write the PowerShell command to create a new GPO called "Security_Settings" and link it to the IT OU. [2]

---

## QUESTION 6: MEMORY CALCULATIONS - LRU [6 Marks]

**6.1** Given the following page reference string and 4 frames, calculate the number of page faults using the LRU algorithm:

**Reference String:** 1, 2, 3, 4, 1, 2, 5, 1, 2, 3, 4, 5

Show your work in a table format with columns: Step, Reference, Frame 1, Frame 2, Frame 3, Frame 4, Fault?, Page Replaced [5]

**6.2** Would FIFO produce more or fewer page faults for this reference string? Why? [1]

---

# SECTION B [38 MARKS]

## QUESTION 1: SCENARIO - FNB BANK SERVER IMPLEMENTATION [33 Marks]

**SCENARIO:**
First National Bank (FNB) has hired you as their IT Consultant. They are planning to upgrade their infrastructure with the following requirements:

- Deploy 50 new Windows Server 2022 domain controllers across 5 branches
- Implement Active Directory for 2,000 employees
- Configure Group Policies for security compliance
- Set up automated user provisioning with PowerShell
- Implement virtualization for their application servers
- Ensure high availability and disaster recovery

Answer the following questions:

**1.1** **Active Directory Design** [7]

a) Design an OU structure for FNB with the following departments: HR, Finance, IT, Customer Service, and Management. Draw a diagram. [3]

b) Explain what FSMO roles need to be configured and which server(s) should hold each role. [4]

**1.2** **Group Policy Implementation** [8]

a) List and explain FOUR security-related Group Policies you would implement for FNB. [4]

b) Explain the concept of GPO inheritance and how you would use "Block Inheritance" and "Enforce" in the FNB environment. [4]

**1.3** **PowerShell Automation** [9]

a) Write a PowerShell script to create 5 new users in the Finance OU with the following details: [5]
   - Usernames: fuser01, fuser02, fuser03, fuser04, fuser05
   - Display Names: Finance User 01, Finance User 02, etc.
   - Department: Finance
   - Enable the accounts

b) Write a PowerShell command to add all Finance users to a group called "Finance_Team". [2]

c) Write a command to generate a report of all disabled user accounts in the domain. [2]

**1.4** **Virtualization Strategy** [6]

a) Compare Type 1 and Type 2 hypervisors. Which would you recommend for FNB's production servers and why? [4]

b) Explain TWO advantages of server virtualization for FNB. [2]

**1.5** **Network Security** [3]

Identify and explain THREE types of network threats FNB should protect against, and suggest one mitigation strategy for each.

---

## QUESTION 2: INTERRUPTS & PAGE FAULTS [5 Marks]

**2.1** Explain the four steps involved in handling a page fault. [4]

**2.2** Differentiate between LAPIC and I/O APIC in the context of interrupt handling. [1]

---

# SECTION C - PRACTICAL [17 MARKS]

## QUESTION 1: POWERSHELL & GROUP POLICY TASK [10 Marks]

You need to perform the following administrative tasks using PowerShell:

**Task 1: User Management** [5]

Write PowerShell commands to:

a) Create a new OU called "Contractors" under the root domain. [1]

b) Create a user "jsmith" (John Smith) in the Contractors OU with:
   - Password: P@ssw0rd123 (must change at first logon)
   - Description: "Temporary Contractor"
   - Account enabled [2]

c) Create a security group "Contractor_Access" in the Contractors OU. [1]

d) Add jsmith to the Contractor_Access group. [1]

**Task 2: Group Policy Configuration** [5]

Write PowerShell commands to:

a) Create a new GPO named "Contractor_Restrictions". [1]

b) Link this GPO to the Contractors OU. [2]

c) Generate an HTML report of all GPOs in the domain and save it to C:\Reports\GPO_Report.html. [2]

---

## QUESTION 2: CMDLETS & ACTIVE DIRECTORY [7 Marks]

**2.1** Write a PowerShell one-liner to: [4]

a) Get all users whose display name starts with "Test" and disable their accounts. [2]

b) Get all computers that haven't logged on in the last 90 days. [2]

**2.2** Explain the difference between these cmdlets: [3]

a) `Get-ADUser` vs `Get-ADGroupMember` [1.5]

b) `Set-ADUser` vs `Enable-ADAccount` [1.5]

---

# END OF PRACTICE EXAM

**TOTAL: 100 MARKS**

---

# ADDITIONAL PRACTICE QUESTIONS

## BONUS SECTION: EXTRA PRACTICE

### Memory Management Practice

**Q1:** Consider the following segment table:

| Segment | Base | Length |
|---------|------|--------|
| 0 | 1400 | 500 |
| 1 | 6300 | 120 |
| 2 | 4300 | 850 |
| 3 | 3200 | 600 |

Calculate the physical addresses for:
- a) (0, 250)
- b) (1, 130)
- c) (2, 400)
- d) (3, 500)

### Process States Practice

**Q2:** Draw a complete process state diagram including:
- Basic 5 states
- Two suspended states (Ready/Suspend, Blocked/Suspend)
- All transitions with labels

### LRU Practice

**Q3:** Reference string: 2, 3, 2, 1, 5, 2, 4, 5, 3, 2, 5, 2
Frames: 3
Calculate page faults using LRU algorithm.

### PowerShell Practice

**Q4:** Write commands to:
1. Create 10 users (user01-user10) in a loop
2. Set their passwords to never expire
3. Add them all to a group "TestUsers"
4. Move them to an OU "Test_OU"

### Active Directory Practice

**Q5:** Explain the difference between:
- Domain vs Organizational Unit
- Security Group vs Distribution Group
- Forest vs Domain vs Tree

### Hypervisor Practice

**Q6:** Complete comparison table:

| Feature | Type 1 | Type 2 |
|---------|--------|--------|
| OS Required? | | |
| Performance | | |
| Use Case | | |
| Examples | | |

### Interrupt Practice

**Q7:** If IDT base = 0xFFFF0000, entry size = 16 bytes:
- Calculate address of interrupt #10
- Calculate address of interrupt #25
- Calculate interrupt # for address 0xFFFF0080

### Namespace Practice

**Q8:** True/False with explanation:
1. unshare() immediately moves the calling process to a new PID namespace
2. The init process in a PID namespace always has PID 1
3. Orphan processes in a PID namespace are reaped by the host's init

### Group Policy Practice

**Q9:** Scenario: You have:
- Domain Policy: Password min 8 chars
- OU Policy: Password min 12 chars (enforced)
- Local Policy: Password min 6 chars

What is the effective password length requirement? Explain.

### Context Switch Practice

**Q10:** Which of these ALWAYS cause context switch?
1. Page fault
2. Timer interrupt (round-robin scheduler)
3. System call read() from disk
4. Division by zero exception
5. Fork() system call

---

**Practice makes perfect! Work through all questions multiple times.**
