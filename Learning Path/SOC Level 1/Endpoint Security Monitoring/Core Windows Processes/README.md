![image](https://user-images.githubusercontent.com/51442719/203886298-d62bbe20-8948-4e78-9637-b2cc17663326.png)

# [Core Windows Processes](https://tryhackme.com/room/btwindowsinternals)

![image](https://user-images.githubusercontent.com/51442719/203886288-581917c8-f4dd-4d1f-9cf1-c0fb188faa2f.png)

### Explore the core processes within a Windows operating system and understand what normal behaviour is. This foundational knowledge will help you identify malicious processes running on an endpoint!

- [Task 1  Introduction]()
- [Task 2  Task Manager]()
- [Task 3  System]()
- [Task 4  System > smss.exe]()
- [Task 5  csrss.exe]()
- [Task 6  wininit.exe]()
- [Task 7  wininit.exe > services.exe]()
- [Task 8  wininit.exe > services.exe > svchost.exe]()
- [Task 9  lsass.exe]()
- [Task 10  winlogon.exe]()
- [Task 11  explorer.exe]()
- [Task 12  Conclusion]()

---

## Task 1  Introduction

In this room, we will explore the core processes within a Windows system. This room aims to help you know and understand what normal behaviour within a Windows operating system is. This foundational knowledge will help you identify malicious processes running on an endpoint. 

The Windows operating system is the most used in the world (whether people like it or not), and the majority of its users don't fully understand its interworkings. Users are simply content that it works, like anything complex, such as a car. It starts, and you can drive from point A to point B. Now regarding computers, if they can surf the web, read/answer emails, shop, listen to music, and watch movies, all is well. It took a long time for users to grasp the need for antivirus programs fully. Only when one of their essential everyday computer functions is disrupted is when antivirus matter. Antivirus was enough over 5-7 years ago (rough estimate).

Time changes everything. Malware and attacks have evolved, and antivirus is no longer enough. Antivirus has struggled to keep up, solely based on how it is designed to catch evil. 

Today antivirus is just one solution within the layered defensive approach. New security tools, such as EDR (Endpoint Detection and Response), have been created because antiviruses cannot catch every malicious binary and process running on the endpoint. 

But guess what? Even with these new tools, it is still not 100% effective. Attackers can still bypass the defences running on the endpoint. This is where we come in. Whether you're a Security Analyst, SOC Analyst, Detection Engineer, or Threat Hunter, if one of the tools alerts us of a suspicious binary or process, we must investigate and decide on a course of action. Knowing the expected behaviour of the systems we have to defend, a Windows system, in this case, we can infer if the binary or process is benign or evil. 

The machine attached to this task will start in a split-screen view. In case the VM is not visible, use the blue Show Split View button at the top-right of the page.

If you want to access the virtual machine via RDP, use the credentials below. 

- Machine IP: MACHINE_IP
- User: `administrator`
- Password: `letmein123!`

> `Note`: The virtual machine may take up to 3 minutes to load.

---

## Task 2  Task Manager

### Task Manager 
is a built-in GUI-based Windows utility that allows users to see what is running on the Windows system. It also provides information on resource usage, such as how much each process utilizes CPU and memory. When a program is not responding, Task Manager is used to end (kill) the process. 

We'll give a brief overview if you're unfamiliar with Task Manager.

To open Task Manager, right-click the Taskbar. When the new window appears, select `Task Manager` (as shown below).

![image](https://user-images.githubusercontent.com/51442719/203887643-84068de3-a053-4a31-be31-036ee3b3b123.png)

If you don't have any explicitly opened apps, you should see the same message as shown below.

![image](https://user-images.githubusercontent.com/51442719/203887658-65e562ca-847a-4cb6-8a55-6308026bda35.png)

Weird. Not seeing much, eh? Within a Windows system, many processes are running. Click on `More details`. 

![image](https://user-images.githubusercontent.com/51442719/203887709-16d0f093-2cc5-48fd-8590-8257426c9497.png)

Ok, now we're getting somewhere. Notice the five tabs within Task Manager. By default, the current tab is `Processes`.

> `Note`: If you're running Task Manager on your Windows machine, you might see additional tabs. 

As shown above, you may notice the processes are categorized as follows: `Apps` and `Background processes`. Another category that is not visible in the above image is `Windows processes`. 

The columns are very minimal. The columns Name, Status, CPU, and Memory are the only ones visible. To view more columns, right-click on any column header to open more options. 

![image](https://user-images.githubusercontent.com/51442719/203887825-666e4e7b-971c-4a74-a131-320745ef5c5b.png)

![image](https://user-images.githubusercontent.com/51442719/203887836-a63ff192-92db-4533-8c34-74ae9fde9613.png)

The view looks a little better. Let's briefly go over each column (excluding Name, of course): 

- Type - Each process falls into 1 of 3 categories (Apps, Background process, or Windows process).
- Publisher - Think of this column as the name of the author of the program/file.
- PID - This is known as the process identifier number. Windows assigns a unique process identifier each time a program starts. If the same program has multiple running processes, each will have its unique process identifier (PID).
- Process name - This is the file name of the process. In the above image, the file name for Task Manager is Taskmrg.exe. 
- Command line - The full command used to launch the process. 
- CPU - The amount of CPU (processing power) the process uses.
- Memory - The amount of physical working memory utilized by the process. 

Task Manager is a utility you should be comfortable using, whether you're troubleshooting or performing analysis on the endpoint. 

Let's move to the `Details` tab. This view provides some core processes that will be discussed in this room. Sort the PID column so that the PIDs are in ascending order.

![image](https://user-images.githubusercontent.com/51442719/203887907-c2006550-e31c-4ba1-801e-2825440d4bb5.png)

Add some additional columns to see more information about these processes. Good columns to add are `Image path` name and `Command line`.

These two columns can quickly alert an analyst of any outliers with a given process. In the below image, PID 384 is paired with a process named svchost.exe, a Windows process, but if the Image path name or Command line is not what it's expected to be, then we can perform a deeper analysis of this process. 

![image](https://user-images.githubusercontent.com/51442719/203887968-028e85fd-b105-4da7-9ada-f55cf325b0cc.png)

Of course, you can add as many columns as you wish, but adding the columns that would be pertinent to your current task is recommended. 

Task Manager is a powerful built-in Windows utility but lacks certain important information when analyzing processes, such as parent process information. It is another key column when identifying outliers. Back to svchost.exe, if the parent process for PID 384 is not services.exe, this will warrant further analysis. 

To further prove this point, where is services.exe? 

![image](https://user-images.githubusercontent.com/51442719/203888010-eef8e362-2b35-488d-ad18-40ed92ebdc88.png)


Based on the above image, the PID for services.exe is 632. But wait, one of the svchost.exe processes has a PID of 384. How did svchost.exe start before services.exe? Well, it didn't. Task Manager doesn't show a Parent-Child process view. That is where other utilities, such as Process Hacker and Process Explorer, come to the rescue.

#### Process Hacker

![image](https://user-images.githubusercontent.com/51442719/203888064-e433b19c-7502-4da0-9bea-7ea0b99bfb58.png)

#### Process Explorer

![image](https://user-images.githubusercontent.com/51442719/203888090-b5b99dc0-cb05-4fa6-aaed-eb4a214d9302.png)

Moving forward, we'll use Process Hacker and Process Explorer instead of Task Manager to obtain information about each Windows process. 

As always, it's encouraged that you inspect and familiarize yourself with all information available within Task Manager. It's a built-in utility that is available in every Windows system. You might find yourself in a situation where you can't bring your tools to the fight and rely on the tools native to the system.

Aside from Task Manager, it would be best if you also familiarize yourself with the command-line equivalent of obtaining information about the running processes on a Windows system: `tasklist`, `Get-Process` or `ps` (PowerShell), and `wmic`.

---

## Task 3  System

The first Windows process on the list is System. It was mentioned in a previous section that a PID for any given process is assigned at random, but that is not the case for the System process. The PID for System is always 4. What does this process do exactly?

The official definition from Windows Internals 6th Edition:

"The System process (process ID 4) is the home for a special kind of thread that runs only in kernel mode a kernel-mode system thread. System threads have all the attributes and contexts of regular user-mode threads (such as a hardware context, priority, and so on) but are different in that they run only in kernel-mode executing code loaded in system space, whether that is in Ntoskrnl.exe or in any other loaded device driver. In addition, system threads don't have a user process address space and hence must allocate any dynamic storage from operating system memory heaps, such as a paged or nonpaged pool."

What is user mode? Kernel-mode? Visit the following [link](https://docs.microsoft.com/en-us/windows-hardware/drivers/gettingstarted/user-mode-and-kernel-mode) to understand each of these.

Now, what is normal behaviour for this process? Let's use Process Explorer and view the properties of the System.

![image](https://user-images.githubusercontent.com/51442719/203888650-86f59c6d-723c-487a-9779-bbe8d08d43a6.png)

- Image Path:  N/A
- Parent Process:  None
- Number of Instances:  One
- User Account:  Local System
- Start Time:  At boot time

The information is slightly different if we view the System properties using Process Hacker. 

![image](https://user-images.githubusercontent.com/51442719/203888673-ade7a40a-b17a-47b5-a2ab-e9285953f221.png)

- `Image Path`: C:\Windows\system32\ntoskrnl.exe (NT OS Kernel)
- `Parent Process`: System Idle Process (0)

Technically this is correct. You may notice that Process Hacker confirms this is legit (Verified) Microsoft Windows. 

What is unusual behaviour for this process?
- A parent process (aside from System Idle Process (0))
- Multiple instances of System. (Should only be one instance) 
- A different PID. (Remember that the PID will always be PID 4)
- Not running in Session 0

---

## Task 4  System > smss.exe

The next process is smss.exe (Session Manager Subsystem). This process, also known as the Windows Session Manager, is responsible for creating new sessions. It is the first user-mode process started by the kernel.

This process starts the kernel and user modes of the Windows subsystem (you can read more about the NT Architecture [here](https://en.wikipedia.org/wiki/Architecture_of_Windows_NT)). This subsystem includes win32k.sys (kernel mode), winsrv.dll (user mode), and csrss.exe (user mode). 

Smss.exe starts csrss.exe (Windows subsystem) and wininit.exe in Session 0, an isolated Windows session for the operating system, and csrss.exe and winlogon.exe for Session 1, which is the user session. The first child instance creates child instances in new sessions, done by smss.exe copying itself into the new session and self-terminating. You can read more about this process [here](https://en.wikipedia.org/wiki/Session_Manager_Subsystem).

Session 0 (csrss.exe & wininit.exe)

![image](https://user-images.githubusercontent.com/51442719/203888991-cfed26d3-8a43-4f11-8aeb-664c40ee39c6.png)

![image](https://user-images.githubusercontent.com/51442719/203889001-edfff677-b9c4-4757-bb8a-4bf79b1680a8.png)

Session 1 (csrss.exe & winlogon.exe)

![image](https://user-images.githubusercontent.com/51442719/203889026-8c4f2485-f0e1-4b0f-8132-b4a9a1515dce.png)

![image](https://user-images.githubusercontent.com/51442719/203889034-40e700a4-7d60-414a-9e0f-ba3a68705162.png)

 Any other subsystem listed in the `Required` value of `HKLM\System\CurrentControlSet\Control\Session Manager\Subsystems` is also launched.

![image](https://user-images.githubusercontent.com/51442719/203889079-ebd3a1cf-8a05-4a7c-8393-6b6a702f9b22.png)

SMSS is also responsible for creating environment variables, virtual memory paging files and starts winlogon.exe (the Windows Logon Manager).

What is normal?

![image](https://user-images.githubusercontent.com/51442719/203889115-f4e657a7-aafa-4f1a-97c1-f4e850d7b267.png)

- `Image Path`:  %SystemRoot%\System32\smss.exe
- `Parent Process`:  System
- `Number of Instances`:  One master instance and child instance per session. The child instance exits after creating the session.
- `User Account`:  Local System
- `Start Time`:  Within seconds of boot time for the master instance

What is unusual?
- A different parent process other than System (4)
- The image path is different from C:\Windows\System32
- More than one running process. (children self-terminate and exit after each new session)
- The running User is not the SYSTEM user
- Unexpected registry entries for Subsystem


---

## Task 5  csrss.exe

As mentioned in the previous section, csrss.exe (Client Server Runtime Process) is the user-mode side of the Windows subsystem. This process is always running and is critical to system operation. If this process is terminated by chance, it will result in system failure. This process is responsible for the Win32 console window and process thread creation and deletion. For each instance, csrsrv.dll, basesrv.dll, and winsrv.dll are loaded (along with others). 

This process is also responsible for making the Windows API available to other processes, mapping drive letters, and handling the Windows shutdown process. You can read more about this process here.

Note: Recall that csrss.exe and winlogon.exe are called from smss.exe at startup for Session 1. 

What is normal?

Session 0 (PID 392)

![image](https://user-images.githubusercontent.com/51442719/203889398-ef6b10c8-45c4-42c6-b6e8-0a4fac3c6bb9.png)

Session 1 (PID 512)

![image](https://user-images.githubusercontent.com/51442719/203889428-8391024c-c7dc-4061-bbc5-f87491ed1e37.png)

Notice what is shown for the parent process for these two processes. Remember, these processes are spawned by smss.exe, which self-terminates itself.  

- `Image Path`:  %SystemRoot%\System32\csrss.exe
- `Parent Process`:  Created by an instance of smss.exe
- `Number of Instances`:  Two or more
- `User Account`:  Local System
- `Start Time`:  Within seconds of boot time for the first two instances (for Session 0 and 1). Start times for additional instances occur as new sessions are created, although only Sessions 0 and 1 are often created.

What is unusual?
- An actual parent process. (smss.exe calls this process and self-terminates)
- Image file path other than C:\Windows\System32
- Subtle misspellings to hide rogue processes masquerading as csrss.exe in plain sight
- The user is not the SYSTEM user.


---

## Task 6  wininit.exe

The Windows Initialization Process, wininit.exe, is responsible for launching services.exe (Service Control Manager), lsass.exe (Local Security Authority), and lsaiso.exe within Session 0. It is another critical Windows process that runs in the background, along with its child processes. 

![image](https://user-images.githubusercontent.com/51442719/204154788-f36dae26-e6e0-4981-bda6-b04b939742cc.png)

> `Note`: lsaiso.exe is a process associated with Credential Guard and KeyGuard. You will only see this process if Credential Guard is enabled. 

What is normal?

![image](https://user-images.githubusercontent.com/51442719/204154803-171b02b1-859f-4b9c-89c6-1bb943c8ff7d.png)

- Image Path:  %SystemRoot%\System32\wininit.exe
- Parent Process:  Created by an instance of smss.exe
- Number of Instances:  One
- User Account:  Local System
- Start Time:  Within seconds of boot time

What is unusual?
- An actual parent process. (smss.exe calls this process and self-terminates)
- Image file path other than C:\Windows\System32
- Subtle misspellings to hide rogue processes in plain sight
- Multiple running instances
- Not running as SYSTEM

---

## Task 7  wininit.exe > services.exe

The next process is the Service Control Manager (SCM) or services.exe. Its primary responsibility is to handle system services: loading services, interacting with services and starting or ending services. It maintains a database that can be queried using a Windows built-in utility, sc.exe. 

cmd.exe
```cmd
C:\Users\Administrator> sc.exe
DESCRIPTION:
        SC is a command line program used for communicating with the
        Service Control Manager and services.
USAGE:
        sc <server> [command] [service name] <option1> <option2>...
```
- Information regarding services is stored in the registry, `HKLM\System\CurrentControlSet\Services`. 

![image](https://user-images.githubusercontent.com/51442719/204154866-02167030-8752-411c-9d85-9704b77c51f3.png)

This process also loads device drivers marked as auto-start into memory. 

When a user logs into a machine successfully, this process is responsible for setting the value of the Last Known Good control set (Last Known Good Configuration), `HKLM\System\Select\LastKnownGood`, to that of the CurrentControlSet. 

![image](https://user-images.githubusercontent.com/51442719/204154880-2220cff6-d1bb-44ac-ba23-f28a5e41b4c7.png)

This process is the parent to several other key processes: svchost.exe, spoolsv.exe, msmpeng.exe, and dllhost.exe, to name a few. You can read more about this process [here](https://en.wikipedia.org/wiki/Service_Control_Manager).

![image](https://user-images.githubusercontent.com/51442719/204154896-e20e0926-080c-44f9-974b-8b70602921b9.png)

What is normal?

![image](https://user-images.githubusercontent.com/51442719/204154902-a6dc6d60-84d0-450e-9d2b-106c740136dd.png)

![image](https://user-images.githubusercontent.com/51442719/204154908-cd2f06f3-975d-4362-a09f-28b5758ea523.png)

- Image Path:  %SystemRoot%\System32\services.exe
- Parent Process:  wininit.exe
- Number of Instances:  One
- User Account:  Local System
- Start Time:  Within seconds of boot time

What is unusual?
- A parent process other than wininit.exe
- Image file path other than C:\Windows\System32
- Subtle misspellings to hide rogue processes in plain sight
- Multiple running instances
- Not running as SYSTEM


---

## Task 8  wininit.exe > services.exe > svchost.exe

The Service Host (Host Process for Windows Services), or svchost.exe, is responsible for hosting and managing Windows services. 

![image](https://user-images.githubusercontent.com/51442719/204155411-0d317830-72ef-4a8a-961d-19aeb43003bf.png)

The services running in this process are implemented as DLLs. The DLL to implement is stored in the registry for the service under the `Parameters` subkey in `ServiceDLL`. The full path is `HKLM\SYSTEM\CurrentControlSet\Services\SERVICE NAME\Parameters`.

The example below is the ServiceDLL value for the Dcomlaunch service.

![image](https://user-images.githubusercontent.com/51442719/204155440-6c5d20e7-9704-4005-959f-1d9eb4fecc43.png)

To view this information from within Process Hacker, right-click the svchost.exe process. In this case, it will be PID 748.

![image](https://user-images.githubusercontent.com/51442719/204155447-49f618a5-2412-44ab-bba6-a40578f06951.png)

Right-click the service and select Properties. Look at Service DLL.

![image](https://user-images.githubusercontent.com/51442719/204155450-5e63dac0-839a-4be7-8962-655e074ccd12.png)

From the above screenshot, the Binary Path is listed.

Also, notice how it is structured. There is a key identifier in the binary path, and that identifier is `-k` . This is how a legitimate svchost.exe process is called. 

The -k parameter is for grouping similar services to share the same process. This concept was based on the OS design and implemented to reduce resource consumption. Starting from Windows 10 Version 1703, services grouped into host processes changed. On machines running more than 3.5 GB of memory, each service will run its own process. You can read more about this process [here](https://en.wikipedia.org/wiki/Svchost.exe).

Back to the key identifier (-k) from the binary path, in the above screen, the -k value is Dcomlaunch. Other services are running with the same binary path in the virtual machine attached to this room.

![image](https://user-images.githubusercontent.com/51442719/204155473-16a87fa2-2f1d-489a-b320-55f8f484bbd2.png)

Each will have a different value for ServiceDLL. Let's take LSM as an example and inspect the value for ServiceDLL.

![image](https://user-images.githubusercontent.com/51442719/204155484-da96f6c9-51e5-42a0-a775-89e5d9633a5f.png)

![image](https://user-images.githubusercontent.com/51442719/204155487-8c73ea65-5691-461d-9a67-7f27141af947.png)

Since svchost.exe will always have multiple running processes on any Windows system, this process has been a target for malicious use. Adversaries create malware to masquerade as this process and try to hide amongst the legitimate svchost.exe processes. They can name the malware svchost.exe or misspell it slightly, such as scvhost.exe. By doing so, the intention is to go under the radar. Another tactic is to install/call a malicious service (DLL).  

Extra reading - [Hexacorn Blog](https://www.hexacorn.com/blog/2015/12/18/the-typographical-and-homomorphic-abuse-of-svchost-exe-and-other-popular-file-names/)

What is normal?

![image](https://user-images.githubusercontent.com/51442719/204155502-149fc7ae-8071-4b39-8328-213e99fa64f9.png)

- Image Path: %SystemRoot%\System32\svchost.exe
- Parent Process: services.exe
- Number of Instances: Many
- User Account: Varies (SYSTEM, Network Service, Local Service) depending on the svchost.exe instance. In Windows 10, some instances run as the logged-in user.
- Start Time: Typically within seconds of boot time. Other instances of svchost.exe can be started after boot.

What is unusual?
- A parent process other than services.exe
- Image file path other than C:\Windows\System32
- Subtle misspellings to hide rogue processes in plain sight
- The absence of the -k parameter


---

## Task 9  lsass.exe

Per Wikipedia, "Local Security Authority Subsystem Service (LSASS) is a process in Microsoft Windows operating systems that is responsible for enforcing the security policy on the system. It verifies users logging on to a Windows computer or server, handles password changes, and creates access tokens. It also writes to the Windows Security Log."

It creates security tokens for SAM (Security Account Manager), AD (Active Directory), and NETLOGON. It uses authentication packages specified in `HKLM\System\CurrentControlSet\Control\Lsa`.

![image](https://user-images.githubusercontent.com/51442719/204155549-9e96fc17-d16e-4f4b-8c00-c6fa9638263f.png)

Lsass.exe is another process adversaries target. Common tools such as mimikatz are used to dump credentials, or adversaries mimic this process to hide in plain sight. Again, they do this by either naming their malware by this process name or simply misspelling the malware slightly. 

Extra reading: [How LSASS is maliciously used and additional features that Microsoft has put into place to prevent these attacks](https://yungchou.wordpress.com/2016/03/14/an-introduction-of-windows-10-credential-guard/).

What is normal?

![image](https://user-images.githubusercontent.com/51442719/204155564-3403406e-807e-4be4-bb91-7f649c37f7f8.png)


- Image Path:  %SystemRoot%\System32\lsass.exe
- Parent Process:  wininit.exe
- Number of Instances:  One
- User Account:  Local System
- Start Time:  Within seconds of boot time

What is unusual?
- A parent process other than wininit.exe
- Image file path other than C:\Windows\System32
- Subtle misspellings to hide rogue processes in plain sight
- Multiple running instances
- Not running as SYSTEM

---

## Task 10  winlogon.exe

The Windows Logon, winlogon.exe, is responsible for handling the Secure Attention Sequence (SAS). It is the ALT+CTRL+DELETE key combination users press to enter their username & password. 

This process is also responsible for loading the user profile. It loads the user's NTUSER.DAT into HKCU, and userinit.exe loads the user's shell. Read more about this process [here](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-2000-server/cc939862(v=technet.10)?redirectedfrom=MSDN).

![image](https://user-images.githubusercontent.com/51442719/204155601-61ba0527-19d8-4808-afa0-03ffc9b887c6.png)

It is also responsible for locking the screen and running the user's screensaver, among other functions. You can read more about this process here.

Remember from earlier sections, smss.exe launches this process along with a copy of csrss.exe within Session 1. 

![image](https://user-images.githubusercontent.com/51442719/204155618-ca86d3b9-3bb9-43e4-ae93-a444e169012b.png)

What is normal?

![image](https://user-images.githubusercontent.com/51442719/204155626-1f76ee9f-a56e-445f-8df6-394595d5da00.png)

![image](https://user-images.githubusercontent.com/51442719/204155627-f18c1808-7819-4705-9703-cd0e2a873471.png)

- Image Path:  %SystemRoot%\System32\winlogon.exe
- Parent Process:  Created by an instance of smss.exe that exits, so analysis tools usually do not provide the parent process name.
- Number of Instances:  One or more
- User Account:  Local System
- Start Time:  Within seconds of boot time for the first instance (for Session 1). Additional instances occur as new sessions are created, typically through Remote Desktop or Fast User Switching logons.

What is unusual?
- An actual parent process. (smss.exe calls this process and self-terminates)
- Image file path other than C:\Windows\System32
- Subtle misspellings to hide rogue processes in plain sight
- Not running as SYSTEM
- Shell value in the registry other than explorer.exe

---

## Task 11  explorer.exe

The last process we'll look at is Windows Explorer, explorer.exe. This process gives the user access to their folders and files. It also provides functionality for other features, such as the Start Menu and Taskbar.

As mentioned previously, the Winlogon process runs userinit.exe, which launches the value in `HKLM\Software\Microsoft\Windows NT\CurrentVersion\Winlogon\Shell`. Userinit.exe exits after spawning explorer.exe. Because of this, the parent process is non-existent. 

There will be many child processes for explorer.exe.

![image](https://user-images.githubusercontent.com/51442719/204155664-4c3c3e51-5b5e-4513-84b5-abf248a54b8a.png)

What is normal?

![image](https://user-images.githubusercontent.com/51442719/204155673-05e021be-2114-44e0-a659-c898a0a8ec06.png)

- Image Path:  %SystemRoot%\explorer.exe
- Parent Process:  Created by userinit.exe and exits
- Number of Instances:  One or more per interactively logged-in user
- User Account:  Logged-in user(s)
- Start Time:  First instance when the first interactive user logon session begins

What is unusual?
- An actual parent process. (userinit.exe calls this process and exits)
- Image file path other than C:\Windows
- Running as an unknown user
- Subtle misspellings to hide rogue processes in plain sight
- Outbound TCP/IP connections

![image](https://user-images.githubusercontent.com/51442719/204155690-f8256e46-2cbc-4f95-b336-a1d86df8f159.png)

---

## Task 12  Conclusion


Understanding how the Windows operating system functions as a defender is vital. The Windows processes discussed in this room are core processes, and understanding how they usually operate can aid a defender in identifying unusual activity on the endpoint. 

With the introduction of Windows 10, new processes have been added to the list of core processes to know and understand normal behaviour.

Earlier it was mentioned that if Credential Guard is enabled on the endpoint, an additional process will be running, which will be a child process to wininit.exe, and that process is lsaiso.exe. This process works with lsass.exe to enhance password protection on the endpoint. 

Other processes with Windows 10 are RuntimeBroker.exe and taskhostw.exe (formerly taskhost.exe and taskhostex.exe). Please research these processes and any other processes you might be curious about to understand their purpose and their normal functionality. 

The information for this room is derived from multiple sources.

- https://www.threathunting.se/tag/windows-process/
- https://www.sans.org/security-resources/posters/hunt-evil/165/download
- https://docs.microsoft.com/en-us/sysinternals/resources/windows-internals

Other links are provided throughout the room. Reading them at your own leisure to further your foundation and understanding of the core Windows processes is encouraged.

---
---

- https://www.cyb3rm3.com/btwindowsinternals
