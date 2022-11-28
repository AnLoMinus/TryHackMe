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

---

## Task 4  File and Disk Utilities

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

