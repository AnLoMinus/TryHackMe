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

Per the Sysinternals website, "Sysinternals Live is a service that enables you to execute Sysinternals tools directly from the Web without hunting for and manually downloading them. Simply enter a tool's Sysinternals Live path into Windows Explorer or a command prompt as live.sysinternals.com/<toolname> or \\live.sysinternals.com\tools\<toolname>."

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

---

## Task 6  Process Utilities

---

## Task 7  Security Utilities

---

## Task 8  System Information

---

## Task 9  Miscellaneous

---

## Task 10  Conclusion


---
---

- https://www.thedutchhacker.com/sysinternals-on-tryhackme/
