# [Windows Internals](https://tryhackme.com/room/windowsinternals)
> #### Learn and understand the fundamentals of how Windows operates at its core.

Task 1  Introduction
Task 2  Processes
Task 3  Threads
Task 4  Virtual Memory
Task 5  Dynamic Link Libraries
Task 6  Portable Executable Format
Task 7  Interacting with Windows Internals
Task 8  Conclusion

---

## Task 1  Introduction

Operating systems have a lot more technology and architecture behind them than we may see at first. In this room, we will be observing the Windows operating systems and common internal components.


### Learning Objectives
- Understand and interact with Windows processes and their underlying technologies.
- Learn about core file formats and how they are used.
- Interact with Windows internals and understand how the Windows kernel operates.

With Windows machines making up a majority of corporate infrastructure, red teams need to understand Windows internals and how they can be (ab)used. The red team can (ab)use Windows to aid in evasion and exploitation when crafting offensive tools or exploits.

Before beginning this room, familiarize yourself with basic Windows usage and functionality. Basic programming knowledge in C++ and PowerShell is also recommended but not required.

We have provided a base Windows machine with the files needed to complete this room. You can access the machine in-browser or through RDP using the credentials below.

Machine IP: 10.10.113.167
Username: THM-Attacker
Password: Tryhackme!

This is going to be a lot of information.
Please buckle your seatbelts and locate your nearest fire extinguisher.


---

## Task 2  Processes

A process maintains and represents the execution of a program; an application can contain one or more processes. A process has many components that it gets broken down into to be stored and interacted with. The Microsoft docs break down these other components, "Each process provides the resources needed to execute a program. A process has a virtual address space, executable code, open handles to system objects, a security context, a unique process identifier, environment variables, a priority class, minimum and maximum working set sizes, and at least one thread of execution." This information may seem intimidating, but this room aims to make this concept a little less complex.

As previously mentioned, processes are created from the execution of an application. Processes are core to how Windows functions, most functionality of Windows can be encompassed as an application and has a corresponding process. Below are a few examples of default applications that start processes.

- MsMpEng (Microsoft Defender)
- wininit (keyboard and mouse)
- lsass (credential storage)

Attackers can target processes to evade detections and hide malware as legitimate processes. Below is a small list of potential attack vectors attackers could employ against processes,

- Process Injection ([TI055](https://attack.mitre.org/techniques/T1055/))
- Process Hollowing ([TI055.012](https://attack.mitre.org/techniques/T1055/012/))
- Process Masquerading ([TI055.013](https://attack.mitre.org/techniques/T1055/013/))

Processes have many components; they can be split into key characteristics that we can use to describe processes at a high level. The table below describes each critical component of processes and their purpose.

Process Component | Purpose
:---:|:---:
Private Virtual Address Space | Virtual memory addresses that the process is allocated.
Executable Program | Defines code and data stored in the virtual address space.
Open Handles | Defines handles to system resources accessible to the process.
Security Context | The access token defines the user, security groups, privileges, and other security information.
Process ID  | Unique numerical identifier of the process.
Threads | Section of a process scheduled for execution.

We can also explain a process at a lower level as it resides in the virtual address space. The table and diagram below depict what a process looks like in memory.


Component | Purpose
:---:|:---:
Code | Code to be executed by the process.
Global Variables | Stored variables.
Process Heap | Defines the heap where data is stored.
Process Resources | Defines further resources of the process.
Environment Block | Data structure to define process information.

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5e73cca6ec4fcf1309f2df86/room-content/66320022b6b57f3c40e135d66de3c1d9.png)

This information is excellent to have when we get deeper into exploiting and abusing the underlying technologies, but they are still very abstract. We can make the process tangible by observing them in the Windows Task Manager. The task manager can report on many components and information about a process. Below is a table with a brief list of essential process details.

Value/Component | Purpose | Example
:---:|:---:|:---:
Name | Define the name of the process, typically inherited from the application | conhost.exe
PID | Unique numerical value to identify the process | 7408
Status | Determines how the process is running (running, suspended, etc.) | Running
User name | User that initiated the process. Can denote privilege of the process | SYSTEM

These are what you would interact with the most as an end-user or manipulate as an attacker.

There are multiple utilities available that make observing processes easier; including [`Process Hacker 2`](https://github.com/processhacker/processhacker), [`Process Explorer`](https://docs.microsoft.com/en-us/sysinternals/downloads/process-explorer), and [`Procmon`](https://docs.microsoft.com/en-us/sysinternals/downloads/procmon).

Processes are at the core of most internal Windows components. The following tasks will extend the information about processes and how they're used in Windows.


---

## Task 3  Threads

---

## Task 4  Virtual Memory

---

## Task 5  Dynamic Link Libraries

---

## Task 6  Portable Executable Format

---

## Task 7  Interacting with Windows Internals

---

## Task 8  Conclusion

---
