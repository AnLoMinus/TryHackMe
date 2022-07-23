![image](https://user-images.githubusercontent.com/51442719/180161008-64a5b047-53f6-4d3c-8e37-621768a43b52.png)

- [ ] [Introduction to Antivirus](https://tryhackme.com/room/introtoav)
  > Understand how antivirus software works and what detection techniques are used to bypass malicious files checks.
    - [x] [Task 1  Introduction](#task-1--introduction)
    - [x] [Task 2  Antivirus Software](#task-2--antivirus-software)
    - [x] [Task 3  Antivirus Features](#task-3--antivirus-features)
    - [x] [Task 4  Deploy the VM](#task-4--deploy-the-vm)
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
- Generally speaking, AV detection can be classified into three main approaches:
  - `Static` Detection
  - `Dynamic` Detection
  - `Heuristic` and `Behavioral` Detection 

### Static Detection
- A static detection technique is the simplest type of Antivirus detection, which is based on predefined signatures of malicious files. 
- Simply, it uses pattern-matching techniques in the detection, such as finding a unique string, CRC (Checksums), sequence of bytecode/Hex values, and Cryptographic hashes (MD5, SHA1, etc.).
- It then performs a set of comparisons between existing files within the operating system and a database of signatures. 
- If the signature exists in the database, then it is considered malicious. 
- This method is effective against static malware.

![image](https://user-images.githubusercontent.com/51442719/180184875-6f35a756-2ee5-4ffa-ab88-49743ecfc85d.png)

- In this task, we will be using a signature-based detection method to see how antivirus products detect malicious files. 
- It is important to note that this technique works against known malicious files only with pre-generated signatures in a database. 
- Thus, the database needs to be updated from time to time.

- We will use the `ClamAV` antivirus software to demonstrate how signature-based detection identifies malicious files. 
- The `ClamAV` software is pre-installed in the provided VM, and we can access it in the following path: `c:\Program Files\ClamAV\clamscan.exe`. 
- We will also scan a couple of malware samples, which can be found on the desktop. 
- The Malware samples folder contains the following files:
  - `EICAR` is a test file containing ASCII strings used to test AV software's effectiveness instead of real malware that could damage your machine. 
    > For more information, you may visit the official EICAR website, [`Here`](https://www.eicar.org/?page_id=3950).
  - `Backdoor 1` is a C# program that uses a well-known technique to establish a reverse connection, including creating a process and executing a Metasploit Framework shellcode.
  - `Backdoor 2` is a C# program that uses process injection and encryption to establish a reverse connection, including injecting a Metasploit shellcode into an existing and running process.
  - `AV-Check` is a C# program that enumerates AV software in a target machine. 
    > Note that this file is not malicious. We will discuss this tool in more detail in task 6. 
  - `notes.txt` is a text file that contains a command line. 
    > Note that this file is not malicious.
- ClamAV comes with its database, and during the installation, we need to download the recently updated version. 
- Let's try to scan the Malware sample folder using the clamscan.exe binary and check how ClamAV performs against these samples.
```cmd
c:\>"c:\Program Files\ClamAV\clamscan.exe" c:\Users\thm\Desktop\Samples
Loading:    22s, ETA:   0s [========================>]    8.61M/8.61M sigs
Compiling:   4s, ETA:   0s [========================>]       41/41 tasks

C:\Users\thm\Desktop\Samples\AV-Check.exe: OK
C:\Users\thm\Desktop\Samples\backdoor1.exe: Win.Malware.Swrort-9872015-0 FOUND
C:\Users\thm\Desktop\Samples\backdoor2.exe: OK
C:\Users\thm\Desktop\Samples\eicar.com: Win.Test.EICAR_HDB-1 FOUND
C:\Users\thm\Desktop\Samples\notes.txt: OK
```
- The above output shows that ClamAV software correctly analyzed and flagged two of our tested files (EICAR, backdoor1, AV-Check, and notes.txt) as malicious. 
- However, it incorrectly identified the backdoor2 as non-malicious while it does.
- You can run `clamscan.exe --debug <file_to_scan>`, and you will see all modules loaded and used during the scanning. 
- For example, it uses the unpacking method to split the files and look for a predefined malicious sequence of bytecode values, and that is how it was able to detect the C# backdoor 1. 
- The bytecode value of the Metasploit shellcode used in backdoor 1 was previously identified and added to ClamAV's database. 
- However, backdoor 2 uses an encryption technique (XOR) for the Metasploit shellcode, resulting in different sequences of bytecode values that it doesn't find in the ClamAV database. 
- While the ClamAV was able to detect the EICAR.COM test file as malicious using the md5 signature-based technique. 
- To confirm this, we can re-scan the EICAR.COM test file again in debug mode (--debug). 
- At some point in the output, you will see the following message:
```cmd
LibClamAV debug: FP SIGNATURE: 44d88612fea8a8f36de82e1278abb02f:68:Win.Test.EICAR_HDB-1  # Name: eicar.com, Type: CL_TYPE_TEXT_ASCII
```
- Now let's generate the md5 value of the EICAR.COM if it matches what we see in the previous message from the output. 
- We will be using the `sigtool` for that: 
```cmd
c:\>"c:\Program Files\ClamAV\sigtool.exe" --md5 c:\Users\thm\Desktop\Samples\eicar.com
44d88612fea8a8f36de82e1278abb02f:68:eicar.com
```
- If you closely check the generated MD5 value, `44d88612fea8a8f36de82e1278abb02f`, it matches.

### Create Your Own Signature Database 
- One of ClamAV's features is creating your own database, allowing you to include items not found in the official ClamAV database. 
- Let's try to create a signature for Backdoor 2, which ClamAV already missed, and add it to a database. 
- The following are the required steps:
  - Generate an MD5 signature for the file.
  - Add the generated signature into a database with the extension "`.hdb`".
  - Re-scan the ClamAV against the file using our new database.
- First, we will be using the `sigtool` tool, which is included in the ClamAV suite, to generate an MD5 hash of `backdoor2.exe`  using the `--md5` argument.
```cmd
C:\Users\thm\Desktop\Samples>"c:\Program Files\ClamAV\sigtool.exe" --md5 backdoor2.exe
75047189991b1d119fdb477fef333ceb:6144:backdoor2.exe 
```
- As shown in the output, the generated hash string contains the following structure: `Hash:Size-in-byte:FileName`. 
- Note that ClamAV uses the generated value in the comparison during the scan.
- Now that we have the MD5 hash, now let's create our own database. 
- We will use the `sigtool` tool and save the output into a file using the > `thm.hdb` as follows,
```cmd
C:\Users\thm\Desktop\Samples>"c:\Program Files\ClamAV\sigtool.exe" --md5 backdoor2.exe > thm.hdb
```
- As a result, a `thm.hdb` file will be created in the current directory that executes the command. 
- We already know that ClamAV did not detect the backdoor2.exe using the official database! 
- Now, let's re-scan it using the database we created, `thm.hdb`, and see the result!
```cmd
C:\Users\thm\Desktop\Samples>"c:\Program Files\ClamAV\clamscan.exe" -d thm.hdb backdoor2.exe
Loading:     0s, ETA:   0s [========================>]        1/1 sigs
Compiling:   0s, ETA:   0s [========================>]       10/10 tasks

C:\Users\thm\Desktop\Samples\backdoor2.exe: backdoor2.exe.UNOFFICIAL FOUND
```
- As we expected, the ClamAV tool flagged the backdoor2.exe binary as malicious based on the database we provided. 
- As a practice, add the `AV-Check.exe`'s MD5 signature into the same database we already created, then check whether ClamAV can flag `AV-Check.exe` as malicious.

### Yara Rules for Static Detection
- One of the tools that help in static detection is [`Yara`](http://virustotal.github.io/yara/). 
- Yara is a tool that allows malware engineers to classify and detect malware. 
- Yara uses rule-based detection, so in order to detect new malware, we need to create a new rule. 
- ClamAV can also deal with Yara rules to detect malicious files. 
- The rule will be the same as in our database in the previous section. 
- To create a rule, we need to examine and analyze the malware; based on the findings, we write a rule. 
- Let's take `AV-Check.exe` as an example and write a rule for it. 
- First, let's analyze the file and list all human-readable strings in the binary using the strings tool. 
- As a result, we will see all functions, variables, and nonsense strings. 
- But, if you look closely, we can use some of the unique strings in our rules to detect this file in the future. 
- The AV-Check uses a program database (`.pdb`), which contains a type and symbolic debugging information of the program during the compiling.
```powershell
C:\Users\thm\Desktop\Samples>strings AV-Check.exe | findstr pdb
C:\Users\thm\source\repos\AV-Check\AV-Check\obj\Debug\AV-Check.pdb
```
- We will use the path in the previous command's output as our unique string example in the Yara rule that we will create. 
- The signature could be something else in the real world, such as Registry keys, commands, etc. 
- If you are not familiar with Yara, then we suggest checking the Yara THM room. 
- The following is Yara's rule that we will use in our detection:
```yara
rule thm_demo_rule {
	meta:
		author = "THM: Intro-to-AV-Room"
		description = "Look at how the Yara rule works with ClamAV"
	strings:
		$a = "C:\\Users\\thm\\source\\repos\\AV-Check\\AV-Check\\obj\\Debug\\AV-Check.pdb"
	condition:
		$a
}
```
- Let's explain this Yara's rule a bit more.
  - The rule starts with `rule thm_demo_rule`, which is the name of our rule. 
  - ClamAV uses this name if a rule matches.
  - The metadata section, which is general information, contains the author and description, which the user can fill.
  - The strings section contains the strings or bytecode that we are looking for. 
  - We are using the C# program's database path in this case. 
  - Notice that we add an extra `\` in that path to escape the special character, so it does not break the rule. 
  - In the condition section, we specify if the defined string is found in the string section, then flag the file.
- Note that Yara rules must store in a `.yara` extension file for ClamAV to deal with it. 
- Let's re-scan the `c:\Users\thm\Desktop\Samples` folder again using the Yara rule we created. 
- You can find a copy of the Yara rule on the desktop at `c:\Users\thm\Desktop\Files\thm-demo-1.yara`.
```powershell
C:\Users\thm>"c:\Program Files\ClamAV\clamscan.exe" -d Desktop\Files\thm-demo-1.yara Desktop\Samples
Loading:     0s, ETA:   0s [========================>]        1/1 sigs
Compiling:   0s, ETA:   0s [========================>]       40/40 tasks

C:\Users\thm\Desktop\Samples\AV-Check.exe: YARA.thm_demo_rule.UNOFFICIAL FOUND
C:\Users\thm\Desktop\Samples\backdoor1.exe: OK
C:\Users\thm\Desktop\Samples\backdoor2.exe: OK
C:\Users\thm\Desktop\Samples\eicar.com: OK
C:\Users\thm\Desktop\Samples\notes.txt: YARA.thm_demo_rule.UNOFFICIAL FOUND
```
- As a result, ClamAV can detect the `AV-Check.exe` binary as malicious based on the Yara rule we provide. 
- However, ClamAV gave a false-positive result where it flagged the `notes.txt` file as malicious. 
- If we open the `notes.txt` file, we can see that the text contains the same path we specified in the rule.
- Let's improve our Yara rule to reduce the false-positive result. We will be specifying the file type in our rule. 
- Often, the types of a file can be identified using magic numbers, which are the first two bytes of the binary. 
- For example, [`executable`](https://en.wikipedia.org/wiki/DOS_MZ_executable) files (.exe) always start with the ASCII "MZ" value or "4D 5A" in hex.
- To confirm this, let's use the [`HxD`](https://mh-nexus.de/en/hxd/) application, which is a freeware Hex Editor, to examine the AV-Check.exe binary and see the first two bytes. 
  > Note that the HxD is already available in the provided VM.
![image](https://user-images.githubusercontent.com/51442719/180619558-f18da962-f4b6-4b38-8be5-223f1b263650.png)
- Knowing this will help improve the detection, let's include this in our Yara rule to flag only the .exe files that contain our signature string as malicious. 
- The following is the improved Yara rule:
```yara
rule thm_demo_rule {
	meta:
		author = "THM: Intro-to-AV-Room"
		description = "Look at how the Yara rule works with ClamAV"
	strings:
		$a = "C:\\Users\\thm\\source\\repos\\AV-Check\\AV-Check\\obj\\Debug\\AV-Check.pdb"
		$b = "MZ"
	condition:
		$b at 0 and $a
}
```
- In the new Yara rule, we defined a unique string ($b) equal to the MZ as an identifier for the .exe file type. 
- We also updated the condition section, which now includes the following conditions:
  - If the string "MZ" is found at the 0 location, the file's beginning.
  - If the unique string (the path) occurs within the binary.
  - In the condition section, we used the `AND` operator for both definitions in 1 and 2 are found, then we have a match. 
- You can find the updated rule in `Desktop\Files\thm-demo-2.yara`. 
- Now that we have our updated Yara rule, now let's try it again.
```powershell
C:\Users\thm>"c:\Program Files\ClamAV\clamscan.exe" -d Desktop\Files\thm-demo-2.yara Desktop\Samples
Loading:     0s, ETA:   0s [========================>]        1/1 sigs
Compiling:   0s, ETA:   0s [========================>]       40/40 tasks

C:\Users\thm\Desktop\Samples\AV-Check.exe: YARA.thm_demo_rule.UNOFFICIAL FOUND
C:\Users\thm\Desktop\Samples\backdoor1.exe: OK
C:\Users\thm\Desktop\Samples\backdoor2.exe: OK
C:\Users\thm\Desktop\Samples\eicar.com: OK
C:\Users\thm\Desktop\Samples\notes.txt: OK
```
- The output shows we improved our Yara rule to reduce the false-positive results. 
- That was a simple example of how AV software works. 
- Thus, AV software vendors work hard to fight against malware and improve their products and database to enhance the performance and accuracy of results.
- The drawback of the signature-based detection is that files will have a different hash value if the binary is modified. 
- Therefore, it is easy for someone to bypass signature-based detection techniques if they know what AV software looks for and how to analyze binaries, as shown in later rooms.

### Answer the questions below
- What is the sigtool tool output to generate an MD5 of the AV-Check.exe binary?
  > Answer format: [`********************************:****:********.***`](#f4a974b0cf25dca7fbce8701b7ab3a88:6144:AV-Check,exe)
- Use the strings tool to list all human-readable strings of the AV-Check binary. What is the flag?
  > Answer format: [`***{**************}`](#THM{Y0uC4nC-5tr16s})
  
---

## Task 6  Other Detection Techniques

---

## Task 7  AV Testing and Fingerprinting

---

## Task 8  Conclusion
