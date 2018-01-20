---
layout: post
title:  "Virtual Memory in Linux"
date:   2018-01-19 12:21:59 -0500
categories: Linux Virtual Memory
---
{% include toc.html %}

# Physical Memory
### Single Address Space
- All processes and OS share same memory space
- Older Systems and Modern Micro-controllers use this architecture.
- Problems:
    - No memory protection (memory stomping)
    - Need memory management- to keep each process memory separate
- Ok for small systems which might not run many processes

# Virtual memory
## Principles
- Mapping Virtual Address Space to Physical address space (which can be physical RAM or hardware devices)
- Mapping is done on H/w, i.e. Zero penalty for already mapped addresses
- Advantages
   - Memory Protection (Kernel is separate)
   - Memory can be moved
   - Can be swapped to HDD
   - Memory Sharing is easier (Physical RAM mapped to multiple processes)

## Memory Management Unit (MMU)
![MMU]({{ "/assets/linux-virtual-memory/MMU.png" | absolute_url }})
- MMU is H/W implementing Virtual Memory
   - often part of physical CPU itself
- Transparently handles memory access from load/ store instructions
- Maps Virtual memory to physical Memory
- Also handles permissions
  - Page Fault if no mapping or permission error
- Consults TLB

## Translation Look Aside Buffer (TLB)
- List of mappings from Virtual Memory to physical address Space
- MMU Consults TLB
  - If Virtual Address is present in TLB, MMU looks up physical address.
  - If not, MMU generates page Fault -> interrupting CPU

## Page Faults
-  Page Faults are CPU Exceptions
-  Happens when
  - Virtual Address is not mapped
  - process has insufficient permissions
  - virtual address is valid, but swapped out (pure software condition, CPU doesn't know about this)

# Virtual Memory in Linux
![Brief overview]({{ "/assets/linux-virtual-memory/abstract.png" | absolute_url }})
- a 32 bit processor yields 4GB address space.
- Virtual address space is split into kernel space and user space. Default: 1 GB and 3 GB. (PAGE_OFFSET)
- if processor is 64 bit, there is sufficient virtual space to be mapped, the split is high enough.
- Virtual address space is split into 3 address spaces
  - Kernel Logical address
  - Kernel Virtual address
  - User Virtual Address

## Kernel Logical address
![Linux Kernel Memory]({{ "/assets/linux-virtual-memory/LinuxMemory.png" | absolute_url }})
- Starts at physical address 0
- Easy to convert between physical and Virtual
- Allocated by `kmalloc()`
- This memory can't be swapped about
- Bottom part of Kernel virtual memory
- Physically Contiguous memory locations
  - Appropriate for DMA

## Kernel Virtual address
- Addresses above Kernel Logical Address block.
- Non-Contiguous Physically
- Allocated by `vmalloc()`
- For Systems with Large Physical memory (above 1GB), This area is smaller

## User Virtual Address
- Below PAGE_OFFSET
- Each process has it's own mapping
  - Memory is non-Contiguous
  - Memory may be swapped out
  - Only used portions of RAM are mapped
- At context switch, memory map is changed.
  - Overhead..but Truth of life for multiprocessing os.

## MMU Implementation
- Operates on basic unit of pages (page size varies by architecture, mostly 4k)
- Physical Memory is split into page-size, page-aligned blocks called frames

## Page Faults Cause
- Process tries to access unmapped region
- Kernel sees this regularly, coz
  - TLB is limited, a process may need more mappings
  - Page faults peak during context switch time
    - All current TLB entries are invalidated

## Lazy Allocation
- Optimisation
- When a process asks to allocate page (or memory)
  - Kernel makes notes of this in its Page table, Doesn't actually allocate.
  - Returns to user process
  - User process tries to access newly allocated, PAGE FAULT
  - page fault handler action:
    - Kernel checks if mapping is valid (present in page table)
    - Allocates physical frame
    - Updates TLB with new mappings
    - Returns to user process

## Page Table
- TLB is limited (as low as 20 sometimes)
- A Process can need more mappings
- All mappings are stored in Page Table in Memory.
- If TLB-unmapped Region is accessed, PAGE FAULT
  - Page Fault handler actions:
    1. Find appropriate mapping in page table
    2. Removes Existing TLB entry
    3. Create TLB entry
    4. Return to User Process

## Swapping
-  When memory utilisation is high
  - Kernel swaps frames to disk
- if swapped frames are needed again
  - CPU page fault when Accessing
  - Page fault handler actions:
    1. check page table, see swapped out
    2. Put process to sleep
    3. Copy frame from disk to RAM
    4. Fix page table entry
    5. Wake process

Watch this video which explains swapping.
<iframe width="560" height="315" src="https://www.youtube.com/embed/EWwfMM2AW9g?start=41.8&end=42.2" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

# Source:
This notes are based on following sources:
  - [Introduction to Memory Management in Linux by Alan Ott]( https://www.youtube.com/watch?time_continue=772&v=EWwfMM2AW9g)
