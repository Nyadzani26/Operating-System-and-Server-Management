# QUICK REFERENCE CHEAT SHEET
## Operating System & Server Management - NOSS631

---

## ⚡ FORMULAS (MEMORIZE THESE!)

```
📐 LOGICAL ADDRESS BITS = log₂(pages × page_size)
📐 PHYSICAL ADDRESS BITS = log₂(frames × frame_size)
📐 PAGE # BITS = log₂(total pages)
📐 OFFSET BITS = log₂(page/frame size)
📐 PHYSICAL ADDRESS (PAGING) = Frame# × Frame_Size + Offset
📐 PHYSICAL ADDRESS (SEGMENT) = Base + Offset (only if Offset < Length)
📐 PAGE TABLE SIZE = Number_of_Pages × Entry_Size
📐 IDT ENTRY ADDRESS = IDT_Base + (Interrupt# × Entry_Size)
```

---

## 🔢 LOGARITHM QUICK REFERENCE

```
log₂(2) = 1          log₂(1024) = 10
log₂(4) = 2          log₂(2048) = 11
log₂(8) = 3          log₂(4096) = 12
log₂(16) = 4         log₂(8192) = 13
log₂(32) = 5         log₂(16384) = 14
log₂(64) = 6         log₂(32768) = 15
log₂(128) = 7        log₂(65536) = 16
log₂(256) = 8        log₂(131072) = 17
log₂(512) = 9        log₂(262144) = 18
```

---

## 📊 COMPARISON TABLES

### Segments vs Paging

| Feature | Segments | Paging |
|---------|----------|--------|
| **Division** | Logical (by program) | Physical (uniform) |
| **Size** | Variable | Fixed (4KB typical) |
| **Formula** | Base + Offset | Frame# × Size + Offset |
| **Fragmentation** | External | Internal |
| **Programmer** | Visible | Transparent |

### Type 1 vs Type 2 Hypervisor

| Feature | Type 1 | Type 2 |
|---------|--------|--------|
| **Runs on** | Hardware | Host OS |
| **Performance** | High | Lower |
| **Security** | Better | Lower |
| **Use** | Production | Development |
| **Examples** | ESXi, Hyper-V | VirtualBox, VMware WS |

### FSMO Roles

| Role | Scope | Function |
|------|-------|----------|
| **Schema Master** | Forest | Manages AD schema changes |
| **Domain Naming** | Forest | Adds/removes domains |
| **PDC Emulator** | Domain | Time sync, passwords |
| **RID Master** | Domain | Allocates RID pools |
| **Infrastructure** | Domain | Cross-domain references |

---

## 💾 MEMORY MANAGEMENT

### Page Replacement Algorithms

