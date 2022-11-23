![image](https://user-images.githubusercontent.com/51442719/203473462-c6f47503-0f68-431a-8fc7-de367030c589.png)

# [Intro to Endpoint Security](#)

![image](https://user-images.githubusercontent.com/51442719/203473302-466c112b-45b8-47a2-8f71-851f149867c1.png)

### Learn about fundamentals, methodology, and tooling for endpoint security monitoring.

---

- `EDR` - Endpoint detection and response 

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

From the previous task, we have learned basic knowledge about the Windows Operating system﻿ in terms of baseline processes and essential tools to analyze events and artefacts running on the machine. However, this only limits us from observing real-time events. With this, we will introduce the importance of endpoint logging, which enables us to audit significant events across different endpoints, collect and aggregate them for searching capabilities, and better automate the detection of anomalies.

### Windows Event Logs

The Windows Event Logs are not text files that can be viewed using a text editor. However, the raw data can be translated into XML using the Windows API. The events in these log files are stored in a proprietary binary format with a .evt or .evtx extension. The log files with the .evtx file extension typically reside in `C:\Windows\System32\winevt\Logs`.

There are three main ways of accessing these event logs within a Windows system:

- Event Viewer (GUI-based application)
- Wevtutil.exe (command-line tool)
- Get-WinEvent (PowerShell cmdlet)

An example image of logs viewed using the Event Viewer tool is shown below.

![image](https://user-images.githubusercontent.com/51442719/203474171-4e144edd-a733-4f31-b9d2-00ae6948c6a6.png)

You may refer to the [Windows Event Logs Room](https://tryhackme.com/room/windowseventlogs) to learn more about Windows Event Logs. 

### Sysmon

Sysmon, a tool used to monitor and log events on Windows, is commonly used by enterprises as part of their monitoring and logging solutions. As part of the Windows Sysinternals package, Sysmon is similar to Windows Event Logs with further detail and granular control.

Sysmon gathers detailed and high-quality logs as well as event tracing that assists in identifying anomalies in your environment. It is commonly used with a security information and event management (SIEM) system or other log parsing solutions that aggregate, filter, and visualize events. 

Lastly, Sysmon includes 27 types of Event IDs, all of which can be used within the required configuration file to specify how the events should be handled and analyzed. An excellent example of a configuration file auditing different Event IDs created by SwiftOnSecurity is linked [here](https://github.com/SwiftOnSecurity/sysmon-config).

The image below shows a sample set of Sysmon logs viewed using an Event Viewer.

![image](https://user-images.githubusercontent.com/51442719/203474243-5a7a93fe-39d4-4392-8f83-b0ecbbf9a404.png)

To learn more about Sysmon, you may refer to the [Sysmon Room](https://tryhackme.com/room/sysmon).

### OSQuery

Osquery is an open-source tool created by Facebook. With Osquery, Security Analysts, Incident Responders, and Threat Hunters can query an endpoint (or multiple endpoints) using SQL syntax. Osquery can be installed on various platforms: Windows, Linux, macOS, and FreeBSD.

To interact with the Osquery interactive console/shell, open CMD (or PowerShell) and run `osqueryi`. You'll know that you've successfully entered into the interactive shell by the new command prompt.

##### cmd.exe
```cmd
C:\Users\Administrator\> osqueryi
Using a virtual database. Need help, type 'help'
osquery> 
```

A sample use case for using OSQuery is to list important process information by its process name. 

##### osqueryi
```cmd
osquery> select pid,name,path from processes where name='lsass.exe';
+-----+-----------+-------------------------------+
| pid | name      | path                          |
+-----+-----------+-------------------------------+
| 748 | lsass.exe | C:\Windows\System32\lsass.exe |
+-----+-----------+-------------------------------+
osquery> 
```
Osquery only allows you to query events inside the machine. But with Kolide Fleet, you can query multiple endpoints from the Kolide Fleet UI instead of using Osquery locally to query an endpoint. A sample of Kolide Fleet in action below shows a result of a query listing the machines with the `lsass` process running.

![image](https://user-images.githubusercontent.com/51442719/203474392-9d0c8b36-f9db-4b35-8111-769049ec57db.png)

To learn more about OSQuery, you may refer to the [OSQuery Room](https://tryhackme.com/room/osqueryf8). 

### Wazuh

﻿Wazuh is an open-source, freely available, and extensive EDR solution, which Security Engineers can deploy in all scales of environments.

Wazuh operates on a management and agent model where a dedicated manager device is responsible for managing agents installed on the devices you'd like to monitor.

As mentioned, Wazuh is an EDR; let's briefly run through what an EDR is. Endpoint detection and response (EDR) are tools and applications that monitor devices for an activity that could indicate a threat or security breach. These tools and applications have features that include:

- Auditing a device for common vulnerabilities
- Proactively monitoring a device for suspicious activity such as unauthorized logins, brute-force attacks, or privilege escalations.
- Visualizing complex data and events into neat and trendy graphs
- Recording a device's normal operating behaviour to help with detecting anomalies

A sample view of how Wazuh works is shown below.

![image](https://user-images.githubusercontent.com/51442719/203474554-7f16bfce-0e79-4935-a5ec-1e37634ed4df.png)

To experience Wazuh in action, you may refer to the [Wazuh Room](https://tryhackme.com/room/wazuhct).


---

## Task 4  Endpoint Log Analysis

---

## Task 5  Conclusion

