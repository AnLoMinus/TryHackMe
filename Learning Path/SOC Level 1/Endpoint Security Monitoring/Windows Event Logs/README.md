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
