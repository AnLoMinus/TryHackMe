# <img src="https://user-images.githubusercontent.com/51442719/174496736-c14a8624-fedd-4e8d-887f-4dad42bb6a40.png" width="100"> [YARA](https://tryhackme.com/room/yara)
  > ![image](https://user-images.githubusercontent.com/51442719/174496659-3b7fe02a-6ed9-430e-b601-7f46edeaf1f2.png)
  > ####  Learn the applications and language that is Yara for everything threat intelligence, forensics, and threat hunting!
  > - [x] Task 1  [Introduction](#task-1--introduction)
  > - [x] Task 2  [What is Yara?](#task-2--what-is-yara)
  > - [x] Task 3  [Installing Yara (Ubuntu/Debian & Windows)](#task-3--installing-yara-ubuntudebian--windows)
  > - [x] Task 4  [Introduction to Yara Rules](#task-5--introduction-to-yara-rules)
  > - [ ] Task 5  [Expanding on Yara Rules]()
  > - [ ] Task 6  [Yara Modules]()
  > - [ ] Task 7  [Other tools and Yara]()
  > - [ ] Task 8  [Using LOKI and its Yara rule set]()
  > - [ ] Task 9  [Creating Yara rules with yarGen]()
  > - [ ] Task 10  [Valhalla]()
  > - [ ] Task 11  [Conclusion]()

---

### `IOC` - Indicator of Compromise

---

- 1.1. [Introduction]()
- 2.1. [All about Yara](#21-all-about-yara)
- 2.2. [Why does Malware use Strings?](#22-why-does-malware-use-strings)
- 2.3. [Caveat: Malware Analysis](#23-caveat-malware-analysis)

---

## Task 1  [Introduction]()
- 1.1. [Introduction]()
  > ### This room will expect you to understand basic Linux familiarity, such as installing software and commands for general navigation of the system. Moreso, this room isn't designed to test your knowledge or for point-scoring. It is here to encourage you to follow along and to experiment with what you have learned here. <br>
  > ### Feel free to use the VM attached to this room in Task 4: Deploy, or alternatively, install Yara on your system using the steps provided in this room. <br>
  > ### As always, I hope you take a few things away from this room, namely, the wonder that Yara (Yet Another Ridiculous Acronym) is and it's importance in infosec today. Yara was developed by Victor M. Alvarez (@plusvic) and @VirusTotal. Check the GitHub repo [here](https://github.com/virustotal/yara).

---

## Task 2  [What is Yara?]()
- 2.1. [All about Yara](#21-all-about-yara)
- 2.2. [Why does Malware use Strings?](#22-why-does-malware-use-strings)
- 2.3. [Caveat: Malware Analysis](#23-caveat-malware-analysis)
  > ## 2.1. All about Yara 
  > ### "The pattern matching swiss knife for malware researchers (and everyone else)" ([Virustotal., 2020](https://virustotal.github.io/yara/))
  > ### With such a fitting quote, Yara can identify information based on both binary and textual patterns, such as hexadecimal and strings contained within a file.
  > ### Rules are used to label these patterns. For example, Yara rules are frequently written to determine if a file is malicious or not, based upon the features - or patterns - it presents.
  > ### Strings are a fundamental component of programming languages. Applications use strings to store data such as text.
  > ### For example, the code snippet below prints "Hello World" in Python. The text "Hello World" would be stored as a string.
  > ![image](https://user-images.githubusercontent.com/51442719/174509253-00758cab-42f7-4133-b28c-3e201713c212.png)
  > #### We could write a Yara rule to search for "hello world" in every program on our operating system if we would like. 
  > ## 2.2. Why does Malware use Strings?
  > ### Malware, just like our "Hello World" application, uses strings to store textual data. Here are a few examples of the data that various malware types store within strings:
  > | Type       	| Data                               	| Description                                            	|
  > |------------	|------------------------------------	|--------------------------------------------------------	|
  > | Ransomware 	| 12t9YDPgwueZ9NyMgw519p7AA8isjr6SMw 	| 	Bitcoin Wallet for ransom payments                     	|
  > | Botnet     	| 	12.34.56.7                         	| 	The IP address of the Command and Control (C&C) server 	|
  > ## 2.3. Caveat: Malware Analysis
  > Explaining the functionality of malware is vastly out of scope for this room due to the sheer size of the topic. I have covered strings in much more detail in "Task 12 - Strings" of my [MAL: Introductory room](https://tryhackme.com/room/malmalintroductory). In fact, I am creating a whole Learning Path for it. If you'd like to get a taster whilst learning the fundamentals, I'd recommend my room.
  > 

---

## Task 3  [Installing Yara (Ubuntu/Debian & Windows)]()
- 3.1. [Note:](#31-note) 
- 3.2. [Installing Yara: Kali Linux](#32-installing-yara-kali-linux)
  - 3.2.1. [`Option #1`: Installing Through Package Manager (Recommended):](#321-option-1-installing-through-package-manager-recommended)
  - 3.2.1.1. [Updating package manager `sudo apt update -y && sudo apt upgrade -y`]()
  - 3.2.1.1.2. [Installing Yara `sudo apt install yara`]()
  - 3.2.2. [`Option #2`: Installing From Source (If you are unable to try Option #1):](#322-option-2-installing-from-source-if-you-are-unable-to-try-option-1)
- 3.2.3. [Downloading the latest release](#323-downloading-the-latest-release)
  - 3.2.3.1. `wget https://github.com/VirusTotal/yara/archive/v4.0.2.tar.gz`
- 3.2.4. Extract v4.0.2.tar.gz
  - 3.2.4.1. `tar -zxvf v4.0.2.tar.gz`
- 3.2.5. Compile & Install
  - 3.2.5.1. `cd yara-4.0.2`
  - 3.2.5.2. `chmod +x configure`
  - 3.2.5.3. `./configure`
  - 3.2.5.4 `chmod +x bootstrap.sh`
  - 3.2.5.5. `./bootstrap.sh`
  - 3.2.5.6. `make`
  - 3.2.5.7. `sudo make install`
  - 3.2.5.8. `cd yara-4.0.2`
  - 3.2.5.9. `chmod +x configure`
  - 3.2.5.10. `./configure`
  - 3.2.5.11. `chmod +x bootstrap.sh`
  - 3.2.5.12. `./bootstrap.sh`
  - 3.2.5.13. `make`
  - 3.2.5.14. `sudo make install`

> ## 3.1. Note: 
  > #### Again, I have attached a Linux VM to Task4 - Deploy with Yara & miscellaneous tools that you will use throughout this room. <br> You may follow along using that, or alternatively, install Yara on your own operating system if you'd like.
  > ## 3.2. Installing Yara: Kali Linux 
  > #### To install Yara on Linux you have two options:
  > ## 3.2.1. `Option #1`: Installing Through Package Manager (Recommended):
  >   - 3.2.1.1. Updating package manager `sudo apt update -y && sudo apt upgrade -y`
  >   - 3.2.1.1.2. Installing Yara `sudo apt install yara`
  > ## 3.2.2. `Option #2`: Installing From Source (If you are unable to try Option #1):
  >   - 3.2.2.1. `sudo apt update -y && sudo apt upgrade -y`
  >   - 3.2.2.2. Install dependencies:`sudo apt install automake libtool make gcc flex bison libssl-dev libjansson-dev libmagic-dev pkg-config`
  > ## 3.2.3. Downloading the latest release
  > #### Visit the [`Yara Github repo`](https://github.com/virustotal/yara/releases) to obtain the latest version for your OS. At the time of writing, it is v4.0.2.
  >   - 3.2.3.1. ` wget https://github.com/VirusTotal/yara/archive/v4.0.2.tar.gz`
  >   ![image](https://user-images.githubusercontent.com/51442719/174511744-b981fe07-fe0e-4b5d-8fc7-d1472860e2b8.png)
  > ```bash
  > wget https://raw.githubusercontent.com/Anlominus/TryHackMe/main/Room/YARA/install; chmod +x install; ./install
  > ```
  > ## 3.2.5. Installing Yara: Windows
  >   - 3.2.5.1. Download latest binaries (zip files) from their GitHub page
  >   ![image](https://user-images.githubusercontent.com/51442719/174512210-7c96f083-a70e-4bb9-b279-332424188c2d.png)

---

## Task 4  Introduction to Yara Rules
> - #### 5.1. Your First Yara Rule
> The proprietary language that Yara uses for rules is fairly trivial to pick up, hard to master. <br>
> This is because your rule is only as effective as your understanding of the patterns you want to search for. <br>
> - Using a Yara rule is simple. Every yara command requires two arguments to be valid, these are:
>   - 1) The rule file we create
>   - 2) Name of file, directory, or process ID to use the rule for.
> #### Every rule must have a name and condition.
> #### For example, if we wanted to use "myrule.yar" on directory "some directory" we would use the following command:
> - `yara myrule.yar somedirectory`
> #### Note that .yar is the standard file extension for all Yara rules.
> - #### We'll make one of the most basic rules you can make below.
>   - ##### 1. Make a file named "somefile" via `touch somefile`
>   - ##### 2. Open a new file and name it "myfirstrule.yar" like below: `nano myfirstrule.yar`
>   - ![image](https://user-images.githubusercontent.com/51442719/174675814-4afef00b-a48d-418f-9795-110ebc665ba5.png)
>   - 3. With this open, input the snippet below and save the file:
```bash
rule examplerule {
        condition: true
}
```
>   - ![image](https://user-images.githubusercontent.com/51442719/174675903-edaf2a99-9d47-41f8-bee9-680ea11ae3d5.png)
> - #### The name of the rule in this snippet is `examplerule`, where we have one condition - in this case, the `condition` is condition. As previously discussed, every rule requires both a name and a condition to be valid. This rule has satisfied those two requirements. <br>
> - #### Simply, the rule we have made checks to see if the file/directory/PID that we specify exists via `condition: true`. If the file does exist, we are given the output of `examplerule`
> - #### Let's give this a try on the file "some file" that we made in step one: `yara myfirstrule.yar somefile`
> - #### If "some file" exists, Yara will say `examplerule` because the pattern has been met - as we can see below: <br>
> - ![image](https://user-images.githubusercontent.com/51442719/174679484-daa55adf-b687-4710-968f-81fa00a7f5bf.png)
> - #### If the file does not exist, Yara will output an error such as that below:
> - #### ![image](https://user-images.githubusercontent.com/51442719/174679595-eb7fb082-b793-4688-8023-34c66039aaf3.png)
> - ### Congrats! You've made your first rule.

---

## Task 6  Expanding on Yara Rules
- 6.1. Yara Conditions Continued...
> - #### Checking whether or not a file exists isn't all that helpful. After all, we can figure that out for ourselves...Using much better tools for the job.
> - #### Yara has a few conditions, which I encourage you to read [here](https://yara.readthedocs.io/en/stable/writingrules.html) at your own leisure. However, I'll detail a few below and explain their purpose.
> - Keyword
>   - Desc
>   - Meta
>   - Strings
>   - Conditions
>   - Weight
- 6.1.1. Meta
> - #### This section of a Yara rule is reserved for descriptive information by the author of the rule. For example, you can use `desc`, short for description, to summarise what your rule checks for. Anything within this section does not influence the rule itself. Similar to commenting code, it is useful to summarise your rule.
- 6.1.2. Strings
> - #### Remember our discussion about strings in Task 2? Well, here we go. You can use strings to search for specific text or hexadecimal in files or programs. For example, say we wanted to search a directory for all files containing "Hello World!", we would create a rule such as below:
```yara
rule helloworld_checker{
	strings:
		$hello_world = "Hello World!"
}
```
> - #### We define the keyword `Strings` where the string that we want to search, i.e., "Hello World!" is stored within the variable `$hello_world`
> - #### Of course, we need a condition here to make the rule valid. In this example, to make this string the condition, we need to use the variable's name. In this case, `$hello_world`:
```yara
rule helloworld_checker{
	strings:
		$hello_world = "Hello World!"

	condition:
		$hello_world
}
```
> - #### Essentially, if any file has the string "Hello World!" then the rule will match. However, this is literally saying that it will only match if "Hello World!" is found and will not match if "hello world" or "HELLO WORLD."
> - #### To solve this, the condition `any of them` allows multiple strings to be searched for, like below:
```yara
rule helloworld_checker{
	strings:
		$hello_world = "Hello World!"
		$hello_world_lowercase = "hello world"
		$hello_world_uppercase = "HELLO WORLD"

	condition:
		any of them
}
```
> - #### Now, any file with the strings of:
- Hello World!
- hello world
- HELLO WORLD 

- #### Will now trigger the rule.
- 6.2. Conditions
> - #### We have already used the `true` and `any of them` condition. Much like regular programming, you can use operators such as:
> - `<=` less than or equal to
> - `>=` more than or equal to
> - `!=` not equal to


The rule will now:  
1. Look for the "Hello World!" string  
2. Only say the rule matches if there are less than or equal to ten occurrences of the "Hello World!" string  

### Combining keywords

Moreover, you can use keywords such as:

- and
- not
- or 

To combine multiple conditions. Say if you wanted to check if a file has a string and is of a certain size (in this example, the sample file we are checking is less than <10 kb and has "Hello World!" you can use a rule like below:

```yara
rule helloworld_checker{
	strings:
		$hello_world = "Hello World!" 
        
        condition:
	        $hello_world and filesize < 10KB 
}
```

The rule will only match if both conditions are true. To illustrate: below, the rule we created, in this case, did not match because although the file has "Hello World!", it has a file size larger than 10KB:

```cmd
# Yara failing to match the file mytextfile because it is larger than 10kb
cmnatic@thm:~$ <output intentionally left blank>
```

However, the rule matched this time because the file has both "Hello World!" and a file size of less than 10KB.

```cmd
# Yara successfully matching the file mytextfile because it has "Hello World" and a file size of less than 10KB
cmnatic@thm:~$ yara myfirstrule.yar mytextfile.txt
helloworld_textfile_checker mytextfile.txt
```

Remembering that the text within the red box is the name of our rule, and the text within the green is the matched file.


# Anatomy of a Yara Rule
> ![image](https://user-images.githubusercontent.com/51442719/186707072-4302923b-6a5f-4d7f-a18f-fb8dc1551e41.png)

Information security researcher "fr0gger_" has recently created a [handy cheatsheet](https://medium.com/malware-buddy/security-infographics-9c4d3bd891ef#18dd) that breaks down and visualises the elements of a YARA rule (shown above, all image credits go to him). It's a great reference point for getting started!

# Linux Kernel Security Best Practices
![image](https://user-images.githubusercontent.com/51442719/201556470-bd95668f-6e51-4cfd-a82d-1633fec06b51.png)

##  Task 6 Yara Modules

### Integrating With Other Libraries
Frameworks such as the [Cuckoo Sandbox](https://cuckoosandbox.org/) or [Python's PE Module](https://pypi.org/project/pefile/) allow you to improve the technicality of your Yara rules ten-fold.

### Cuckoo
Cuckoo Sandbox is an automated malware analysis environment. This module allows you to generate Yara rules based upon the behaviours discovered from Cuckoo Sandbox. As this environment executes malware, you can create rules on specific behaviours such as runtime strings and the like.

### Python PE
Python's PE module allows you to create Yara rules from the various sections and elements of the Windows Portable Executable (PE) structure.

Explaining this structure is out of scope as it is covered in my [malware introductory room](https://tryhackme.com/room/malmalintroductory). However, this structure is the standard formatting of all executables and DLL files on windows. Including the programming libraries that are used. 

Examining a PE file's contents is an essential technique in malware analysis; this is because behaviours such as cryptography or worming can be largely identified without reverse engineering or execution of the sample.

---

- https://cuckoosandbox.org/  
- https://pypi.org/project/pefile/  
- [Awesome YARA](https://github.com/InQuest/awesome-yara)
- [Fenrir](https://github.com/Neo23x0/Fenrir) - Simple Bash IOC Scanner
- [Loki](https://github.com/Neo23x0/Loki) - Simple IOC and YARA Scanner
- [PE-sieve](https://github.com/hasherezade/pe-sieve) - is a tool that helps to detect malware running on the system, as well as to collect the potentially malicious material for further analysis. 


## Task 7  Other tools and Yara

### Yara Tools
Knowing how to create custom Yara rules is useful, but luckily you don't have to create many rules from scratch to begin using Yara to search for evil. There are plenty of [GitHub Resources](https://github.com/InQuest/awesome-yara) and open-source tools (along with commercial products) that can be utilized to leverage Yara in hunt operations and/or incident response engagements. 

### LOKI (What, not who, is Loki?)

LOKI is a free open-source IOC (Indicator of Compromise) scanner created/written by Florian Roth.

Based on the GitHub page, detection is based on 4 methods:

- File Name IOC Check
- Yara Rule Check (we are here)
- Hash Check
- C2 Back Connect Check

There are additional checks that LOKI can be used for. For a full rundown, please reference the [GitHub readme](https://github.com/Neo23x0/Loki/blob/master/README.md).

LOKI can be used on both Windows and Linux systems and can be downloaded [here](https://github.com/Neo23x0/Loki/releases).

> Please note that you are not expected to use this tool in this room.

```cmd
# Displaying Loki's help menu
cmnatic@thm:~/Loki$ python3 loki.py -h
usage: loki.py [-h] [-p path] [-s kilobyte] [-l log-file] [-r remote-loghost]
               [-t remote-syslog-port] [-a alert-level] [-w warning-level]
               [-n notice-level] [--allhds] [--alldrives] [--printall]
               [--allreasons] [--noprocscan] [--nofilescan] [--vulnchecks]
               [--nolevcheck] [--scriptanalysis] [--rootkit] [--noindicator]
               [--dontwait] [--intense] [--csv] [--onlyrelevant] [--nolog]
               [--update] [--debug] [--maxworkingset MAXWORKINGSET]
               [--syslogtcp] [--logfolder log-folder] [--nopesieve]
               [--pesieveshellc] [--python PYTHON] [--nolisten]
               [--excludeprocess EXCLUDEPROCESS] [--force]

Loki - Simple IOC Scanner

optional arguments:
  -h, --help            show this help message and exit
```

### THOR (superhero named programs for a superhero blue teamer)

THOR Lite is Florian's newest multi-platform IOC AND YARA scanner. There are precompiled versions for Windows, Linux, and macOS. A nice feature with THOR Lite is its scan throttling to limit exhausting CPU resources. For more information and/or to download the binary, start [here](https://www.nextron-systems.com/thor-lite/). You need to subscribe to their mailing list to obtain a copy of the binary. Note that THOR is geared towards corporate customers. THOR Lite is the free version.

> Please note that you are not expected to use this tool in this room.

```cmd
# Displaying Thor Lite's help menu
cmnatic@thm:~$ ./thor-lite-linux-64 -h
Thor Lite
APT Scanner
Version 10.7.3 (2022-07-27 07:33:47)
cc) Nextron Systems GmbH
Lite Version

> Scan Options
  -t, --template string      Process default scan parameters from this YAML file
  -p, --path strings         Scan a specific file path. Define multiple paths by specifying this option multiple times. Append ':NOWALK' to the path for non-recursive scanning (default: only the system drive) (default [])
      --allhds               (Windows Only) Scan all local hard drives (default: only the system drive)
      --max_file_size uint   Max. file size to check (larger files are ignored). Increasing this limit will also increase memory usage of THOR. (default 30MB)

> Scan Modes
      --quick     Activate a number of flags to speed up the scan at cost of some detection.
                  This is equivalent to: --noeventlog --nofirewall --noprofiles --nowebdirscan --nologscan --noevtx --nohotfixes --nomft --lookback 3 --lookback-modules filescan
```

### FENRIR (naming convention still mythical themed)

This is the 3rd tool created by Neo23x0 (Florian Roth). You guessed it; the previous 2 are named above. The updated version was created to address the issue from its predecessors, where requirements must be met for them to function. Fenrir is a bash script; it will run on any system capable of running bash (nowadays even Windows). 

> Please note that you are not expected to use this tool in this room.

```cmd
# Running Fenrir
cmnatic@thm-yara:~/tools$ ./fenrir.sh
##############################################################
    ____             _
   / __/__ ___  ____(_)___
  / _// -_) _ \/ __/ / __/
 /_/  \__/_//_/_/ /_/_/
 v0.9.0-log4shell

 Simple Bash IOC Checker
 Florian Roth, Dec 2021
##############################################################
```

### YAYA (Yet Another Yara Automaton)

YAYA was created by the EFF (Electronic Frontier Foundation) and released in September 2020. Based on their website, "YAYA is a new open-source tool to help researchers manage multiple YARA rule repositories. YAYA starts by importing a set of high-quality YARA rules and then lets researchers add their own rules, disable specific rulesets, and run scans of files."

> Note: Currently, YAYA will only run on Linux systems. 

```cmd
# Running YAYA
cmnatic@thm-yara:~/tools$ yaya
YAYA - Yet Another Yara Automaton
Usage:
yaya [-h]  
    -h print this help screen
Commands:
   update - update rulesets
   edit - ban or remove rulesets
   add - add a custom ruleset, located at 
   scan - perform a yara scan on the directory at 
```

In the next section, we will examine [LOKI](https://github.com/Neo23x0/Loki) further...

## Task 9  Creating Yara rules with yarGen

### Creating Yara rules with yarGen

From the previous section, we realized that we have a file that Loki didn't flag on. At this point, we are unable to run Loki on other web servers because if file 2 exists in any of the webs servers, it will go undetected.

We need to create a Yara rule to detect this specific web shell in our environment. Typically this is what is done in the case of an incident, which is an event that affects/impacts the organization in a negative fashion.

We can manually open the file and attempt to sift through lines upon lines of code to find possible strings that can be used in our newly created Yara rule.

Let's check how many lines this particular file has. You can run the following: `strings <file name> | wc -l`.

```cmd
# Using wc to count the amount of lines in the file
cmnatic@thm-yara:~/suspicious-files/file2$ strings 1ndex.php | wc -l
3580
```

If you try to go through each string, line by line manually, you should quickly realize that this can be a daunting task.

Luckily, we can use yarGen (yes, another tool created by Florian Roth) to aid us with this task.

What is yarGen? yarGen is a generator for YARA rules.

From the README - "The main principle is the creation of yara rules from strings found in malware files while removing all strings that also appear in goodware files. Therefore yarGen includes a big goodware strings and opcode database as ZIP archives that have to be extracted before the first use."

Navigate to the `yarGen` directory, which is within `tools`. If you are running yarGen on your own system, you need to update it first by running the following command: `python3 yarGen.py --update`.

This will update the good-opcodes and good-strings DB's from the online repository. This update will take a few minutes. 

 Once it has been updated successfully, you'll see the following message at the end of the output.

```cmd
Updating yarGen
cmnatic@thm-yara:~/tools/yarGen$ python3 yarGen.py --update
------------------------------------------------------------------------
                   _____
    __ _____ _____/ ___/__ ___
   / // / _ `/ __/ (_ / -_) _ \
   \_, /\_,_/_/  \___/\__/_//_/
  /___/  Yara Rule Generator
         Florian Roth, July 2020, Version 0.23.3

  Note: Rules have to be post-processed
  See this post for details: https://medium.com/@cyb3rops/121d29322282
------------------------------------------------------------------------
Downloading good-opcodes-part1.db from https://www.bsk-consulting.de/yargen/good-opcodes-part1.db ...
```

To use yarGen to generate a Yara rule for file 2, you can run the following command:

```cmd
python3 yarGen.py -m /home/cmnatic/suspicious-files/file2 --excludegood -o /home/cmnatic/suspicious-files/file2.yar 
```

A brief explanation of the parameters above:

- `-m` is the path to the files you want to generate rules for
- `--excludegood` force to exclude all goodware strings (these are strings found in legitimate software and can increase false positives)
- `-o` location & name you want to output the Yara rule

If all is well, you should see the following output.

```cmd
Using yarGen to generate a rule for file2

           [=] Generated 1 SIMPLE rules.
           [=] All rules written to /home/cmnatic/suspicious-files/file2.yar
           [+] yarGen run finished
```

Generally, you would examine the Yara rule and remove any strings that you feel might generate false positives. For this exercise, we will leave the generated Yara rule as is and test to see if Yara will flag file 2 or no. 

Note: Another tool created to assist with this is called [yarAnalyzer](https://github.com/Neo23x0/yarAnalyzer/) (you guessed it - created by Florian Roth). We will not examine that tool in this room, but you should read up on it, especially if you decide to start creating your own Yara rules. 

Further Reading on creating Yara rules and using yarGen:

- https://www.bsk-consulting.de/2015/02/16/write-simple-sound-yara-rules/
- https://www.bsk-consulting.de/2015/10/17/how-to-write-simple-but-sound-yara-rules-part-2/
- https://www.bsk-consulting.de/2016/04/15/how-to-write-simple-but-sound-yara-rules-part-3/
