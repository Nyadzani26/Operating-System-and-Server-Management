# OPERATING SYSTEMS: ANSWER KEY
## Comprehensive Solutions to Practice Test

**TOTAL MARKS:** 100

---

## SECTION A ANSWERS [45 MARKS]

### QUESTION 1: Comparison (12 Marks)

**1.1** Segmentation vs Paging Table [10]

| Aspect | Segmentation | Paging |
|--------|--------------|--------|
| **Division** | Logical units (code, data, stack) | Fixed-size blocks |
| **Size** | Variable (different sizes) | Fixed (all pages/frames same size) |
| **Calculation/Formula** | Physical Address = Base + Offset (if Offset < Length) | Physical Address = (Frame# × PageSize) + Offset |
| **Fragmentation Type** | External fragmentation | Internal fragmentation (last page only) |
| **User Visibility** | Visible to programmer | Transparent to programmer |

**1.2** LRU vs LFU [2]

| Aspect | LRU (Least Recently Used) | LFU (Least Frequently Used) |
|--------|---------------------------|----------------------------|
| **Replacement Criterion** | Replace page not used for longest time | Replace page with lowest reference count |
| **Implementation Complexity** | High (needs timestamps/stack) | Medium (needs counters) |

---

### QUESTION 2: Completion (10 Marks)

1. **registers, cache, main memory (RAM)** [1]

2. **logical (or virtual)** [1]

3. **Swapping** [1]

4. **Base + Offset (if Offset < Length)** [1]

5. **LRU (Least Recently Used)** [1]

6. **deadlock** [1]

7. **shared memory** [1]

8. **thread** [1]

9. **low** [1]

10. **page number, offset** (or page number, displacement) [1]

---

### QUESTION 3: Multiple Choice (10 Marks)

1. **b) A blocking system call** [1]
   - Always causes context switch because process must wait for I/O; another process must run.

2. **c) Orphan processes in the namespace will be reaped by P1** [1]
   - P1 is the init process for the namespace; it reaps all orphans in that namespace.

3. **c) It can result in involuntary context switches** [1]
   - When time quantum expires, process is preempted (involuntary context switch).

4. **b) Internal fragmentation only** [1]
   - Paging causes internal fragmentation in the last page of a process; no external fragmentation.

5. **b) fork()** [1]
   - fork() creates a new child process by duplicating the parent.

6. **b) Program counter** [1]
   - Program counter (PC) holds the address of the next instruction to execute.

7. **d) PID of child process** [1]
   - Stack contains function parameters, return addresses, and local variables, not child PIDs.

8. **b) Uniprogramming systems** [1]
   - Systems allowing only one process at a time are called uniprogramming systems.

9. **c) OPT** [1]
   - OPT (Optimal/Belady's) algorithm is theoretically optimal but requires future knowledge.

10. **c) Waits for child process termination** [1]
    - Parent uses wait() to wait for child termination and retrieve exit status.

---

### QUESTION 4: True or False (8 Marks)

**1. TRUE** [2]
**Explanation:** The unshare() system call creates a new namespace and places the calling process in it. However, for PID namespaces specifically, the calling process remains in the old namespace, and the new namespace takes effect for child processes created afterward.

**2. FALSE** [2]
**Explanation:** Round-Robin scheduling with a time quantum REQUIRES hardware timer interrupt support. Without timer interrupts, the OS cannot enforce the time quantum and preempt processes, making the policy impossible to implement efficiently.

**3. TRUE** [2]
**Explanation:** Type 1 hypervisors run directly on hardware (bare metal) without a host OS, providing better performance, lower latency, and reduced overhead compared to Type 2 hypervisors that run on top of a host OS.

**4. FALSE** [2]
**Explanation:** In segmentation, if the offset exceeds the segment length (limit), it's an INVALID address that causes a segmentation fault. The address is only valid if offset < length.

---

### QUESTION 5: Identification and Diagrams (5 Marks)

**5.1** Basic Process State Diagram [3]

```
         ┌──────────┐
         │   New    │
         └────┬─────┘
              │ admitted
              ↓
         ┌────────────┐     timeout      ┌─────────────┐
    ┌───→│   Ready    │←─────────────────│   Running   │────┐
    │    └────────────┘                  └──────┬──────┘    │
    │           ↑          dispatch             │           │
    │           │     ←─────────────────────────┘           │
    │           │                                            │
    │           │                                            │ exit
    │           │ I/O or event                               ↓
    │           │ completion                           ┌──────────┐
    │           │                                      │Terminated│
    │      ┌────┴──────┐                              └──────────┘
    └──────│  Waiting  │
           │ (Blocked) │
           └───────────┘
              ↑      │
              │ wait │
              │ event│
              └──────┘
```

**5.2** Process States with Two Suspended States [2]

