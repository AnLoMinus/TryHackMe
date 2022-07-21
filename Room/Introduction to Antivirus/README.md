![image](https://user-images.githubusercontent.com/51442719/180161008-64a5b047-53f6-4d3c-8e37-621768a43b52.png)

- [ ] [Introduction to Antivirus](https://tryhackme.com/room/introtoav)
  > Understand how antivirus software works and what detection techniques are used to bypass malicious files checks.
    - [ ] [Task 1  Introduction](#task-1--introduction)
    - [ ] [Task 2  Antivirus Software](#task-2--antivirus-software)
    - [ ] [Task 3  Antivirus Features](#task-3--antivirus-features)
    - [ ] [Task 4  Deploy the VM](#task-4--deploy-the-vm)
    - [ ] [Task 5  AV Static Detection](#task-5--av-static-detection)
    - [ ] [Task 6  Other Detection Techniques](#task-6--other-detection-techniques)
    - [ ] [Task 7  AV Testing and Fingerprinting](#task-7--av-testing-and-fingerprinting)
    - [ ] [Task 8  Conclusion](#task-8--conclusion)

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

<img width="100" src="https://user-images.githubusercontent.com/51442719/180164398-5973d7da-e912-4599-9687-b12846990720.png">

- In addition to AV software, other host-based security solutions provide real-time protection to endpoint devices. 
- `Endpoint Detection and Response` (`EDR`) is a security solution that provides real-time protection based on behavioral analytics. 
- An antivirus application performs scanning, detecting, and removing malicious files. 
- On the other hand, EDR monitors various security checks in the target machine, including file activities, memory, network connections, Windows registry, processes, etc.

Modern Antivirus products are implemented to integrate the traditional Antivirus features and other advanced functionalities (similar to EDR functionalities) into one product to provide comprehensive protection against digital threats.

For more information about Host-based security solutions, we suggest visiting the THM room: [`The Lay of the Land`](https://tryhackme.com/room/thelayoftheland).

### AV software in the past and present
- McAfee Associates, Inc. 
  - started the first AV software implementation in 1987. 
  - It was called "VirusScan," and its main goal at that time was to remove a virus named "Brain" that infected John McAfee's computer. 
  - Later, other companies joined in the battle against viruses. 
  - AV software was called scanners, and they were command-line software that searched for malicious patterns in files. 
- Since then, things have changed. 
  - AV software nowadays uses a Graphical User Interface (GUI) to perform scans for malicious files and other tasks. 
  - Malware programs have also expanded in scope and now target victims on Windows and other operating systems. 
  - Modern AV software supports most devices and platforms, including Windows, Linux, macOS, Android, and iOS. 
  - Modern AV software has improved and become more intelligent and sophisticated, as they pack a bundle of versatile features, including Antivirus, Anti-Exploit, Firewall, Encryption tool, etc.

- We will be discussing some AV features in the next task.

### Answer the questions below

- What was the virus name that infected John McAfee's PC?
  > Answer format: [`*****`](#Brain)
- Which PC Antivirus product was the first AV software on the market?
  > Answer format: [`******`](#McAfee)
- Antivirus software is a _____-based security solution.
  > Answer format: [`****`](#Host)

---

## Task 3  Antivirus Features

### Antivirus Engines
- An AV engine is responsible for finding and removing malicious code and files. 
- Good AV software implements an effective and solid AV core that accurately and quickly analyzes malicious files. 
- Also, It should handle and support various file types, including archive files, where it can self-extract and inspect all compressed files.
- Most AV products share the same common features but are implemented  differently, including but not limited to:
  - Scanner
  - Detection techniques
  - Compressors and Archives
  - Unpackers
  - Emulators

### Scanner
- The scanner feature is included in most AV products: AV software runs and scans in real-time or on-demand. 
- This feature is available in the GUI or through the command prompt. 
- The user can use it whenever required to check files or directories. 
- The scanning feature must support the most known malicious file types to detect and remove the threat. 
- In addition, it also may support other types of scanning depending on the AV software, including vulnerabilities, emails, Windows memory, and Windows Registry.
- An AV detection technique searches for and detects malicious files; different detection techniques can be used within the AV engine, including:
  - `Signature-based` detection is the traditional AV technique that looks for predefined malicious patterns and signatures within files.
  - `Heuristic` detection is a more advanced technique that includes various behavioral methods to analyze suspicious files.
  - `Dynamic` detection is a technique that includes monitoring the system calls and APIs and testing and analyzing in an isolated environment.
- We will cover these techniques in the next task. 
- A good AV engine is accurate and quickly detects malicious files with fewer false-positive results. 
- We will showcase several AV products that provide inaccurate results and misclassify a file.

### Compressors and Archives
- The "Compressors and Archives" feature should be included in any AV software. 
- It must support and be able to deal with various system file types, including compressed or archived files: ZIP, TGZ, 7z, XAR, RAR, etc. 
- Malicious code often tries to evade host-based security solutions by hiding in compressed files. 
- For this reason, AV software must decompress and scan through all files before a user opens a file within the archive.

### PE (Portable Executable) Parsing and Unpackers
- Malware hides and packs its malicious code by compressing and encrypting it within a payload. 
- It decompresses and decrypts itself during runtime to make it harder to perform static analysis. 
- Thus, AV software must be able to detect and unpack most of the known packers (UPX, Armadillo, ASPack, etc.) before the runtime for static analysis.

- Malware developers use various techniques, such as Packing, to shrink the size and change the malicious file's structure. 
- Packing compresses the original executable file to make it harder to analyze. 
- Therefore, AV software must have an unpacker feature to unpack protected or compressed executable files into the original code.

- Another feature that AV software must have is Windows Portable Executable (PE) header parser. 
- Parsing PE of executable files helps distinguish malicious and legitimate software (.exe files). 
- The PE file format in Windows (32 and 64 bits) contains various information and resources, such as object code, DLLs, icon files, font files, and core dumps.

### Emulators
- An emulator is an Antivirus feature that does further analysis on suspicious files. 
- Once an emulator receives a request, the emulator runs the suspect (exe, DLL, PDF, etc.) files in a virtualized and controlled environment. 
- It monitors the executable files' behavior during the execution, including the Windows APIs calls, Registry, and other Windows files. 
- The following are examples of the artifacts that the emulator may collect:
  - API calls
  - Memory dumps
  - Filesystem modifications
  - Log events
  - Running processes
  - Web requests
- An emulator stops the execution of a file when enough artifacts are collected to detect malware.

### Other common features
- The following are some common features found in AV products:
  - A self-protection driver to guard against malware attacking the actual AV.
  - Firewall and network inspection functionality.
  - Command-line and graphical interface tools.
  - A daemon or service.
  - A management console.

### Answer the questions below
- Which AV feature analyzes malware in a safe and isolated environment?
  > Answer format: [`********`](#Emulators)
- An _______ feature is a process of restoring or decrypting the compressed executable files to the original. 
  > Answer format: [`********`](#Unpackers)
- Read the above to proceed to the next task, where we discuss the AV detection techniques.
  > `No answer needed`

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
