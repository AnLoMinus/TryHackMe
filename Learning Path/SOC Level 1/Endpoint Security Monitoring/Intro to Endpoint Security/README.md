![image](https://user-images.githubusercontent.com/51442719/203473462-c6f47503-0f68-431a-8fc7-de367030c589.png)

# [Intro to Endpoint Security](#)

![image](https://user-images.githubusercontent.com/51442719/203473302-466c112b-45b8-47a2-8f71-851f149867c1.png)

### Learn about fundamentals, methodology, and tooling for endpoint security monitoring.

---

- [Task 1  Room Introduction](#)
- [Task 2  Endpoint Security Fundamentals](#)
- [Task 3  Endpoint Logging and Monitoring](#)
- [Task 4  Endpoint Log Analysis](#)
- [Task 5  Conclusion](#)

---

## Task 1  Room Introduction

In this room, we will introduce the fundamentals of endpoint security monitoring, essential tools, and high-level methodology. This room gives an overview of determining a malicious activity from an endpoint and mapping its related events.

To start with, we will tackle the following topics to build a stepping stone on how to deal with Endpoint Security Monitoring.

- Endpoint Security Fundamentals
- Endpoint Logging and Monitoring
- Endpoint Log Analysis

At the end of this room, we will have a threat simulation wherein you need to investigate and remediate the infected machines. This activity may require you first to understand the fundamentals of endpoint security monitoring to complete it.

Now, let’s deep-dive into the basics of Endpoint Security!


---

## Task 2  Endpoint Security Fundamentals

### Core Windows Processes

Before we deal with learning how to deep-dive into endpoint logs, we need first to learn the fundamentals of how the Windows Operating System works. Without prior knowledge, differentiating an outlier from a haystack of events could be problematic. 

To learn more about Core Windows Processes, a built-in Windows tool named Task Manager may aid us in understanding the underlying processes inside a Windows machine. 

Task Manager is a built-in GUI-based Windows utility that allows users to see what is running on the Windows system. It also provides information on resource usage, such as how much each process utilizes CPU and memory. When a program is not responding, the Task Manager is used to terminate the process.

![image](https://user-images.githubusercontent.com/51442719/203473642-5953dfe2-a02b-4297-95aa-c286439ef9fc.png)

A Task Manager provides some of the Core Windows Processes running in the background. Below is a summary of running processes that are considered normal behaviour.

> `Note`: ">" symbol represents a parent-child relationship. `System (Parent) > smss.exe (Child)`

- System
- System > smss.exe
- csrss.exe
- wininit.exe
- wininit.exe > services.exe
- wininit.exe > services.exe > svchost.exe
- lsass.exe
- winlogon.exe
- explorer.exe

In addition, the processes with no depiction of a parent-child relationship should not have a Parent Process under normal circumstances, except for the System process, which should only have System Idle Process (0) as its parent process.

You may refer to the [Core Windows Processes Room](https://tryhackme.com/room/btwindowsinternals) to learn more about this topic.
 
### Sysinternals

With the prior knowledge of Core Windows Processes, we can now proceed to discuss the available toolset for analyzing running artefacts in the backend of a Windows machine.

The Sysinternals tools are a compilation of over 70+ Windows-based tools. Each of the tools falls into one of the following categories:

- File and Disk Utilities
- Networking Utilities
- Process Utilities
- Security Utilities
- System Information
- Miscellaneous

We will introduce two of the most used Sysinternals tools for endpoint investigation for this task.

- TCPView - Networking Utility tool.
- Process Explorer - Process Utility tool.

### TCPView

"TCPView is a Windows program that will show you detailed listings of all TCP and UDP endpoints on your system, including the local and remote addresses and state of TCP connections. On Windows Server 2008, Vista, and XP, TCPView also reports the name of the process that owns the endpoint. TCPView provides a more informative and conveniently presented subset of the Netstat program that ships with Windows. The TCPView download includes Tcpvcon, a command-line version with the same functionality." (official definition)

![image](https://user-images.githubusercontent.com/51442719/203473829-1ffb550e-b55a-429f-9ea0-3f3483524ad3.png)

As shown above, every connection initiated by a process is listed by the tool, which may aid in correlating the network events executed concurrently.

### Process Explorer

"The Process Explorer display consists of two sub-windows. The top window always shows a list of the currently active processes, including the names of their owning accounts, whereas the information displayed in the bottom window depends on the mode that Process Explorer is in: if it is in handle mode, you'll see the handles that the process selected in the top window has opened; if Process Explorer is in DLL mode you'll see the DLLs and memory-mapped files that the process has loaded." (official definition)

![image](https://user-images.githubusercontent.com/51442719/203473852-dde58bcc-bb19-4ca4-baa3-5c9119133529.png)

Process Explorer enables you to inspect the details of a running process, such as:

- Associated services
- Invoked network traffic
- Handles such as files or directories opened
- DLLs and memory-mapped files loaded

To learn more about Sysinternals, you may refer to the [Sysinternals Room](https://tryhackme.com/room/btsysinternalssg).
 

---

## Task 3  Endpoint Logging and Monitoring

---

## Task 4  Endpoint Log Analysis

---

## Task 5  Conclusion