```
      New → Ready ⇄ Running → Terminated
              ↕       ↕
           Waiting   (timeout/dispatch/wait)
              ↕
      Suspended Ready ⇄ Suspended Waiting
      
Transitions:
- Ready → Suspended Ready (swap out)
- Suspended Ready → Ready (swap in)
- Waiting → Suspended Waiting (swap out)
- Suspended Waiting → Suspended Ready (event occurs while swapped)
- Suspended Waiting → Waiting (swap in)
```

---

## SECTION B ANSWERS [35 MARKS]

### QUESTION 1: Critical Thinking / Scenario (25 Marks)

**1.1** Type 1 vs Type 2 Hypervisors [6]

**Type 1 Hypervisor (Bare Metal):**
```
┌─────────────┬─────────────┬─────────────┐
│   Guest OS  │   Guest OS  │   Guest OS  │
├─────────────┴─────────────┴─────────────┤
│           Hypervisor (Type 1)           │
├─────────────────────────────────────────┤
│          Physical Hardware              │
└─────────────────────────────────────────┘
```
- Runs directly on hardware
- No host OS layer
- Examples: VMware ESXi, Hyper-V, KVM

**Type 2 Hypervisor (Hosted):**
```
┌─────────────┬─────────────┬─────────────┐
│   Guest OS  │   Guest OS  │   Guest OS  │
├─────────────┴─────────────┴─────────────┤
│           Hypervisor (Type 2)           │
├─────────────────────────────────────────┤
│              Host OS                    │
├─────────────────────────────────────────┤
│          Physical Hardware              │
└─────────────────────────────────────────┘
```
- Runs as application on host OS
- Additional OS layer
- Examples: VirtualBox, VMware Workstation

**1.2** Recommendation for Production Banking [4]

**Recommendation: Type 1 Hypervisor**

**Reasons:**
1. **Performance:** Direct hardware access provides native-level performance without host OS overhead—critical for banking transactions requiring fast processing.

2. **Security:** Smaller attack surface (no host OS to compromise). Banking data requires maximum security; Type 1's minimal code base reduces vulnerability.

3. **Latency:** Lower latency due to fewer abstraction layers. Banking applications are latency-sensitive—customers expect instant transaction responses.

4. **Reliability:** Better stability for 24/7 operation. Production banking cannot tolerate host OS crashes affecting guest VMs.

**1.3** Page Fault Handling Steps [4]

1. **Trap to OS:** Hardware detects page fault and generates interrupt, transferring control to OS page fault handler.

2. **Find Page Location:** OS checks page table to locate page on secondary storage (disk). Validates that reference was legal.

3. **Find Free Frame:** OS finds a free frame in physical memory. If no free frames, select victim page using replacement algorithm (FIFO, LRU, etc.) and swap it out if modified.

4. **Load Page:** OS initiates disk I/O to read page from disk into the free frame. Process is blocked during I/O.

**1.4** LAPIC vs I/O APIC [4]

**LAPIC (Local APIC):**
- One per CPU core
- Receives interrupts destined for that core
- Handles inter-processor interrupts (IPIs)
- Manages local timer interrupts

**I/O APIC:**
- Centralized controller for I/O device interrupts
- Routes interrupts from devices to appropriate LAPIC
- Supports up to 256 interrupt lines

**Why APIC is Better for Multi-Processor Servers:**
1. **More IRQ Lines:** Traditional systems limited to 16 IRQs; APIC supports 256, eliminating IRQ sharing conflicts.
2. **Better Distribution:** I/O APIC can intelligently route interrupts to least-busy CPU, improving load balancing.
3. **Scalability:** Designed for multi-processor systems; each core has dedicated LAPIC.
4. **Performance:** Reduced interrupt latency and better concurrent interrupt handling.

**1.5** Shared Memory IPC [5]

**How Shared Memory Works:**
- One process creates a shared memory segment in RAM
- Other processes attach to the same segment
- All processes can read/write directly to shared memory
- No kernel mediation needed after initial setup

**Why It's Fastest:**
- **No copying:** Data isn't copied between processes—all access same memory location
- **No kernel calls:** After setup, processes access memory directly without system calls
- **Minimal overhead:** Just memory read/write operations, as fast as accessing any variable

**Disadvantage:**
Requires explicit synchronization (semaphores, mutexes) to prevent race conditions. Without proper synchronization, concurrent writes can corrupt data.

**1.6** fork() System Call [2]

**What Happens:**
- fork() creates a child process by duplicating the parent
- Child gets copy of parent's memory, file descriptors, and registers
- Both processes continue execution after fork()
- Parent receives child's PID as return value; child receives 0

**Determining Child Termination:**
Parent calls `wait()` system call, which:
- Blocks parent until a child terminates
- Returns child's PID and exit status
- Reaps zombie child process (cleans up process table entry)

