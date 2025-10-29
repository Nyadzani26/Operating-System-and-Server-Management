# NOSS631 - SAMPLE EXAMINATION
## Operating Systems & Server Management

---

**PROGRAMME:** IT0603  
**MODULE CODE:** NOSS631  
**MODULE DESCRIPTION:** Operating Systems & Server Management  
**DURATION:** 2 Hours  
**TOTAL MARKS:** 100  
**EXAMINER:** Based on Course Content  

---

## INSTRUCTIONS TO CANDIDATES

- Answer **ALL** questions
- Write your student number on your answer sheet
- This question paper consists of **THREE** sections:
  - **Section A:** 45 Marks (Objective & Short Questions)
  - **Section B:** 38 Marks (Scenarios & Application)
  - **Section C:** 17 Marks (Technical Tasks & Calculations)
- Show all calculations and working
- Use diagrams where appropriate
- Non-programmable calculators allowed

---

## SECTION A [45 MARKS]

### QUESTION 1: Matching and Processing (12 Marks)

**1.1** Complete the following table comparing Segmentation and Paging. [5]

| Aspect | Segmentation | Paging |
|--------|--------------|--------|
| **Division Method** | | |
| **Size Characteristics** | | |
| **Fragmentation Type** | | |
| **Formula/Calculation** | | |
| **User Visibility** | | |

**1.2** Complete the table on fragmentation types. [4]

| Fragmentation Type | Definition | Where It Occurs | Example |
|-------------------|------------|-----------------|---------|
| **Internal Fragmentation** | | | |
| **External Fragmentation** | | | |

**1.3** Match the following Windows Server roles with their functions: [3]

**Roles:**
A. Active Directory Domain Services  
B. DNS Server  
C. DHCP Server  
D. File Server  
E. Web Server (IIS)  
F. Print Server  

**Functions:**
1. Provides centralized file storage and sharing ____
2. Manages network printers and print queues ____
3. Provides domain controller functionality and authentication ____
4. Automatically assigns IP addresses to network clients ____
5. Resolves domain names to IP addresses ____
6. Hosts websites and web applications ____

---

### QUESTION 2: Fill in the Blanks (10 Marks)

Complete each statement with the correct term:

1. A _____________ is a Windows Server role that provides major functionality, while a _____________ is a supporting software component. [2]

2. The _____________ file system provides file-level security, compression, and encryption capabilities in Windows Server. [1]

3. In Active Directory, the _____________ is the core structural unit containing OUs and objects. [1]

4. The _____________ FSMO role is responsible for allocating RID pools to domain controllers. [1]

5. When a page fault occurs and all frames are occupied, the _____________ algorithm replaces the page that won't be used for the longest time in the future. [1]

6. The _____________ system call creates a new child process in UNIX/Linux by duplicating the parent process. [1]

7. In memory management, _____________ is generally faster than cache, and cache is faster than _____________. [2]

8. A _____________ hypervisor runs directly on hardware, while a _____________ hypervisor runs on a host operating system. [1]

---

### QUESTION 3: Multiple Choice (5 Marks)

Choose the BEST answer for each question.

1. Which Active Directory management tool is built on PowerShell? [1]
   - a) Active Directory Users and Computers
   - b) Active Directory Administrative Center
   - c) Server Manager
   - d) Group Policy Management Console

2. Which RAID level provides fault tolerance through mirroring? [1]
   - a) RAID 0
   - b) RAID 1
   - c) RAID 5
   - d) RAID 10

3. In a domain environment, where are user accounts stored? [1]
   - a) On each individual computer
   - b) In the Registry
   - c) In Active Directory
   - d) In local SAM database

4. Which page replacement algorithm suffers from Belady's Anomaly? [1]
   - a) LRU
   - b) LFU
   - c) FIFO
   - d) OPT

5. What happens when a blocking system call is made? [1]
   - a) The process continues executing
   - b) A context switch always occurs
   - c) The CPU shuts down
   - d) Nothing happens

---

### QUESTION 4: Operating Systems Calculations (5 Marks)

Consider the following segment table:

| Segment | Base | Length |
|---------|------|--------|
| 0 | 300 | 400 |
| 1 | 1800 | 200 |
| 2 | 500 | 250 |

Calculate the physical addresses for the following logical addresses. Show your work and indicate if invalid: [5]

a) (0, 150)  
b) (1, 250)  
c) (2, 100)  
d) (0, 399)  
e) (1, 50)  

---

### QUESTION 5: Server Activity - Group Policy (10 Marks)

**Scenario:** You are a Windows Server administrator at a company with 500 employees. Management wants to enforce the following policies:

- All users must have strong passwords (minimum 10 characters, complexity required)
- Desktop wallpaper must display company logo
- USB storage devices should be disabled
- Screen lock after 10 minutes of inactivity

Refer to the Group Policy structure below:

```
Domain: company.local
├── Default Domain Policy (linked to domain)
├── OU: Employees
│   ├── OU: Marketing (50 users)
│   ├── OU: IT Department (20 users)
│   └── OU: Finance (30 users)
└── OU: Domain Controllers
    └── Default Domain Controllers Policy
```

