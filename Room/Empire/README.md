![image](https://user-images.githubusercontent.com/51442719/172147333-d5f57d13-9826-4149-b092-c411c15f32cf.png)

# [Empire](https://tryhackme.com/room/rppsempire)
> #### Learn how to use Empire and it's GUI Starkiller, a powerful post-exploitation C2 framework.
  - [x] [Task 1  Introduction](#task-1--introduction)
  - [x] [Task 2  Deploy!](#task-2--deploy)
  - [x] [Task 3  Installation](#task-3--installation)
  - [ ] [Task 4  Menu Overview](#task-4--menu-overview)
  - [ ] [Task 5  Listeners](#task-5--listeners)
  - [ ] [Task 6  Stagers](#task-6--stagers)
  - [ ] [Task 7  Agents](#task-7--agents)
  - [ ] [Task 8  Modules](#task-8--modules)
  - [ ] [Task 9  Plugins](#task-9--plugins)
  - [ ] [Task 10  Conclusion](#task-10--conclusion)

---

# [Task 1  Introduction]()
- Empire, a C2 or Command and Control server created by BC-Security, used to deploy agents onto a device and remotely run modules. 
- Empire is a free and open-source alternative to other command and control servers like the well known Cobalt Strike C2. 
- In this room, we will cover the basics of setting up a listener and stager as well as what types are available, then learn how to use an agent on a device.
  > ![image](https://user-images.githubusercontent.com/51442719/180655567-3d560a24-ac46-4c48-9475-52bc0cded873.png)
- The virtual machine used in this room is [`Blue`](https://tryhackme.com/room/blue) created by DarkStar7417 you can download the box for offline use here or deploy the box on Tryhackme in Task 6.
- Before completing this room we recommend completing the '[`What the Shell`](https://tryhackme.com/room/introtoshells)' room by MuirlandOracle and ''Blue' by DarkStar7471.
- If you have a general understanding of basic reverse shells and exploitation techniques then you will be ready to begin.

---

# [Task 2  Deploy!]()
- Before we can move on to using Empire we need to deploy a machine to connect the Empire server with.
- Deploy this machine and discover what exploit this machine is vulnerable to. 
- The virtual machine used in this room (Blue) can be downloaded for offline usage from https://darkstar7471.com/resources.html
- We recommend completing the room '[`Blue`](https://tryhackme.com/room/blue)' prior to this room for this purpose alone.

---

# [Task 3  Installation]()

- The installation for Empire and Starkiller very easy and can all be done from the command line. The choice is up to you on whether or not you want to use the GUI for Empire, the room itself will showcase Starkiller but all functionalities are the same. 
- For further instructions on installing Empire refer to the [`BC-Security Github`](https://github.com/BC-SECURITY/Empire).
> 💡 `Note`: Starkiller is the GUI for Empire is not required however it will be used within this room.
- For more information about Empire check out the BC-Security blog.

### Installing Empire
#### We can begin by installing Empire on our device. Follow the instructions below to install Empire.

```cmd
cd /opt
```
```cmd
git clone https://github.com/BC-SECURITY/Empire/
```
```cmd
cd /opt/Empire
```
```cmd
./setup/install.sh
```

### Installing Starkiller
#### Once Empire is installed we can install the GUI for Empire known as Starkiller.
```cmd
cd /opt
```
- Download an up to date version of Starkiller from the BC-Security Github repo 
  - https://github.com/BC-SECURITY/Starkiller/releases 
```cmd
chmod +x starkiller-0.0.0.AppImage
```

### Starting Empire
#### Once both Empire and Starkiller are installed we can start both servers. 
- Being by starting Empire with the instructions below.
```cmd
cd /opt/Empire
```
```cmd
./empire --rest
```

### Starting Starkiller
#### Once Empire is started follow the instructions below to start Starkiller.
```cmd
cd /opt
```
```cmd
./starkiller-0.0.0.AppImage
```
- Login to Starkiller
  - Default Credentials
    - Uri: `127.0.0.1:1337`
    - User: `empireadmin`
    - Pass: `password123`
- Once you have logged into Starkiller you should be greeted with the Listeners menu, once you have Starkiller or Empire ready move on to Task 3 to get familiar with the menu.



---

# [Task 4  Menu Overview]()

---

# [Task 5  Listeners]()

---

# [Task 6  Stagers]()

---

# [Task 7  Agents]()

---

# [Task 8  Modules]()

---

# [Task 9  Plugins]()

---

# [Task 10  Conclusion]()

---