---

### QUESTION 2: Memory Management Scenario (10 Marks)

**Reference String:** 7, 0, 1, 2, 0, 3, 0, 4, 2, 3, 0, 3, 2  
**Frames:** 3

**2.1 FIFO Algorithm** [3]

```
Reference | Frame 1 | Frame 2 | Frame 3 | Fault?
    7     |    7    |    -    |    -    |  Yes
    0     |    7    |    0    |    -    |  Yes
    1     |    7    |    0    |    1    |  Yes
    2     |    2    |    0    |    1    |  Yes (replace 7)
    0     |    2    |    0    |    1    |  No (hit)
    3     |    2    |    3    |    1    |  Yes (replace 0)
    0     |    2    |    3    |    0    |  Yes (replace 1)
    4     |    4    |    3    |    0    |  Yes (replace 2)
    2     |    4    |    2    |    0    |  Yes (replace 3)
    3     |    4    |    2    |    3    |  Yes (replace 0)
    0     |    0    |    2    |    3    |  Yes (replace 4)
    3     |    0    |    2    |    3    |  No (hit)
    2     |    0    |    2    |    3    |  No (hit)
```

**FIFO Page Faults: 10**

**2.1 LRU Algorithm** [3]

```
Reference | Frame 1 | Frame 2 | Frame 3 | Fault? | Notes
    7     |    7    |    -    |    -    |  Yes   | 
    0     |    7    |    0    |    -    |  Yes   | 
    1     |    7    |    0    |    1    |  Yes   | 
    2     |    2    |    0    |    1    |  Yes   | Replace 7 (LRU)
    0     |    2    |    0    |    1    |  No    | Hit, update 0
    3     |    2    |    0    |    3    |  Yes   | Replace 1 (LRU)
    0     |    2    |    0    |    3    |  No    | Hit, update 0
    4     |    4    |    0    |    3    |  Yes   | Replace 2 (LRU)
    2     |    4    |    2    |    3    |  Yes   | Replace 0 (LRU)
    3     |    4    |    2    |    3    |  No    | Hit, update 3
    0     |    0    |    2    |    3    |  Yes   | Replace 4 (LRU)
    3     |    0    |    2    |    3    |  No    | Hit, update 3
    2     |    0    |    2    |    3    |  No    | Hit, update 2
```

**LRU Page Faults: 8**

**2.2** Performance Comparison [2]

**LRU performed better** (8 faults vs 10 faults for FIFO).

**Why:** LRU considers recency of use—it keeps frequently/recently accessed pages in memory based on temporal locality principle (pages used recently are likely to be used again soon). FIFO blindly replaces the oldest page regardless of usage, which can evict pages that are still being actively used.

**2.3** OPT Algorithm [2]

**OPT (Optimal/Belady's Algorithm):**
- Replaces the page that won't be used for the longest period in the future
- Guarantees the fewest possible page faults (theoretically optimal)

**Why It Can't Be Implemented:**
Requires knowledge of future page references, which is impossible in practice. The OS cannot predict which pages a program will access in the future. OPT is used only as a theoretical benchmark to evaluate other algorithms.

---

## SECTION C ANSWERS [20 MARKS]

### QUESTION 1: Address Translation Calculations (10 Marks)

**Given:**
- Logical address space: 128 pages × 2048 words per page
- Physical memory: 64 frames

**a) Logical Address Bits** [3]

```
Step 1: Calculate page size
Page Size = 2048 words = 2^11 words
Offset Bits = log₂(2048) = 11 bits

Step 2: Calculate number of pages
Number of Pages = 128 = 2^7 pages
Page Number Bits = log₂(128) = 7 bits

Step 3: Total logical address bits
Logical Address Bits = Page Number Bits + Offset Bits
                     = 7 + 11 = 18 bits
```

**Answer: 18 bits**

**b) Physical Address Bits** [3]

```
Step 1: Frame size (same as page size)
Frame Size = 2048 words = 2^11 words
Offset Bits = 11 bits (same as logical)

Step 2: Calculate number of frames
Number of Frames = 64 = 2^6 frames
Frame Number Bits = log₂(64) = 6 bits

Step 3: Total physical address bits
Physical Address Bits = Frame Number Bits + Offset Bits
                      = 6 + 11 = 17 bits
```

**Answer: 17 bits**

**c) Page Number Bits** [2]

```
Number of Pages = 128 = 2^7
Page Number Bits = log₂(128) = 7 bits
```

**Answer: 7 bits**

**d) Offset Bits** [2]

```
Page Size = 2048 words = 2^11
Offset Bits = log₂(2048) = 11 bits
```

**Answer: 11 bits**

---

### QUESTION 2: Segment Addressing (10 Marks)

