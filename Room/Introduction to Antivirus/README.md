![image](https://user-images.githubusercontent.com/51442719/180161008-64a5b047-53f6-4d3c-8e37-621768a43b52.png)

- [ ] [Introduction to Antivirus](https://tryhackme.com/room/introtoav)
  > Understand how antivirus software works and what detection techniques are used to bypass malicious files checks.
    - [ ] [Task 1  Introduction](#task-1--introduction)
    - [ ] [Task 2  Antivirus Software](#task-2--antivirus-software)
    - [ ] [Task 3  Antivirus Features](#task-3--antivirus-features)
    - [ ] [Task 4  Deploy the VM]()
    - [ ] [Task 5  AV Static Detection]()
    - [ ] [Task 6  Other Detection Techniques]()
    - [ ] [Task 7  AV Testing and Fingerprinting]()
    - [ ] [Task 8  Conclusion]()

---

- `AV` - AntiVirus
- `EDR` - Endpoint Detection and Response

---

## Task 1  Introduction

### Welcome to Intro to AV
- Antivirus (`AV`) software is one of the essential host-based security solutions available to detect and prevent malware attacks within the end-user's machine. 
- AV software consists of different modules, features, and detection techniques, which are discussed in this room.
- As a red teamer or pentester, it is essential to be familiar with and understand how AV software and its detection techniques work. 
- Once this knowledge is acquired, it will be easier to work toward AV evasion techniques.

### Learning Objectives
- What is Antivirus software?
- Antivirus detection approaches
- Enumerate installed AV software in the target machine
- Test in a simulated environment

### Room prerequisites
- General knowledge of host-based detection solutions; check [`The Lay of the Land`](https://tryhackme.com/room/thelayoftheland) room for more information.
- General experience with Hashing crypto; check the [`Hashing - Crypto 101`](https://tryhackme.com/room/hashingcrypto101) room for more information.
- Basic knowledge of Yara Rules; check the THM [`Yara`](https://tryhackme.com/room/yara) room for more information.



---

## Task 2  Antivirus Software

### What is AV software?
- Antivirus (AV) software is an extra layer of security that aims to detect and prevent the execution and spread of malicious files in a target operating system.
- It is a host-based application that runs in real-time (in the background) to monitor and check the current and newly downloaded files. 
- The AV software inspects and decides whether files are malicious using different techniques, which will be covered later in this room.
- Interestingly, the first antivirus software was designed solely to detect and remove computer viruses. 
- Nowadays, that has changed; modern antivirus applications can detect and remove [`computer viruses`](https://malware-history.fandom.com/wiki/Virus) as well other harmful files and threats.

### What does AV software look for?
- Traditional AV software looks for malware with predefined malicious patterns or signatures. 
- Malware is harmful software whose primary goal is to cause damage to a target machine, including but not limited to:
  - Gain full access to a target machine.
  - Steal sensitive information such as passwords.
  - Encrypt files and cause damage to files.
  - Inject other malicious software or unwanted advertisements.
  - Used the compromised machine to perform further attacks such as botnet attacks.

### AV vs other security products
- In addition to AV software, other host-based security solutions provide real-time protection to endpoint devices. 
- `Endpoint Detection and Response` (`EDR`) is a security solution that provides real-time protection based on behavioral analytics. 
- An antivirus application performs scanning, detecting, and removing malicious files. 
- On the other hand, EDR monitors various security checks in the target machine, including file activities, memory, network connections, Windows registry, processes, etc.

Modern Antivirus products are implemented to integrate the traditional Antivirus features and other advanced functionalities (similar to EDR functionalities) into one product to provide comprehensive protection against digital threats.

For more information about Host-based security solutions, we suggest visiting the THM room: The Lay of the Land.


---

## Task 3  Antivirus Features

---

## Task 4  Deploy the VM

---

## Task 5  AV Static Detection

---

## Task 6  Other Detection Techniques

---

## Task 7  AV Testing and Fingerprinting

---

## Task 8  Conclusion
