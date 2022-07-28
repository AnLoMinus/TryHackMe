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