**FIFO:** Replace oldest page (may cause Belady's anomaly)
**LRU:** Replace least recently used (best performance, needs hardware)
**Optimal:** Replace page unused longest in future (impossible to implement)

### Page Fault Steps

1. **Trap** to OS
2. **Check** validity
3. **Find** free frame
4. **Swap** page in

### Fragmentation

**Internal:** Wasted space WITHIN allocated blocks (Paging)
**External:** Free space BETWEEN blocks (Segmentation)

**Solutions:**
- Compaction (move processes together)
- Paging (eliminates external)
- Better allocation (Best-fit, First-fit)

---

## 🖥️ POWERSHELL CMDLETS

### User Management
```powershell
New-ADUser -Name "John Doe" -SamAccountName "jdoe" -Enabled $true
Set-ADUser -Identity "jdoe" -Department "IT"
Get-ADUser -Filter * -Properties *
Get-ADUser -Identity "jdoe"
Enable-ADAccount -Identity "jdoe"
Disable-ADAccount -Identity "jdoe"
Remove-ADUser -Identity "jdoe"
```

### Group Management
```powershell
New-ADGroup -Name "IT_Team" -GroupScope Global
Add-ADGroupMember -Identity "IT_Team" -Members "jdoe"
Get-ADGroupMember -Identity "IT_Team"
Remove-ADGroupMember -Identity "IT_Team" -Members "jdoe"
```

### OU Management
```powershell
New-ADOrganizationalUnit -Name "Sales" -Path "DC=company,DC=com"
Get-ADOrganizationalUnit -Filter *
```

### Group Policy
```powershell
New-GPO -Name "Security_Policy"
New-GPLink -Name "Security_Policy" -Target "OU=Sales,DC=company,DC=com"
Get-GPO -All
Get-GPOReport -Name "Policy" -ReportType HTML -Path "report.html"
Invoke-GPUpdate -Force
```

### Common Parameters
```
-Identity      Specify object
-Filter        Query (use * for all, or {Property -eq "Value"})
-Properties    Additional attributes to get
-Path          AD location
-Force         Skip confirmations
```

---

## 🌐 SERVER CONCEPTS

### GPO Application Order: **LSDOU**
1. **L**ocal
2. **S**ite
3. **D**omain
4. **O**U (Organizational Unit)

Last applied = Highest priority

### GPO Modifiers
- **Enforce:** Forces policy, overrides Block Inheritance
- **Block Inheritance:** Stops parent GPOs from applying

### Active Directory Structure
```
Forest
└── Domain
    └── OU
        ├── Users
        ├── Groups
        └── Computers
```

---

## 🔄 PROCESS MANAGEMENT

### Process States
```
NEW → READY → RUNNING → TERMINATED
        ↑        ↓
        └─ WAITING/BLOCKED
```

### With Suspend States
```
READY ⟷ READY/SUSPEND
BLOCKED ⟷ BLOCKED/SUSPEND
```

### Context Switch Triggers

**ALWAYS:**
- Blocking system call (read, write from disk)
- Exit system call
- Timer interrupt (preemptive scheduler)

**MAYBE:**
- Disk interrupt (if ready process has higher priority)

### Scheduling - Round Robin
- Time quantum (e.g., 10ms)
- Preemptive
- Requires timer interrupt
- Fair but overhead from context switches

---

## ⚡ INTERRUPTS

### Types
**Hardware:** Device-generated (keyboard, disk, timer) - Asynchronous
**Software:** Program-generated (syscall, exception) - Synchronous

### Interrupt Vector Table
**Location:** Low memory (NOT high, mid, or both)

### APIC
**LAPIC:** Local (per-CPU), handles local interrupts, IPIs
**I/O APIC:** Central, routes device interrupts to LAPICs, 24+ IRQs

### Limited IRQs Problem
**Traditional PIC:** Only 16 IRQs (0-15)
**Solution:** IRQ sharing, I/O APIC, MSI

---

## 🔐 SECURITY

### Network Threats

**DoS/DDoS:** Prevent authorized access (flood attacks)
**Malware:** Viruses, ransomware, trojans
**Phishing:** Social engineering for credentials
**MITM:** Intercept communications
**Brute Force:** Password guessing attacks

---

## 📝 EXAM STRATEGIES

### Time Allocation (100 marks, 2 hours)
- **Section A (45 marks):** ~54 minutes
- **Section B (38 marks):** ~45 minutes
- **Section C (17 marks):** ~20 minutes
- **Review:** ~1 minute

### Question Approach
1. ✅ Read ALL questions first
2. ✅ Answer easy questions first
3. ✅ Show ALL work for calculations
4. ✅ Double-check arithmetic
5. ✅ Draw diagrams where helpful

### Common Mistakes to AVOID
- ❌ Not checking segment length (causes segmentation fault)
- ❌ Mixing up logical vs physical addresses
- ❌ Wrong LRU tracking (use access timestamps!)
- ❌ Confusing Type 1/Type 2 hypervisor features
- ❌ Wrong GPO order (remember LSDOU)
- ❌ Incorrect cmdlet syntax (Verb-Noun)
- ❌ Forgetting to convert SecureString for passwords

---

## 🎯 HIGH-YIELD TOPICS

### Most Likely to Appear

**Memory:**
- LRU calculations (show table!)
- Logical/physical address bits
- Segment table lookups
- Page fault handling steps

**Server:**
- PowerShell cmdlets (New-, Get-, Set-, Remove-)
- GPO application order (LSDOU)
- Active Directory structure
- FSMO roles

**Processes:**
- Process state diagram
- Context switch triggers
- Scheduling algorithms

**Calculations:**
- log₂ conversions
- Address translations
- Page table sizes

---

## 🧮 CALCULATION TEMPLATES

### Address Bits Template
```
Given: X pages/frames, Y words per page/frame

Step 1: Total space = X × Y
Step 2: Total bits = log₂(Total space)
Step 3: Page/Frame bits = log₂(X)
Step 4: Offset bits = log₂(Y)
Verify: Step 3 + Step 4 = Step 2 ✓
```

### Segment Translation Template
```
Given: Logical (segment, offset)
Segment table: Base, Length

Step 1: Check validity: offset < length?
        If NO → SEGMENTATION FAULT
        If YES → Continue
Step 2: Physical = Base + Offset
```

### LRU Template
```
For each reference:
1. Check if page in frames
   - YES: No fault, update access time
   - NO: Page fault, go to step 2
2. Find empty frame OR frame with oldest access
3. Load page, update access time
4. Mark as fault
```

---

## 🔑 KEY TERMS TO DEFINE

**Swapping:** Process copied between memory and disk
**Relocation register:** Base physical address
**Limit register:** Process address space size
**Fixed partition:** Each contains exactly ONE process
**Fastest IPC:** Shared Memory
**Namespace init:** Process P1 (PID 1) reaps orphans
**unshare():** Creates namespace for caller (except PID - affects children)

---

## 💡 POWERSHELL PATTERNS

### Create Password
```powershell
$Pass = ConvertTo-SecureString "Password123" -AsPlainText -Force
```

### Loop to Create Users
```powershell
for ($i = 1; $i -le 10; $i++) {
    New-ADUser -Name "User$i" -SamAccountName "user$i" -Enabled $true
}
```

### Filter Patterns
```powershell
-Filter *                           # All
-Filter {Enabled -eq $false}        # Disabled
-Filter {Department -eq "IT"}       # Specific value
-Filter {Name -like "Test*"}        # Wildcard
```

### Pipeline Pattern
```powershell
Get-ADUser -Filter * | Where-Object {condition} | Set-ADUser -Property Value
```

---

## ✏️ LAST MINUTE CHECKLIST

Before the exam:
- [ ] Memorized all formulas
- [ ] Practiced LRU calculations
- [ ] Know LSDOU order
- [ ] Can write basic PowerShell cmdlets
- [ ] Understand FSMO roles
- [ ] Know page fault steps (4)
- [ ] Can differentiate Type 1/Type 2
- [ ] Remember: Segments=External frag, Paging=Internal frag
- [ ] Remember: Shared Memory = fastest IPC
- [ ] Remember: IVT in low memory

---

**🌟 YOU'VE GOT THIS! STAY CALM AND THINK CLEARLY! 🌟**

**Pro Tips:**
- Start with questions you're 100% confident about
- Show all steps in calculations (partial credit!)
- If stuck, move on and come back
- Use process of elimination for multiple choice
- Read questions carefully (especially "NOT" questions)
- Check your work if time permits

**GOOD LUCK! 🎓✨**
