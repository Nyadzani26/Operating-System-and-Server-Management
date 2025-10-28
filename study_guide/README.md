# Operating System & Server Management - Exam Study Guide
## Sol Plaatje University - NOSS631 - 100 Marks

---

## TABLE OF CONTENTS
1. [Key Concepts & Formulas](#key-concepts--formulas)
2. [Memory Management](#memory-management)
3. [Server Management](#server-management)
4. [Process Management](#process-management)
5. [Important Calculations](#important-calculations)
6. [PowerShell & Cmdlets](#powershell--cmdlets)

---

## KEY CONCEPTS & FORMULAS

### Memory Address Calculations

**Logical Address Calculation:**
```
Logical Address Bits = log₂(pages × page_size)
```

**Physical Address Calculation:**
```
Physical Address Bits = log₂(frames × frame_size)
```

**Physical Address from Logical (Paging):**
```
Physical Address = (Frame Number × Frame Size) + Offset
```

**Physical Address from Segments:**
```
Physical Address = Base + Offset
Valid if: Offset < Length (otherwise segmentation fault)
```

---

## MEMORY MANAGEMENT

### 1. SEGMENTS vs PAGING

| Aspect | Segments | Paging |
|--------|----------|--------|
| **Division** | Logical division (by program structure) | Physical division (fixed blocks) |
| **Size** | Variable size | Fixed size (typically 4KB) |
| **Calculation** | Physical Addr = Base + Offset | Physical Addr = Frame# × Page Size + Offset |
| **Fragmentation** | External fragmentation | Internal fragmentation |
| **Visibility** | Visible to programmer | Transparent to programmer |

### 2. FRAGMENTATION TYPES

**Internal Fragmentation:**
- Occurs in paging
- Wasted space within allocated memory blocks
- Example: Process needs 4.3KB, gets 8KB page → 3.7KB wasted

**External Fragmentation:**
- Occurs in segmentation
- Free memory scattered in small blocks
- Total free memory sufficient, but not contiguous

**Solutions:**
- Compaction (move processes to create contiguous space)
- Paging (eliminates external fragmentation)
- Best-fit, First-fit, Worst-fit allocation strategies

### 3. PAGE REPLACEMENT ALGORITHMS

**FIFO (First-In-First-Out):**
- Replace oldest page in memory
- Simple but may cause Belady's anomaly
- Easy to implement with queue

**LRU (Least Recently Used):**
- Replace page not used for longest time
- Better performance than FIFO
- Requires hardware support (counter/stack)

**Optimal:**
- Replace page that won't be used for longest time
- Best performance but impossible to implement (needs future knowledge)

**Additional Reference Bit:**
- Uses reference bits to approximate LRU
- Cheaper to implement than full LRU

**LRU Calculation Steps:**
1. Track when each page was last accessed
2. Find page with oldest access time
3. Replace that page
4. Update access times

### 4. PAGE FAULT HANDLING (4 Steps)

1. **Trap to OS** - Hardware detects invalid page reference
2. **Check validity** - Verify address is in process's logical address space
3. **Find free frame** - Locate or create available physical frame
4. **Swap page in** - Load page from disk to memory, update page table

### 5. MEMORY COMPONENTS

**Speed Hierarchy (Fastest → Slowest):**
```
Cache > Main Memory (RAM) > Secondary Storage (Disk)
```

**Relocation & Limit Registers:**
- Each logical address must be **less than** the limit register
- Base register: starting physical address
- Limit register: size of process's address space

### 6. SWAPPING

**Definition:** Process copied into main memory from secondary memory according to requirement

**Types:**
- Swap out: Move process from memory to disk
- Swap in: Load process from disk to memory

---

## SERVER MANAGEMENT

### 1. ACTIVE DIRECTORY (AD)

**Key Components:**
- **Domain:** Logical group of network objects (users, computers, devices)
- **Domain Controller (DC):** Server managing security authentication
- **Organizational Units (OU):** Containers for organizing objects
- **Forest:** Collection of domains sharing schema
- **Tree:** Hierarchy of domains

**Benefits:**
- Centralized management
- Single sign-on (SSO)
- Security policies enforcement
- Resource sharing control

### 2. GROUP POLICIES (GPO)

**Definition:** Centralized configuration management for users and computers

**Common GPO Settings:**
- Password policies (complexity, length, expiration)
- Software installation/removal
- Desktop restrictions
- Security settings
- Logon/logoff scripts

**GPO Application Order (LSDOU):**
1. **L**ocal
2. **S**ite
3. **D**omain
4. **O**U (Organizational Unit)

**GPO Management:**
- Create: `New-GPO` cmdlet
- Link: Link GPO to OU/Domain
- Edit: Configure settings in GPMC
- Enforce: Prevent override by child OUs
- Block inheritance: Prevent parent GPO application

### 3. DOMAIN CONTROLLER ROLES (FSMO)

**Forest-wide roles (1 per forest):**
- Schema Master
- Domain Naming Master

**Domain-wide roles (1 per domain):**
- PDC Emulator (Primary Domain Controller)
- RID Master (Relative ID)
- Infrastructure Master

### 4. VIRTUALIZATION

**Type 1 Hypervisor (Bare Metal):**
- Runs directly on hardware
- Examples: VMware ESXi, Hyper-V, Xen
- Better performance
- Higher security
- Used in enterprise environments

**Type 2 Hypervisor (Hosted):**
- Runs on host OS
- Examples: VMware Workstation, VirtualBox
- Easier to set up
- Lower performance
- More overhead

**Differences:**

| Aspect | Type 1 | Type 2 |
|--------|--------|--------|
| Performance | Higher (direct hardware access) | Lower (OS overhead) |
| Security | More secure (smaller attack surface) | Less secure |
| Use case | Enterprise/Production | Development/Testing |
| Management | Requires specialized tools | Easier, desktop-based |

---

## PROCESS MANAGEMENT

### 1. PROCESS STATES

**Basic States:**
- **New:** Process being created
- **Ready:** Waiting for CPU assignment
- **Running:** Instructions being executed
- **Waiting/Blocked:** Waiting for I/O or event
- **Terminated:** Finished execution

**Suspended States:**
- **Ready Suspended:** In secondary storage, ready to run
- **Blocked Suspended:** In secondary storage, waiting for event

**State Transition Diagram:**
```
New → Ready → Running → Terminated
         ↑      ↓
         └─ Waiting
```

**With Suspended States:**
```
Ready ⟷ Ready/Suspend
Blocked ⟷ Blocked/Suspend
```

### 2. CONTEXT SWITCHING

**Always causes context switch:**
- Blocking system call (process waits for I/O)
- Exit system call (process terminates)
- Timer interrupt (time quantum expired in preemptive scheduling)

**May cause context switch:**
- Disk interrupt (if blocked process becomes ready and has higher priority)

**Definition:** Saving state of current process and loading state of next process

### 3. SCHEDULING POLICIES

**Round-Robin (RR):**
- Time quantum (e.g., 10ms)
- Preemptive scheduling
- Requires timer interrupt support
- Can cause involuntary context switches
- Fair CPU distribution

**Characteristics:**
- **Preemptive:** Yes (timer interrupts process)
- **Fair:** Yes (all processes get equal time)
- **Starvation:** No
- **Overhead:** Medium (frequent context switches)

### 4. INTER-PROCESS COMMUNICATION (IPC)

**Fastest IPC in UNIX:** **Shared Memory**

**IPC Methods (Speed ranking):**
1. Shared Memory (fastest - direct memory access)
2. Pipes
3. Message Queues
4. Sockets (slowest - network overhead)

### 5. NAMESPACES (Linux)

**PID Namespace:**
- Process P1 = init process in namespace (PID 1)
- Orphan processes reaped by P1 (namespace init)
- unshare() creates namespace for calling process (except PID - affects children)

**Types:**
- PID (Process IDs)
- NET (Network)
- MNT (Mount points)
- UTS (Hostname)
- IPC (Inter-process communication)
- USER (User/Group IDs)

---

## INTERRUPTS

### 1. INTERRUPT TYPES

**Hardware Interrupts:**
- Generated by hardware devices (keyboard, disk, timer)
- Asynchronous (unpredictable timing)
- Examples: I/O completion, timer tick

**Software Interrupts:**
- Generated by programs (system calls, exceptions)
- Synchronous (predictable)
- Examples: Division by zero, system call trap

### 2. INTERRUPT HANDLING

**Components:**
- **Interrupt Vector Table (IVT):** Located in **low memory**
- **Interrupt Handler:** Routine to service interrupt
- **IRQ (Interrupt Request):** Hardware interrupt line

**Process:**
1. Device signals interrupt
2. CPU checks interrupt vector table
3. Save current process state
4. Jump to interrupt handler
5. Execute handler
6. Restore process state
7. Resume execution

### 3. APIC (Advanced Programmable Interrupt Controller)

**LAPIC (Local APIC):**
- Per-CPU interrupt controller
- Handles local interrupts (timer, errors)
- Inter-processor interrupts (IPI)

**I/O APIC:**
- Centralized I/O interrupt controller
- Routes interrupts to LAPICs
- Supports more IRQ lines than traditional PIC

**Limited IRQs Issue:**
- Traditional PIC: Only 16 IRQ lines (0-15)
- Problem: More devices than IRQ lines
- Solutions: IRQ sharing, I/O APIC (supports 24+ IRQs), MSI (Message Signaled Interrupts)

---

## POWERSHELL & CMDLETS

### 1. ESSENTIAL CMDLETS

**User Management:**
```powershell
New-ADUser -Name "John Doe" -SamAccountName "jdoe"
Set-ADUser -Identity "jdoe" -Department "IT"
Remove-ADUser -Identity "jdoe"
Get-ADUser -Filter * -Properties *
Enable-ADAccount -Identity "jdoe"
Disable-ADAccount -Identity "jdoe"
```

**Group Management:**
```powershell
New-ADGroup -Name "IT_Team" -GroupScope Global
Add-ADGroupMember -Identity "IT_Team" -Members "jdoe"
Remove-ADGroupMember -Identity "IT_Team" -Members "jdoe"
Get-ADGroupMember -Identity "IT_Team"
```

**Organizational Unit (OU):**
```powershell
New-ADOrganizationalUnit -Name "Sales" -Path "DC=company,DC=com"
Get-ADOrganizationalUnit -Filter *
```

**Group Policy:**
```powershell
New-GPO -Name "Security_Policy"
New-GPLink -Name "Security_Policy" -Target "OU=Sales,DC=company,DC=com"
Get-GPO -All
Get-GPOReport -Name "Security_Policy" -ReportType HTML -Path "report.html"
Invoke-GPUpdate -Force
```

**Computer Management:**
```powershell
New-ADComputer -Name "PC01" -Path "OU=Computers,DC=company,DC=com"
Get-ADComputer -Filter * -Properties *
Remove-ADComputer -Identity "PC01"
```

**Domain Controller:**
```powershell
Get-ADDomainController
Get-ADDomain
Get-ADForest
Test-ComputerSecureChannel -Repair
```

### 2. CMDLET SYNTAX PATTERNS

**Verb-Noun structure:**
- Get-* (retrieve information)
- Set-* (modify settings)
- New-* (create objects)
- Remove-* (delete objects)
- Enable-* (activate)
- Disable-* (deactivate)
- Add-* (add to collection)

**Common Parameters:**
- `-Identity`: Specify object
- `-Name`: Object name
- `-Filter`: Query filter
- `-Properties`: Additional properties to retrieve
- `-Path`: Location in AD hierarchy
- `-Force`: Skip confirmations

### 3. NETWORK SECURITY THREATS

**DOS (Denial of Service):**
- Intended to prevent authorized users from accessing resources
- Floods system with requests
- Makes services unavailable

**Types:**
- SYN Flood
- Ping of Death
- DDoS (Distributed)
- Resource exhaustion

---

## IMPORTANT CALCULATIONS

### Example 1: Logical & Physical Address Bits

**Problem:** 64 pages, 1024 words/page, 32 frames

**Logical Address:**
```
Total logical space = 64 pages × 1024 words = 65,536 words
Logical bits = log₂(65,536) = 16 bits
  - Page number: log₂(64) = 6 bits
  - Offset: log₂(1024) = 10 bits
```

**Physical Address:**
```
Total physical space = 32 frames × 1024 words = 32,768 words
Physical bits = log₂(32,768) = 15 bits
  - Frame number: log₂(32) = 5 bits
  - Offset: log₂(1024) = 10 bits
```

### Example 2: Segment Table Translation

**Segment Table:**
| Segment | Base | Length |
|---------|------|--------|
| 0 | 219 | 600 |
| 1 | 2300 | 14 |
| 2 | 90 | 100 |

**Logical Address (0, 430):**
```
Segment 0, Offset 430
Check: 430 < 600? YES (valid)
Physical = Base + Offset = 219 + 430 = 649
```

**Logical Address (2, 500):**
```
Segment 2, Offset 500
Check: 500 < 100? NO (invalid - segmentation fault)
```

### Example 3: LRU Page Replacement

**Reference String:** 7, 0, 1, 2, 0, 3, 0, 4, 2, 3, 0, 3, 2
**Frames:** 3

```
Step | Ref | Frame1 | Frame2 | Frame3 | Fault? | Replaced
-----|-----|--------|--------|--------|--------|----------
1    | 7   | 7      | -      | -      | Yes    | -
2    | 0   | 7      | 0      | -      | Yes    | -
3    | 1   | 7      | 0      | 1      | Yes    | -
4    | 2   | 2      | 0      | 1      | Yes    | 7 (LRU)
5    | 0   | 2      | 0      | 1      | No     | -
6    | 3   | 2      | 0      | 3      | Yes    | 1 (LRU)
7    | 0   | 2      | 0      | 3      | No     | -
8    | 4   | 4      | 0      | 3      | Yes    | 2 (LRU)
9    | 2   | 4      | 2      | 3      | Yes    | 0 (LRU)
10   | 3   | 4      | 2      | 3      | No     | -
11   | 0   | 0      | 2      | 3      | Yes    | 4 (LRU)
12   | 3   | 0      | 2      | 3      | No     | -
13   | 2   | 0      | 2      | 3      | No     | -

Total Page Faults: 9
```

### Example 4: IDT (Interrupt Descriptor Table)

**IDT Entry Calculation:**
```
IDT Base Address = 0x80000000
Entry Size = 8 bytes
Interrupt # = 5

IDT Entry Address = Base + (Interrupt# × Entry Size)
                  = 0x80000000 + (5 × 8)
                  = 0x80000000 + 40
                  = 0x80000028
```

---

## EXAM TIPS

### Time Management
- **Section A (45 marks):** ~54 minutes (1.2 min/mark)
- **Section B (38 marks):** ~45 minutes (1.2 min/mark)
- **Section C (17 marks):** ~20 minutes (1.2 min/mark)
- **Review:** ~1 minute

### Strategy
1. **Read all questions first** - identify easy wins
2. **Answer calculations last** - check arithmetic twice
3. **Draw diagrams** - for process states, memory layout
4. **Show work** - partial marks for correct method
5. **Memorize cmdlets** - New-, Get-, Set-, Remove- patterns

### Common Mistakes to Avoid
- ❌ Forgetting to check segment length (segmentation fault)
- ❌ Confusing logical vs physical addresses
- ❌ Wrong LRU tracking (use timestamps/access order)
- ❌ Type 1 vs Type 2 hypervisor features
- ❌ GPO application order (LSDOU)
- ❌ PowerShell cmdlet syntax (Verb-Noun)

### Formulas to Memorize
```
✓ Logical Bits = log₂(pages × page_size)
✓ Physical Bits = log₂(frames × frame_size)
✓ Physical Address (Paging) = Frame# × Frame_Size + Offset
✓ Physical Address (Segment) = Base + Offset (if Offset < Length)
✓ Page Faults = Count misses in reference string simulation
```

---

## QUICK REFERENCE TABLES

### Memory Partitioning
| Fixed Partitions | Dynamic Partitions |
|------------------|-------------------|
| Equal/unequal sizes | Variable sizes |
| Internal fragmentation | External fragmentation |
| Simple allocation | Complex allocation |
| Each contains exactly ONE process | Flexible process placement |

### Process Context Switch Triggers
| Always Switch | May Switch |
|--------------|------------|
| Blocking syscall | Disk interrupt + ready process |
| Exit syscall | - |
| Timer interrupt (preemptive) | - |

### Interrupt Table Location
**Low memory** (not high, mid, or both)

### Fastest IPC
**Shared Memory** (not Virtual, Main, or generic Memory)

---

**Good Luck! 🎓**