**Answer the following:**

**5.1** Explain where you would configure the password policy and why. [3]

**5.2** Explain the Group Policy application order (LSDOU) and how it affects policy enforcement. [4]

**5.3** If the IT Department needs an exception to use USB devices, explain how you would implement this without affecting other departments. [3]

---

### QUESTION 6: Memory Calculations - LRU Algorithm (6 Marks)

Given the following page reference string: **1, 2, 3, 4, 1, 2, 5, 1, 2, 3, 4, 5**

With **3 frames** available, calculate the number of page faults using the **LRU (Least Recently Used)** algorithm.

Show your work clearly with frame contents at each step. [6]

---

## SECTION B [38 MARKS]

### QUESTION 1: Server Infrastructure Scenario (33 Marks)

**Scenario:**

Standard Bank of South Africa is implementing a new hybrid infrastructure to support their nationwide operations. They have 15 branches across the country, a main data center in Johannesburg, and a disaster recovery site in Cape Town. The bank handles sensitive financial data and requires high availability, security, and performance.

**Current Environment:**
- 200 employees (tellers, managers, IT staff, executives)
- 50 ATMs nationwide
- Online banking portal
- Mobile banking application
- Legacy banking application on-premises
- Plans to migrate some services to Microsoft Azure

**Requirements:**
- Centralized user management
- Secure authentication
- Automated desktop configuration
- Disaster recovery solution
- High-performance database servers
- Compliance with financial regulations

**As a Senior Systems Architect, answer the following:**

---

**1.1 Active Directory Design** [8]

a) Explain why Standard Bank should use a domain-based network instead of a workgroup. List FOUR specific advantages for this environment. [4]

b) Design an appropriate OU (Organizational Unit) structure for Standard Bank. Draw the structure and explain your design choices. [4]

---

**1.2 FSMO Roles and Domain Controllers** [6]

a) Standard Bank wants to deploy multiple domain controllers for fault tolerance. Explain the purpose of THREE forest-wide or domain-wide FSMO roles and why they're important for the bank. [3]

b) Recommend how many domain controllers should be deployed and where (considering main data center, DR site, and branches). Justify your recommendation. [3]

---

**1.3 Group Policy Implementation** [5]

a) List THREE specific Group Policy settings you would configure to enhance security for Standard Bank employees. [3]

b) Explain how you would use PowerShell to verify which Group Policy Objects are linked to a specific OU. Provide the command. [2]

---

**1.4 Virtualization Strategy** [6]

a) Standard Bank plans to virtualize their servers. Compare Type 1 and Type 2 hypervisors using a table format. [4]

b) Recommend which hypervisor type Standard Bank should use for their production banking servers and explain why. [2]

---

**1.5 Memory Management** [4]

The bank's database server is experiencing performance issues with frequent page faults.

a) Explain what a page fault is and list THREE steps involved in page fault handling. [3]

b) What page replacement algorithm would you recommend for a database server and why? [1]

---

**1.6 Hybrid Infrastructure and Azure Integration** [4]

a) Explain what a hybrid infrastructure is and why it makes sense for Standard Bank. [2]

b) Name TWO Azure services that could benefit Standard Bank and explain their use cases. [2]

---

### QUESTION 2: Process Management (5 Marks)

**This question is based on Operating Systems concepts:**

**2.1** Draw a complete process state diagram showing:
- Five basic states (New, Ready, Running, Waiting, Terminated)
- All transitions between states
- Labels for each transition (e.g., "admitted", "dispatch", "timeout") [3]

**2.2** Explain what causes an involuntary context switch and give TWO examples. [2]

---

## SECTION C [17 MARKS]

### QUESTION 1: PowerShell and Group Policy Tasks (10 Marks)

You are managing a Windows Server 2022 environment with Active Directory.

**Task 1:** Write PowerShell commands to perform the following operations: [6]

a) Install the Active Directory Domain Services role with management tools. [1]

b) Create a new Organizational Unit named "Sales" in the domain "company.local". [2]

c) Create a new user account with the following details: [2]
   - Name: John Smith
   - Username: jsmith
   - Department: Sales

d) Display all domain controllers in the forest. [1]

**Task 2:** Group Policy Management [4]

a) Explain the difference between Computer Configuration and User Configuration nodes in a GPO. [2]

b) If a policy is configured at both the Domain level and OU level with conflicting settings, which one takes precedence and why? [2]

---

### QUESTION 2: Address Translation Calculation (7 Marks)

Consider a computer system with the following specifications:
- Logical address space: **256 pages**
- Page size: **4096 bytes (4 KB)**
- Physical memory: **128 frames**
- Frame size: **4096 bytes (4 KB)**

**Calculate the following (show all working):**

a) How many bits are in the logical address? [2]

b) How many bits are in the physical address? [2]

c) How many bits are used for the page number? [1.5]

d) How many bits are used for the offset? [1.5]

---

## END OF EXAMINATION

**Total: 100 Marks**

**Remember to:**
- Check all your answers
- Ensure all calculations show working
- Label all diagrams clearly
- Review your PowerShell commands for syntax

**Good luck!**