**Segment Table:**
| Segment | Base | Length |
|---------|------|--------|
| 0 | 400 | 500 |
| 1 | 1500 | 250 |
| 2 | 200 | 150 |
| 3 | 2500 | 800 |
| 4 | 3200 | 100 |

**Formula:** Physical Address = Base + Offset (if Offset < Length)

**Solutions:** [1 mark each = 10 marks]

**a) (0, 250)**
- Check: 250 < 500? YES ✓
- Physical Address = 400 + 250 = **650**

**b) (1, 100)**
- Check: 100 < 250? YES ✓
- Physical Address = 1500 + 100 = **1600**

**c) (2, 200)**
- Check: 200 < 150? NO ✗
- **INVALID - Segmentation Fault** (offset exceeds segment length)

**d) (3, 450)**
- Check: 450 < 800? YES ✓
- Physical Address = 2500 + 450 = **2950**

**e) (4, 99)**
- Check: 99 < 100? YES ✓
- Physical Address = 3200 + 99 = **3299**

**f) (1, 300)**
- Check: 300 < 250? NO ✗
- **INVALID - Segmentation Fault**

**g) (0, 499)**
- Check: 499 < 500? YES ✓
- Physical Address = 400 + 499 = **899**

**h) (3, 800)**
- Check: 800 < 800? NO ✗
- **INVALID - Segmentation Fault** (offset equals length, must be less than)

**i) (2, 75)**
- Check: 75 < 150? YES ✓
- Physical Address = 200 + 75 = **275**

**j) (4, 50)**
- Check: 50 < 100? YES ✓
- Physical Address = 3200 + 50 = **3250**

---

## BONUS QUESTION ANSWERS

**Bonus 1: Belady's Anomaly** [5]

**Belady's Anomaly:** Counterintuitive situation where increasing the number of frames can actually INCREASE the number of page faults (not decrease as expected).

**Example:**
```
Reference String: 1, 2, 3, 4, 1, 2, 5, 1, 2, 3, 4, 5

With 3 frames (FIFO): 9 page faults
With 4 frames (FIFO): 10 page faults ← MORE faults with MORE frames!
```

This anomaly occurs only with certain algorithms (like FIFO), not with stack-based algorithms (like LRU).

**Bonus 2: Deadlock Conditions** [4]

**Four Necessary Conditions (ALL must hold):**

1. **Mutual Exclusion:** At least one resource must be non-shareable (only one process can use at a time).

2. **Hold and Wait:** Process holds at least one resource while waiting to acquire additional resources held by others.

3. **No Preemption:** Resources cannot be forcibly taken from processes; must be voluntarily released.

4. **Circular Wait:** Circular chain of processes, each waiting for a resource held by the next in the chain.

**Bonus 3: Interrupt Handling Process** [6]

```
1. Device signals interrupt → IRQ line activated
                 ↓
2. Interrupt controller → Sends interrupt # to CPU
                 ↓
3. CPU finishes current instruction (atomic)
                 ↓
4. CPU checks interrupt priority & masks
                 ↓
5. CPU looks up handler in IDT using interrupt #
                 ↓
6. CPU saves context (registers, PC, flags) to stack
                 ↓
7. CPU loads handler address from IDT → CS:EIP
                 ↓
8. Interrupt handler executes (device-specific code)
                 ↓
9. Handler sends EOI (End Of Interrupt) to controller
                 ↓
10. IRET instruction → Restore context from stack
                 ↓
11. CPU resumes interrupted process
```

**Bonus 4: Page Table Calculation** [5]

**Given:**
- Virtual address: 20-bit page number, 12-bit offset
- Page table entries: 4 bytes each

**a) Page Size:**
```
Offset bits = 12
Page Size = 2^12 bytes = 4096 bytes = 4 KB
```

**b) Page Table Size:**
```
Number of Pages = 2^20 pages (from 20-bit page number)
Entry Size = 4 bytes
Page Table Size = 2^20 × 4 bytes = 2^22 bytes = 4,194,304 bytes = 4 MB
```

---

## SUMMARY OF KEY FORMULAS

**Memory Addressing:**
```
Logical Address Bits = log₂(Pages × Page_Size)
Physical Address Bits = log₂(Frames × Frame_Size)
Page/Frame Number Bits = log₂(Number_of_Pages/Frames)
Offset Bits = log₂(Page_Size)
```

**Segmentation:**
```
Physical Address = Base + Offset
Valid only if: Offset < Length
```

**Page Table:**
```
Page Table Size = Number_of_Pages × Entry_Size
```

---

**END OF ANSWER KEY**

**Study Tips:**
- Practice calculations until automatic
- Draw diagrams for process states and hypervisors
- Memorize page fault handling steps
- Understand WHY algorithms perform differently
- Always show your working in calculations

**Good luck with your exam! 🎓**
