---
layout: post
title:  "Facebook 2: Systems Round!"
date:   2018-01-25 12:21:59 -0500
categories: facebook systems
---

**Company** | Facebook
**Position** | Intern - Production Engineer
**Interviewer** | :star::star::star::star:/5
**Time** | 45 Minutes
**Rounds** | 2
**Offer**  | Maybe
**NDA** | No

{% include toc.html %}
## Preparation
2 Weeks of in-depth preparation of Linux +  Operating Systems + Networks.
[Linux SysAdmin Github Academy](https://github.com/chassing/linux-sysadmin-interview-questions)  was my primary guide.
 - My solutions can be found in this [fork](https://github.com/HotSushi/linux-sysadmin-interview-questions)

## What happens when a linux system boots?
My Answer:
  - BIOS chip checks hardware is ok
  - BIOS Chip loads first sector (Bootloader) from primary HD
  - Bootloader like grub knows locations of other operating system
  - Bootloader starts kernel code
  - Kernel Code checks hardware again and starts init
  - init starts daemons
  - 1 daemon is xserver responsible for GUI
  - GUI shows login

What I missed:
  - How File system is loaded?
  - What about `/`  directory?
  - What about `/boot`?
  - How EXT4 gets loaded? what if drivers not there?
  - What about Swap partition and primary partition?

## What happens when `ls -l foo*` is run?
My Answer:
  - Terminal is a bash program
  - Bash program is listening for inputs
  - Every time I press a keyboard button, hardware interrupt to cpu
  - CPU switches to kernel mode, reads keyboard input, serves process
  - bash displays keyboard input
  - when enter is pressed, bash starts something called as Fork-Execute-Wait Cycle
  - bash forks and creates replica
  - I talked about switching into kernel mode too.
  - replica runs `exec` to switch into `ls`
  - ls takes command line arguments
  - ls runs and prints and exits
  - returns and bash which was waiting now continues

What I missed:
  - `foo*` is actually passed into shell globbing program
    - Example ./\*cat\*
    - it will linearly pass arguments such as cat netcate.sh tcat.sh
    - *Follow Up*: What if arguments are too long?
      - my answer `xargs` but not able to convince
      - second answer `find -name 'foo*' -exec rm {} +`


## What is Fork-Execute-Wait Cycle?
My Answer:
  - Pattern where Fork creates replica to the point PC is also same
    - *Follow up* How Parent, child process know which ones they are?
      - fork returns non zero PID for Parent
      - returns zero PID for child
    - *Follow up* Can Fork Fail?
      - Yes, PIDs are limited
      - If a parent process keeps creating zombie children PIDs will run out.
      - how to handle that?
        - returns negative
  - Exec
    - replica runs `exec` to switch into `ls`
      - exec loads executable mostly in `ELF` format.
      - Loads into memory which has typical `C program` format of growing stack from above, growing heap from below, initialised and uninitialised variables etc.
  - Wait
    - Waits for child process to finish
    - Successfully or unsuccessfully is determined by return value

What I missed:
  - Not Actually missed, but told irrelevant information about throwing exceptions in C language (goto).

## What are Zombie Processes?
My Answer:
  - child processes which have finished executing
  - Parents are still running
    - *Follow up* How to limit no of max processes that can be created?
    - *Follow up* Heard of `ulimit`?
      - yes, explained

What I missed:
  - Didn't know about limiting max no of processes.


## Explain VMSTAT output
  - showed me vmstat output and asked me whether I knew what the output was.
    - First I said no, but realized I knew about it.. so I interrupted and told
  -  Explained to me each column, but given my feeble memory I already forgot about them by the time he finished.
  - I didn't do so well here.
  - What is interruptible vs uninterruptible sleep?
    - Answered (hardware interrupt for uninterruptible vs signal for interruptible)
  - Two modes of CPU are IO mode and Computational mode.
  - What is wait time? is it good?
    - CPU sleeping.
    - Not good, because precious CPU cycles are wasted.
  - There were other questions but didn't do so good here.

## My Wifi Went Down during the interview :scream:
 - Of all the possible times for the Wifi to not work.... it had to be now.
 - Switched immediately to hotspot on my phone
 - Lost 4 minutes
 - Apologized frantically

## My Summary:
- Did OK.
- May not be positive.
- But definitely not negative.
- PS. preparing for this interview was really useful
  - It was a good refresher for Operating Systems and networks.
  - Learned new things about linux, for instance `nohup` instead of `tmux`
  - Thanks Spandan Chowdhury (The networks guru) for explaining to me all the fundamentals in Networks.
