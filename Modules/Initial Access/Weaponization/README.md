![image](https://user-images.githubusercontent.com/51442719/180655800-ab7238f2-e777-4ea2-8203-8c2a0ca86566.png)

# [Weaponization](https://tryhackme.com/room/weaponization)
> #### Understand and explore common red teaming weaponization techniques. 
> #### You will learn to build custom payloads using common methods seen in the industry to get initial access.

---

- [ ] [Task 1  Introduction]()
- [ ] [Task 2  Deploy the Windows Machine]()
- [ ] [Task 3  Windows Scripting Host - WSH]()
- [ ] [Task 4  An HTML Application - HTA]()
- [ ] [Task 5  Visual Basic for Application - VBA]()
- [ ] [Task 6  PowerShell - PSH]()
- [ ] [Task 7  Command And Control - (C2 Or C&C)]()
- [ ] [Task 8  Delivery Techniques]()
- [ ] [Task 9  Practice Arena](#task-9--practice-arena)

---

# [Task 1  Introduction]()

---

# [Task 2  Deploy the Windows Machine]()

---

# [Task 3  Windows Scripting Host - WSH]()

---

# [Task 4  An HTML Application - HTA]()

---

# [Task 5  Visual Basic for Application - VBA]()

---

# [Task 6  PowerShell - PSH]()

---

# [Task 7  Command And Control - (C2 Or C&C)]()

---

# [Task 8  Delivery Techniques]()

---

# [Task 9  Practice Arena]()

- We have prepared a Windows 10 machine that runs a user simulation web app to execute your payloads or visit the malicious HTA links automatically. 
- Deploy the attached machine and wait a couple of minutes until it's up and running. 
- Then, visit the user simulator web application at `http://10.10.132.115:8080/`.
- Make sure to visit the user simulator web application from the AttackBox, or you can access it by connecting to the VPN.
  > ![image](https://user-images.githubusercontent.com/51442719/180656171-3cd54534-77fc-458a-9d7b-f431ca69280d.png)
- The web application allows uploading payloads as VBS, DOC, PS1 files. In addition, if you provide a malicious HTA link, the web application will visit your link.
- **Note for Doc files**: the simulation used in the provided Windows 10 machine will open the malicious Word document and be closed within 90 seconds. 
- In order to get longer prescience, you need to migrate as soon as you receive the connection back. 
- In the Metasploit framework, we can inject our current process into another process on the victim machine using migrate. 
- In our case, we need to `migrate` our current process, which is the MS word document, into another process to make the connection stable even if the MS word document is closed. 
- The easiest way to do this is by using `migrate` post-module as follow,
```cmd
meterpreter > run post/windows/manage/migrate 
```
- In this task, the goal is to generate a reverse shell payload of your choice and send it through the web application. 
- Once the web application runs your payload, you should receive a connect back. 
- Answer the question below and prove your access by finding the flag once you receive a reverse shell.
- For reference, you can use the MSFVenom Cheat Sheet on this [`website`](https://thedarksource.com/msfvenom-cheat-sheet-create-metasploit-payloads/).

### Answer the questions below
- What is the flag? Hint: Check the user desktop folder for the flag!
  > Answer format: [`***{********************************}`]()







