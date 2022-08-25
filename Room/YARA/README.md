# <img src="https://user-images.githubusercontent.com/51442719/174496736-c14a8624-fedd-4e8d-887f-4dad42bb6a40.png" width="100"> [YARA](https://tryhackme.com/room/yara)
  > ![image](https://user-images.githubusercontent.com/51442719/174496659-3b7fe02a-6ed9-430e-b601-7f46edeaf1f2.png)
  > ####  Learn the applications and language that is Yara for everything threat intelligence, forensics, and threat hunting!
  > - [x] Task 1  [Introduction](#task-1--introduction)
  > - [x] Task 2  [What is Yara?](#task-2--what-is-yara)
  > - [x] Task 3  [Installing Yara (Ubuntu/Debian & Windows)](#task-3--installing-yara-ubuntudebian--windows)
  > - [x] Task 4  [Deploy](#task-4--deploy)
  > - [x] Task 5  [Introduction to Yara Rules](#task-5--introduction-to-yara-rules)
  > - [ ] Task 6  [Expanding on Yara Rules]()
  > - [ ] Task 7  [Yara Modules]()
  > - [ ] Task 8  [Other tools and Yara]()
  > - [ ] Task 9  [Using LOKI and its Yara rule set]()
  > - [ ] Task 10  [Creating Yara rules with yarGen]()
  > - [ ] Task 11  [Valhalla]()
  > - [ ] Task 12  [Conclusion]()

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

## Task 4  Deploy
- 4.1. In-Browser (No  VPN required)
- 4.2. Using SSH (TryHackMe VPN required).
> - IP Address: `MACHINE_IP`
> - Username: `cmnatic`
> - Password: `yararules!`
> - SSH Port: `22`

---

## Task 5  Introduction to Yara Rules
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
> - ![image](https://user-images.githubusercontent.com/51442719/174680206-fd1b001b-abc6-4be0-99c6-732b3641ac50.png)
> - #### We define the keyword `Strings` where the string that we want to search, i.e., "Hello World!" is stored within the variable `$hello_world`
> - #### Of course, we need a condition here to make the rule valid. In this example, to make this string the condition, we need to use the variable's name. In this case, `$hello_world`:
> - ![image](https://user-images.githubusercontent.com/51442719/174680284-328255f2-0c2f-40cb-850b-e39f71ea614e.png)
> - #### Essentially, if any file has the string "Hello World!" then the rule will match. However, this is literally saying that it will only match if "Hello World!" is found and will not match if "hello world" or "HELLO WORLD."
> - #### To solve this, the condition `any of them` allows multiple strings to be searched for, like below:
> - ![image](https://user-images.githubusercontent.com/51442719/174680342-91907bea-e5f2-4fb6-aac8-4e8d2c9b2303.png)
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

# Anatomy of a Yara Rule
> ![image](https://user-images.githubusercontent.com/51442719/186707072-4302923b-6a5f-4d7f-a18f-fb8dc1551e41.png)


##  Task 7 Yara Modules

- https://cuckoosandbox.org/  
- https://pypi.org/project/pefile/  
- [Awesome YARA](https://github.com/InQuest/awesome-yara)
- [Fenrir](https://github.com/Neo23x0/Fenrir) - Simple Bash IOC Scanner
- [Loki](https://github.com/Neo23x0/Loki) - Simple IOC and YARA Scanner
- [PE-sieve](https://github.com/hasherezade/pe-sieve) - is a tool that helps to detect malware running on the system, as well as to collect the potentially malicious material for further analysis. 


