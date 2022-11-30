![image](https://user-images.githubusercontent.com/51442719/204398767-eb06eb84-23bb-4b42-803f-02173e7849e5.png)

# [Sysinternals](https://tryhackme.com/room/btsysinternalssg)
### Learn to use the Sysinternals tools to analyze Windows systems or applications.

![image](https://user-images.githubusercontent.com/51442719/204398752-b4eae1e9-7271-44d4-9cfc-e463e219a123.png)

---

- [Task 1  Introduction](#)
- [Task 2  Install the Sysinternals Suite](#)
- [Task 3  Using Sysinternals Live](#)
- [Task 4  File and Disk Utilities](#)
- [Task 5  Networking Utilities](#)
- [Task 6  Process Utilities](#)
- [Task 7  Security Utilities](#)
- [Task 8  System Information](#)
- [Task 9  Miscellaneous](#)
- [Task 10  Conclusion](#)

---

## Task 1  Introduction


What are the tools known as Sysinternals?

The Sysinternals tools is a compilation of over 70+ Windows-based tools. Each of the tools falls into one of the following categories:

- File and Disk Utilities
- Networking Utilities
- Process Utilities
- Security Utilities
- System Information
- Miscellaneous

The Sysinternals tools and its website (sysinternals.com) were created by Mark Russinovich in the late '90s, along Bryce Cogswell under the company Wininternals Software.
In 2006, Microsoft acquired Wininternals Software, and Mark Russinovich joined Microsoft. Today he is the CTO of Microsoft Azure. 

Mark Russinovich made headlines when he reported that Sony embedded rootkits into their music CDs back in 2005. This discovery was made known thanks to one of the Sysinternals tools he was testing. You can read more about that [here](https://www.virusbulletin.com/virusbulletin/2005/12/inside-sony-s-rootkit).  

He also discovered in 2006 that Symantec was using rootkit-like technology. You can read more about that [here](https://www.zdnet.com/article/symantec-confesses-to-using-rootkit-technology/). 

The Sysinternals tools are extremely popular among IT professionals who manage Windows systems. These tools are so popular that even red teamers and adversaries alike use them. Throughout this room, I'll note which tools MITRE has identified to have been used by adversaries. 

The goal of this room is to introduce you to a handful of Sysinternals tools with the hopes that you will expand on this knowledge with your own research and curiosity.

Hopefully, you can add Sysinternals to your toolkit, as many already have. 

If you want to access the virtual machine via [Remote Desktop](https://www.cyberark.com/resources/threat-research-blog/explain-like-i-m-5-remote-desktop-protocol-rdp), use the credentials below. 

- Machine IP: MACHINE_IP
- User: administrator
- Password: letmein123!

![image](https://user-images.githubusercontent.com/51442719/204398552-349850af-ba1f-4054-bd39-79220e0a8747.png)

Accept the Certificate when prompted, and you should be logged into the remote system now.

> `Note`: The virtual machine may take up to 3 minutes to load.
> 
---

## Task 2  Install the Sysinternals Suite

Time to get our hands dirty with Sysinternals.

The Sysinternals tool(s) can be downloaded and run from the local system, or the tool(s) can be run from the web. 

Regarding local install/run, you can download the entire suite or just the tool(s) you need.

If you wish to download a tool or two but not the entire suite, you can navigate to the Sysinternals Utilities Index page, https://docs.microsoft.com/en-us/sysinternals/downloads/, and download the tool(s). If you know which tool you want to download, then this is fine. The tools are listed in alphabetical order are not separated by categories.

![image](https://user-images.githubusercontent.com/51442719/204402028-cc35b41e-efd0-429f-ab6f-90dbe4654a24.png)

Alternatively, you can use the category links to find and download the tool(s). This route is better since there are so many tools you can focus on all the tools of interest instead of the entire index.

For example, let's say you need tools to inspect Windows processes; then, you can navigate to the Process Utilities page, https://docs.microsoft.com/en-us/sysinternals/downloads/process-utilities/, for all the tools that fall under this category.

![image](https://user-images.githubusercontent.com/51442719/204402062-426af026-b953-43e8-8d61-834e1f046376.png)

Notice that you are conveniently supplied with a brief explanation for each tool. 

Lastly, you can do the same from the Sysinternals Live URL, https://live.sysinternals.com/. This is the same URL to use if you wish to run the tool from the web. We will look at how to accomplish this in the next section.

If you chose to download from this page, it is similar to the Sysinternals Utilities Index page. The tools are listed in alphabetical order and are not separated by categories.

If you wish to download the Sysinternals Suite, you can download the zip file from [here](https://docs.microsoft.com/en-us/sysinternals/downloads/sysinternals-suite).

The suite has a select number of Sysinternal tools. See below for a rundown of the tools included in the suite.

![image](https://user-images.githubusercontent.com/51442719/204402129-d376e653-fb50-4fea-869f-ae92380c3b8c.png)

After you download the zip file, you need to extract the files. After the files are extracted, the extra step, which is by choice, is to add the folder path to the environment variables. By doing so, you can launch the tools via the command line without navigating to the directory the tools reside in. 

Environment Variables can be edited from System Properties.

The System Properties can be launched via the command line by running `sysdm.cpl`. Click on the `Advanced` tab. 

![image](https://user-images.githubusercontent.com/51442719/204402183-a95edf04-a64e-4f29-a055-18bcd4051812.png)

Select `Path` under `System Variables` and select Edit... then OK.

![image](https://user-images.githubusercontent.com/51442719/204402240-585e136c-11bf-4755-8134-89b8ef3a9ec2.png)

In the next screen select `New` and enter the folder path where the Sysinternals Suite was extracted to. Press OK to confirm the changes.

![image](https://user-images.githubusercontent.com/51442719/204402278-846263c5-43f7-4c8d-9d6a-3b0a2e0df4ca.png)

Open a new command prompt (elevated) to confirm that the Sysinternals Suite can be executed from any location.

![image](https://user-images.githubusercontent.com/51442719/204402287-a5270dbe-4245-458c-b1c4-ba538a646d34.png)

A local copy of the Sysinternals Suite is located in `C:\Tools\Sysint`. 

Alternatively, a PowerShell module can download and install all of the Sysinternals tools. 

- PowerShell command: `Download-SysInternalsTools C:\Tools\Sysint`

Now let's look at how to run the Sysinternals tools from the web. 

---

## Task 3  Using Sysinternals Live

Per the Sysinternals website, 
"Sysinternals Live is a service that enables you to execute Sysinternals tools directly from the Web without hunting for and manually downloading them.
Simply enter a tool's Sysinternals Live path into Windows Explorer or a command prompt as:

- `live.sysinternals.com/<toolname>`

or 

-  `\\live.sysinternals.com\tools\<toolname>`

Let's take a look at how we can do this.

Based on the instructions, to launch Process Monitor from the web the syntax is `\\live.sysinternals.com\tools\procmon.exe`.

And it fails.

![image](https://user-images.githubusercontent.com/51442719/204412416-c3baf9a5-0e95-4917-b676-61eeb55eb558.png)

To resolve this issue the WebDAV client must be installed and running on the machine. The WebDAV protocol is what allows a local machine to access a remote machine running a WebDAV share and perform actions in it.

On a Windows 10 client, the WebDAV client is installed but the client is most likely not running. If you try to run a Sysinternals tool it will fail with a message "The network path was not found."

![image](https://user-images.githubusercontent.com/51442719/204412594-fb18415b-3772-4cc2-945c-6d56e04b9588.png)

The service needs to be started before attempting to call any Sysinternals tool in this fashion.

![image](https://user-images.githubusercontent.com/51442719/204412667-30716275-59ec-4830-a12a-dbb9f428c20e.png)

Verify it's running before proceeding.

![image](https://user-images.githubusercontent.com/51442719/204412685-875fd93d-6b19-4ec8-945c-08761f0faac4.png)

Also, Network Discovery needs to be enabled as well. This setting can be enabled in the Network and Sharing Center.

There are a few ways to open the Network and Sharing Center. Here is a neat command line to launch it.

![image](https://user-images.githubusercontent.com/51442719/204412706-890a45cc-3c6f-45a6-a356-4653e680abca.png)

Click on `Change advanced sharing settings` and select `Turn on network discovery` for your current network profile.

The attached VM is a Windows Server 2019 edition. The WebDAV client is not installed by default.

The feature to install on Windows Server is WebDAV Redirector. This feature can be installed via Server Manager or using PowerShell.

To install with PowerShell, `Install-WindowsFeature WebDAV-Redirector –Restart`. The server needs to reboot for the installation to complete.

After reboot, the installation can be verified with the following PowerShell command, `Get-WindowsFeature WebDAV-Redirector | Format-Table –Autosize`.

![image](https://user-images.githubusercontent.com/51442719/204412841-a4c604cd-bbe3-491c-b1f6-c72cbbcabaaa.png)

The same process as with a Windows 10 client applies from this point:

- Make sure the WebClient service is running
- Make sure Network Discovery is enabled

Now with all the necessary components installed and enabled the local machine is ready to run Sysinternals tools from the web. 

There are 2 ways the tools can be run:

- Run the tool from the command line (as shown above from the Windows 10 machine)
- Create a network drive and run the tool from the mapped drive

Method 1 - Run tool from command line

![image](https://user-images.githubusercontent.com/51442719/204412904-c5895724-611a-4de3-b2b1-a2f34dd8baae.png)

Method 2 - Run tool from a mapped drive

![image](https://user-images.githubusercontent.com/51442719/204412918-d0b9f743-d89b-4f8d-8cd0-a5d4984fe7de.png)

Note: The asterisk will auto-assign a drive letter. The asterick can be replaced with an actual drive letter instead.

![image](https://user-images.githubusercontent.com/51442719/204412939-1adca69d-ee38-4900-9542-474322e7ec7f.png)

The website is now browsable within the local machine.

![image](https://user-images.githubusercontent.com/51442719/204413008-fec1766f-ee39-4411-b69b-93ce7a7a027c.png)

![image](https://user-images.githubusercontent.com/51442719/204413089-41a56765-601d-46d5-a448-cb6c124cbda2.png)

Now that we got that out of the way time to start exploring some of these tools.

---

## Task 4  File and Disk Utilities

Each task within this room will focus on 1 or 2 tools per section (maybe more).

Again, the goal is to introduce you to the Sysinternals tools, but there are far too many tools to go into each tool in depth.

### Sigcheck

"Sigcheck is a command-line utility that shows file version number, timestamp information, and digital signature details, including certificate chains. It also includes an option to check a file’s status on VirusTotal, a site that performs automated file scanning against over 40 antivirus engines, and an option to upload a file for scanning." (official definition)

![image](https://user-images.githubusercontent.com/51442719/204417001-9c45cc35-bff9-4622-a28a-40ada58d9833.png)

From the official Sigcheck [page](https://docs.microsoft.com/en-us/sysinternals/downloads/sigcheck), a use case is identified towards the bottom of the page.

If you completed the Core Windows Processes room you should be aware that the location of all the executables is `C:\Windows\System32`, except for Explorer.exe (which is `C:\Windows`).

Use Case: Check for unsigned files in C:\Windows\System32.

Command: `sigcheck -u -e C:\Windows\System32`

![image](https://user-images.githubusercontent.com/51442719/204417132-4ea8d33a-5972-4712-ab9a-c0ad27fb66ed.png)

Parameter usage:

- `-u` "If VirusTotal check is enabled, show files that are unknown by VirusTotal or have non-zero detection, otherwise show only unsigned files."
- `-e` "Scan executable images only (regardless of their extension)"

> `Note`: If the results were different it would warrant an investigation into any listed executables. 

### Streams
"The NTFS file system provides applications the ability to create alternate data streams of information. By default, all data is stored in a file's main unnamed data stream, but by using the syntax 'file:stream', you are able to read and write to alternates." (official definition)

Alternate Data Streams (ADS) is a file attribute specific to Windows NTFS (New Technology File System). Every file has at least one data stream ($DATA) and ADS allows files to contain more than one stream of data. Natively Window Explorer doesn't display ADS to the user. There are 3rd party executables that can be used to view this data, but Powershell gives you the ability to view ADS for files.

Malware writers have used ADS to hide data in an endpoint, but not all its uses are malicious. When you download a file from the Internet unto an endpoint, there are identifiers written to ADS to identify that it was downloaded from the Internet.

![image](https://user-images.githubusercontent.com/51442719/204417344-022ca750-0c41-4347-ac6c-5bac66c96509.png)

Example: A file downloaded from the Internet.

![image](https://user-images.githubusercontent.com/51442719/204417371-a81d08b2-cdc9-41c8-8c88-51a0fc65271b.png)

Since the file has this identifier, additional security measures are added to its properties.

![image](https://user-images.githubusercontent.com/51442719/204417395-ed8d4fa7-cd6b-4b61-a7f6-21a118bef4ed.png)

You can read more on streams [here](https://docs.microsoft.com/en-us/sysinternals/downloads/streams).

### SDelete

"SDelete is a command line utility that takes a number of options. In any given use, it allows you to delete one or more files and/or directories, or to cleanse the free space on a logical disk."

As per the official documentation page, SDelete (Secure Delete) implemented the DOD 5220.22-M (Department of Defense clearing and sanitizing protocol).

![image](https://user-images.githubusercontent.com/51442719/204417512-1c4df0a3-3cc9-46c2-aba2-420514418709.png)

Source: https://www.lifewire.com/dod-5220-22-m-2625856

SDelete has been used by adversaries and is associated with MITRE techniques T1485 (Data Destruction) and T1070.004 (Indicator Removal on Host: File Deletion). It's MITRE ID S0195.

You can review this tool more in-depth by visiting its Sysinternals SDelete [page](https://docs.microsoft.com/en-us/sysinternals/downloads/sdelete). 

Other tools fall under the File and Disk Utilities category. I encourage you to explore these tools at your own leisure.

Link: https://docs.microsoft.com/en-us/sysinternals/downloads/file-and-disk-utilities 

---

## Task 5  Networking Utilities

### TCPView

"TCPView is a Windows program that will show you detailed listings of all TCP and UDP endpoints on your system, including the local and remote addresses and state of TCP connections. On Windows Server 2008, Vista, and XP, TCPView also reports the name of the process that owns the endpoint. TCPView provides a more informative and conveniently presented subset of the Netstat program that ships with Windows. The TCPView download includes Tcpvcon, a command-line version with the same functionality." (official definition)

This is a good time to mention that Windows has a built-in utility that provides the same functionality. This tool is called Resource Monitor. There are many ways to open this tool. From the command line use `resmon`.

![image](https://user-images.githubusercontent.com/51442719/204419121-5b6430d0-6087-4dcb-87b7-02c24d253b3c.png)

Expand TCP Connections to view the Remote Address for each Process with an outbound connection.

![image](https://user-images.githubusercontent.com/51442719/204419151-f03bd248-1d91-4a6e-8aec-d07b92b84109.png)

This tool can also be called from the Performance tab within Task Manager. Look at the bottom left for the link to open Resource Monitor.

![image](https://user-images.githubusercontent.com/51442719/204419178-956a5930-45ef-4fd0-9496-65b65549fa83.png)

Now back to TCPView.

![image](https://user-images.githubusercontent.com/51442719/204419207-405e2b5a-aba5-41ee-b68c-c90365b056ae.png)

The below image shows the default view for TCPView.

![image](https://user-images.githubusercontent.com/51442719/204419247-5aaaa55d-06b0-4ac3-96f7-41c675c06272.png)

We can apply additional filtering by turning off TCP v4, TCP v6, UDP v4, and UDP v6 at the top toolbar, depending on which protocols we want to display. Moreover, we can click on the green flag to use the States Filter.

![image](https://user-images.githubusercontent.com/51442719/204419338-4af99e7e-4a6e-45d6-9ba5-3b6ed912e221.png)

Clicking the green flag opens the States Filter, which provides an extensive list of options to select which connection states we want to display. Most of the connection states available apply only to TCP connections. (UDP, being a connectionless protocol, cannot offer this flexibility in filtering.)

![image](https://user-images.githubusercontent.com/51442719/204419354-162a89da-decb-4fbd-aee1-30c31c5c4e49.png)

The list below shows all TCP v4 and TCP v6 connections in any state except in the "Listen" state. For instance, we notice that we have one TCP connection in an Established state and another connection in a Close Wait state.

In the below image, I unselected Listen in the Connection States from the States Filter and turned off UDP v4 and UDP v6 from the top toolbar.

![image](https://user-images.githubusercontent.com/51442719/204419377-a69219eb-9de8-46d4-8b4e-5cca26398d33.png)

Now the output only displays processes with an established outbound connection.

Other tools fall under the Networking Utilities category. I encourage you to explore these tools at your own leisure.

> `Link`: https://docs.microsoft.com/en-us/sysinternals/downloads/networking-utilities

---

## Task 6  Process Utilities

> `Note`: Some of these tools require you to run as an administrator.

### Autoruns

"This utility, which has the most comprehensive knowledge of auto-starting locations of any startup monitor, shows you what programs are configured to run during system bootup or login, and when you start various built-in Windows applications like Internet Explorer, Explorer and media players. These programs and drivers include ones in your startup folder, Run, RunOnce, and other Registry keys. Autoruns reports Explorer shell extensions, toolbars, browser helper objects, Winlogon notifications, auto-start services, and much more. Autoruns goes way beyond other autostart utilities." (official definition)

> `Note`: This is a good tool to search for any malicious entries created in the local machine to establish Persistence.

Launch Autoruns.

![image](https://user-images.githubusercontent.com/51442719/204656600-244bf2af-358a-4fe3-80b9-089411353a05.png)

Below is a snapshot of Autoruns, showing the first couple of items from the Everything tab. Normally there are a lot of entries within this tab.

![image](https://user-images.githubusercontent.com/51442719/204656640-3f83015e-848e-4eef-808b-b960f0c088a2.png)

Notice all the tabs within the application. Click on each tab to inspect the items associated with each. 

The below image is a snapshot of the Image Hijacks tab. (At this time there is only 1 item listed)

![image](https://user-images.githubusercontent.com/51442719/204656694-13db293e-3c3d-4b08-95e0-6df208a8f02f.png)

### ProcDump

"ProcDump is a command-line utility whose primary purpose is monitoring an application for CPU spikes and generating crash dumps during a spike that an administrator or developer can use to determine the cause of the spike." (official definition)

![image](https://user-images.githubusercontent.com/51442719/204656845-9fdd9e3b-1e8f-4625-b583-67a333a298dc.png)

Alternatively, you can use Process Explorer to do the same.

Right-click on the process to create a Minidump or Full Dump of the process.

![image](https://user-images.githubusercontent.com/51442719/204656865-bfabc8f7-ee61-40b8-a5aa-d63ba8ed142e.png)

Please refer to the examples listed on the ProcDump [page](https://docs.microsoft.com/en-us/sysinternals/downloads/procdump) to learn about all the available options with running this tool.

### Process Explorer

"The Process Explorer display consists of two sub-windows. The top window always shows a list of the currently active processes, including the names of their owning accounts, whereas the information displayed in the bottom window depends on the mode that Process Explorer is in: if it is in handle mode you'll see the handles that the process selected in the top window has opened; if Process Explorer is in DLL mode you'll see the DLLs and memory-mapped files that the process has loaded." (official definition)

![image](https://user-images.githubusercontent.com/51442719/204656955-313d534f-624f-44ce-8321-b7fae2e5b86c.png)

This tool was touched on slightly within the Core Windows Processes room. Process Hacker was intentionally used in that room to broaden your exposure to various tools that essentially perform the same tasks with subtle differences. 

Since much of the basic foundational information was discussed in the Core Windows Processes room, Process Explorer will be briefly touched.

In the following images, let's look at svchost.exe PID 3636 more closely.

![image](https://user-images.githubusercontent.com/51442719/204656980-b6a6be10-8a45-4418-8097-8a76fa738f9a.png)

![image](https://user-images.githubusercontent.com/51442719/204657010-a7f91c8a-08ea-42c5-bf9e-04d872a1c1f3.png)

This process is associated with the WebClient service that is needed to connect to live.sysinternals.com (WebDAV).

There should be web traffic listed in the TCP/IP tab.

![image](https://user-images.githubusercontent.com/51442719/204657045-22b89b7f-2da0-4f21-9923-5226c50492fe.png)

Ideally, it would be wise to check if that IP is what we assume it is.

Various online tools can be utilized to verify the authenticity of an IP address. For this demonstration, I'll use Talos Reputation Center.

![image](https://user-images.githubusercontent.com/51442719/204657087-b1b2598c-f39d-461a-8ee7-60f6a73182b5.png)

https://talosintelligence.com/reputation_center/lookup?search=52.154.170.73

As mentioned in the ProcExp description, we can see open handles associated with the process within the bottom window.

![image](https://user-images.githubusercontent.com/51442719/204657160-1113e568-2ef0-46ac-a78a-f53c463dfa61.png)

Listed as an open handle is the connection to the remote WebDAV folder.

There is an option within ProcExp to Verify Signatures. Once enabled, it shows up as a column within the Process view.

![image](https://user-images.githubusercontent.com/51442719/204657221-9996cfec-a1f7-4ded-b5ad-03c6bb24fc28.png)

Other options to note include Run at Logon and Replace Task Manager.

You may have noticed that some of the processes within Process Explorer have different colors. Those colors have meaning.

Below is a snippet from MalwareBytes explaining what each of those colors means.

### Process Monitor

"Process Monitor is an advanced monitoring tool for Windows that shows real-time file system, Registry and process/thread activity. It combines the features of two legacy Sysinternals utilities, Filemon and Regmon, and adds an extensive list of enhancements including rich and non-destructive filtering, comprehensive event properties such as session IDs and user names, reliable process information, full thread stacks with integrated symbol support for each operation, simultaneous logging to a file, and much more. Its uniquely powerful features will make Process Monitor a core utility in your system troubleshooting and malware hunting toolkit." (official definition)

Launch ProcMon.

![image](https://user-images.githubusercontent.com/51442719/204657285-3336f16f-eb63-4e53-a0f1-c7c3ab36f01d.png)

In the below snapshot, I set a filter to capture all the events related to PID 3888, notepad.exe. You can see some of the file operations that were captured and the file path or registry path/key the action occurred on, and the operation result.

![image](https://user-images.githubusercontent.com/51442719/204657321-0c43af5e-d148-41bc-9f1d-590a152044aa.png)

ProcMon will capture thousands upon thousands of events occurring within the operating system.

The option to capture events can be toggled on and off. 

![image](https://user-images.githubusercontent.com/51442719/204657361-3602c15a-2283-4529-96d4-b6e4d7353e39.png)

In this ProcMon example, the session captured events only for a few seconds. Look at how many events were captured in that short space of time!

![image](https://user-images.githubusercontent.com/51442719/204657401-dd5e277d-d432-4fd1-b2b5-0c796859a888.png)

To use ProcMon effectively you must use the Filter and must configure it properly.

![image](https://user-images.githubusercontent.com/51442719/204657430-36e5091e-192d-4783-9f6f-c71cd8c2e464.png)

In the above image, a filter was already set to capture events associated with PID 3888. Alternatively, a filter could have been set to capture events with the Process Name = notepad.exe. 

Here is a useful guide on configuring ProcMon.

> `Note`: To fully understand the output from some of these tools you need to understand some Windows concepts, such as [Processes and Threads](https://docs.microsoft.com/en-us/windows/win32/procthread/about-processes-and-threads) and [Windows API](https://docs.microsoft.com/en-us/windows/win32/apiindex/windows-api-list) calls.  

### PsExec

"PsExec is a light-weight telnet-replacement that lets you execute processes on other systems, complete with full interactivity for console applications, without having to manually install client software. PsExec's most powerful uses include launching interactive command-prompts on remote systems and remote-enabling tools like IpConfig that otherwise do not have the ability to show information about remote systems." (official definition)

![image](https://user-images.githubusercontent.com/51442719/204858742-31bbef02-b4c4-4003-908f-760c784d6c0f.png)

PsExec is another tool that is utilized by adversaries. This tool is associated with MITRE techniques [T1570](https://attack.mitre.org/techniques/T1570) (Lateral Tool Transfer), [T1021.002](https://attack.mitre.org/techniques/T1021/002) (Remote Services: SMB/Windows Admin Shares), and [T1569.002](https://attack.mitre.org/techniques/T1569/002) (System Services: Service Execution). It's MITRE ID is [S0029](https://attack.mitre.org/software/S0029/).

You can review this tool more in-depth by visiting its Sysinternals [PsExec](https://docs.microsoft.com/en-us/sysinternals/downloads/psexec) page. You can also check out this resource [page](https://adamtheautomator.com/psexec-ultimate-guide/).

Other tools fall under the Process Utilities category. I encourage you to explore these tools at your own leisure.

- Link: https://docs.microsoft.com/en-us/sysinternals/downloads/process-utilities

---

## Task 7  Security Utilities

### Sysmon

"System Monitor (Sysmon) is a Windows system service and device driver that, once installed on a system, remains resident across system reboots to monitor and log system activity to the Windows event log. It provides detailed information about process creations, network connections, and changes to file creation time. By collecting the events it generates using Windows Event Collection or SIEM agents and subsequently analyzing them, you can identify malicious or anomalous activity and understand how intruders and malware operate on your network." (official definition)

Sysmon is a comprehensive tool, and it can't be summarized in just one section.

Check out the Sysmon [room](https://tryhackme.com/room/sysmon) to further learn what Sysmon is and how to use it.  

Screenshot of the Sysmon room card

![image](https://user-images.githubusercontent.com/51442719/204862748-e5066c31-8575-404b-b151-2dac5a472b29.png)

Other tools fall under the Security Utilities category. I encourage you to explore these tools at your own leisure.

- Link: https://docs.microsoft.com/en-us/sysinternals/downloads/security-utilities

---

## Task 8  System Information

### WinObj

"WinObj is a 32-bit Windows NT program that uses the native Windows NT API (provided by NTDLL.DLL) to access and display information on the NT Object Manager's name space." (official definition)

To showcase this tool, let's look into the concept of Session 0 and Session 1 that was mentioned in the Core Windows Processes room.

Remember that Session 0 is the OS session and Session 1 is the User session. Also recall that there will be at least 2 csrss.exe processes running, one for each session. Note Session 1 will be for the first user logged into the system.  

Launch WinObj.

![image](https://user-images.githubusercontent.com/51442719/204862879-7b0435e1-5ccb-4a16-804e-8dcf6ed6b336.png)

The below image shows the default view for WinObj.

![image](https://user-images.githubusercontent.com/51442719/204862904-8f7b9ed8-45b9-49d9-9e36-0fc641d19386.png)

Within Session 0, under `DosDevices`, there is an entry for the network drive I mounted in my local machine.

![image](https://user-images.githubusercontent.com/51442719/204863011-8c4c449d-22f9-4ebd-8d02-93a29c5f3d9b.png)

Let's look at `WindowStations` value for Session 1. 

![image](https://user-images.githubusercontent.com/51442719/204863077-3ffb3848-9756-4a4c-b948-b8ecdb74833e.png)

Let's compare this information with Process Explorer. The below image is for csrss.exe, which was launched along with winlogon.exe by smss.exe.

![image](https://user-images.githubusercontent.com/51442719/204863125-fce8f4e4-eca5-4971-884d-63de53ca91f0.png)

> `Note`: This is a high-level exposure for this tool.

Other tools fall under the System Information category. I encourage you to explore these tools at your own leisure.

- Link: https://docs.microsoft.com/en-us/sysinternals/downloads/system-information

---

## Task 9  Miscellaneous

---

## Task 10  Conclusion


---
---

- https://www.thedutchhacker.com/sysinternals-on-tryhackme/
