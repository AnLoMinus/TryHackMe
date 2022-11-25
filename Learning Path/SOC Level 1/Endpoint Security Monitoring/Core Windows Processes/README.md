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

---

## Task 4  System > smss.exe

---

## Task 5  csrss.exe

---

## Task 6  wininit.exe

---

## Task 7  wininit.exe > services.exe

---

## Task 8  wininit.exe > services.exe > svchost.exe

---

## Task 9  lsass.exe

---

## Task 10  winlogon.exe

---

## Task 11  explorer.exe

---

## Task 12  Conclusion
