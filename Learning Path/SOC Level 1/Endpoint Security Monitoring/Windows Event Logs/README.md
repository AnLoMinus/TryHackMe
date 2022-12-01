# [Windows Event Logs](https://tryhackme.com/room/windowseventlogs)
### Introduction to Windows Event Logs and the tools to query them.

![image](https://user-images.githubusercontent.com/51442719/204950471-d51493e5-a6fa-49c4-9066-8f5bebe2fc54.png)

---

- [Task 1 What are event logs?]()
- [Task 2 Event Viewer]()
- [Task 3 wevtutil.exe]()
- [Task 4 Get-WinEvent]()
- [Task 5 XPath Queries]()
- [Task 6 Event IDs]()
- [Task 7 Putting theory into practice]()
- [Task 8 Conclusion]()

---

## Task 1  What are event logs?

Per Wikipedia, "Event logs record events taking place in the execution of a system to provide an audit trail that can be used to understand the activity of the system and to diagnose problems. They are essential to understand the activities of complex systems, particularly in applications with little user interaction (such as server applications)."

This definition would apply to system administrators, IT technicians, desktop engineers, etc. If the endpoint is experiencing an issue, the event logs can be queried to see clues about what led to the problem. The operating system, by default, writes messages to these logs.

As defenders (blue teamers), there is another use case for event logs. "It can also be useful to combine log file entries from multiple sources. This approach, in combination with statistical analysis, may yield correlations between seemingly unrelated events on different servers."

This is where SIEMs (Security information and event management) such as Splunk and Elastic come into play.

If you don't know exactly what a SEIM is used for, below is a visual overview of its capabilities. (Image credit: [Varonis](https://www.varonis.com/blog/what-is-siem/))

![image](https://user-images.githubusercontent.com/51442719/204950735-e7ad7e01-cb59-4bd1-b5e7-c0c5532ef98a.png)

Even though it's possible to access a remote machine's event logs, this will not be feasible in a large enterprise environment. Instead, one can view the logs from all the endpoints, appliances, etc., in a SIEM. This will allow you to query the logs from multiple devices instead of manually connecting to a single device to view its logs.

Windows is not the only operating system that uses a logging system. Linux and macOS do as well. For example, on Linux systems, the logging system is known as Syslog. Within this room, though, we're only focusing on the Windows logging system called Windows Event Logs.

### Room Machine

Before moving forward, please deploy the machine. 

You can use the AttackBox and Remmina to connect to the remote machine. Make sure the remote machine is deployed before proceeding.

Click on the plus icon, as shown below.

![image](https://user-images.githubusercontent.com/51442719/204950830-cff7e265-e5ec-4650-95a3-f19c094369f0.png)

For Server provide (`10.10.242.68`) as the IP address provided to you for the remote machine. The credentials for the user account are:

- User name: `administrator`
- User password: `blueT3aming!`

![image](https://user-images.githubusercontent.com/51442719/204950875-be8a79e6-31f1-4706-b390-f503f12abb1d.png)

---

## Task 2  Event Viewer

The Windows Event Logs are not text files that can be viewed using a text editor. However, the raw data can be translated into XML using the Windows API. The events in these log files are stored in a proprietary binary format with a .evt or .evtx extension. The log files with the .evtx file extension typically reside in `C:\Windows\System32\winevt\Logs`.


### Elements of a Windows Event Log
Event logs are crucial for troubleshooting any computer incident and help understand the situation and how to remediate the incident. To get this picture well, you must first understand the format in which the information will be presented. Windows offers a standardized means of relaying this system information.

First, we need to know what elements form event logs in Windows systems. These elements are:
- System Logs: Records events associated with the Operating System segments. They may include information about hardware changes, device drivers, system changes, and other activities related to the device.
- Security Logs: Records events connected to logon and logoff activities on a device. The system's audit policy specifies the events. The logs are an excellent source for analysts to investigate attempted or successful unauthorized activity.
- Application Logs: Records events related to applications installed on a system. The main pieces of information include application errors, events, and warnings.
- Directory Service Events: Active Directory changes and activities are recorded in these logs, mainly on domain controllers.
- File Replication Service Events:
- DNS Event Logs: DNS servers use these logs to record domain events and to map out
- Custom Logs: Events are logged by applications that require custom data storage. This allows applications to control the log size or attach other parameters, such as ACLs, for security purposes.

Under this categorization, event logs can be further classified into types. Here, types describe the activity that resulted in the event being logged. There are 5 types of events that can be logged, as described in the table below from [docs.microsoft.com](https://docs.microsoft.com/en-us/windows/win32/eventlog/event-types).

![image](https://user-images.githubusercontent.com/51442719/204951375-e6986142-4d16-4cab-bb10-ab082929887c.png)


There are three main ways of accessing these event logs within a Windows system:
- Event Viewer (GUI-based application)
- Wevtutil.exe (command-line tool)
- Get-WinEvent (PowerShell cmdlet)

### Event Viewer
In any Windows system, the Event Viewer, a Microsoft Management Console (MMC) snap-in, can be launched by simply right-clicking the Windows icon in the taskbar and selecting Event Viewer. For the savvy sysadmins that use the CLI much of their day, Event Viewer can be launched by typing `eventvwr.msc`. It is a GUI-based application that allows you to interact quickly with and analyze logs.

Event Viewer has three panes.
- The pane on the left provides a hierarchical tree listing of the event log providers.
- The pane in the middle will display a general overview and summary of the events specific to a selected provider.
- The pane on the right is the actions pane.

![image](https://user-images.githubusercontent.com/51442719/204951486-c18ac7bd-d174-4732-957d-8479127b277e.png)


The standard logs we had earlier defined on the left pane are visible under Windows Logs. 

The following section is the Applications and Services Logs. Expand this section and drill down on `Microsoft > Windows > PowerShell > Operational`. PowerShell will log operations from the engine, providers, and cmdlets to the Windows event log. 

Right-click on Operational then Properties.

![image](https://user-images.githubusercontent.com/51442719/204951723-1bd2b993-afe2-43fc-b015-0b0ba9087de8.png)

Within Properties, you see the log location, log size, and when it was created, modified, and last accessed. Within the Properties window, you can also see the maximum set log size and what action to take once the criteria are met. This concept is known as log rotation. These are discussions held with corporations of various sizes. How long does it take to keep logs, and when it's permissible to overwrite them with new data.

Lastly, notice the Clear Log button at the bottom right. There are legitimate reasons to use this button, such as during security maintenance, but adversaries will likely attempt to clear the logs to go undetected. Note: This is not the only method to remove the event logs for any given event provider.

Focus your attention on the middle pane. Remember from previous descriptions that this pane will display the events specific to a selected provider. In this case, PowerShell/Operational.

![image](https://user-images.githubusercontent.com/51442719/204951773-8ffec8a5-f1f2-47b2-b32a-12d7348c67eb.png)

From the above image, notice the event provider's name and the number of events logged. In this case, there are 44 events logged. You might see a different number. No worries, though. Each column of the pane presents a particular type of information as described below:
- Level: Highlights the log recorded type based on the identified event types specified earlier. In this case, the log is labeled as Information.
- Date and Time: Highlights the time at which the event was logged.
- Source: The name of the software that logs the event is identified. From the above image, the source is PowerShell.
- Event ID: This is a predefined numerical value that maps to a specific operation or event based on the log source. This makes Event IDs not unique, so Event ID 4103 in the above image is related to Executing Pipeline but will have an entirely different meaning in another event log.
- Task Category: Highlights the Event Category. This entry will help you organize events so the Event Viewer can filter them. The event source defines this column.

The middle pane has a split view. More information is displayed in the bottom half of the middle pane for any event you click on.

This section has two tabs: General and Details.
- General is the default view, and the rendered data is displayed.
- The Details view has two options: Friendly view and XML view.

Below is a snippet of the General view.

![image](https://user-images.githubusercontent.com/51442719/204955700-c0a60519-5e0e-47c6-89fc-cf1b8569cb41.png)


Lastly, take a look at the Actions pane. Several options are available, but we'll only focus on a few. Please examine all the actions that can be performed at your leisure if you're unfamiliar with MMC snap-ins.

As you should have noticed, you can open a saved log within the Actions pane. This is useful if the remote machine can't be accessed. The logs can be provided to the analyst. You will perform this action a little later. 

The Create Custom View and Filter Current Log are nearly identical. The only difference between the 2 is that the By log and By source radio buttons are greyed out in Filter Current Log. What is the reason for that? The filter you can make with this specific action only relates to the current log. Hence no reason for '`by log`' or '`by source`' to be enabled.

![image](https://user-images.githubusercontent.com/51442719/204955765-8ba49f73-5166-4d61-823f-e805be6ae737.png)

Why are these actions beneficial? Say, for instance, you don't want all the events associated with PowerShell/Operational cluttering all the real estate in the pane. Maybe you're only interested in 4104 events. That is possible with these two actions. 

To view event logs from another computer, right-click `Event Viewer (Local) > Connect to Another Computer...`

![image](https://user-images.githubusercontent.com/51442719/204955890-d563c6a6-c5f7-436c-abb3-0ed473bd78d7.png)

That will conclude the general overview of the Event Viewer—time to become familiar with the tool.

> `Note`: Don't forget to deploy the machine for this room before proceeding. Give the room about 3 minutes to load fully.

---

## Task 3  wevtutil.exe

---

## Task 4  Get-WinEvent

---

## Task 5  XPath Queries

---

## Task 6  Event IDs

---

## Task 7  Putting theory into practice

---

## Task 8  Conclusion
