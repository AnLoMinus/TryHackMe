# [Password Attacks](https://tryhackme.com/room/passwordattacks)

- [x] [Task 1  Introduction](#task-1--introduction)
- [x] [Task 2  Password Attacking Techniques](#task-2--password-attacking-techniques)
- [x] [Task 3  Password Profiling #1 - Default, Weak, Leaked, Combined , and Username Wordlists](#task-3--password-profiling-1---default-weak-leaked-combined--and-username-wordlists)
- [ ] [Task 4  Password Profiling #2 - Keyspace Technique and CUPP](#)
- [ ] [Task 5  Offline Attacks - Dictionary and Brute-Force](#)
- [ ] [Task 6  Offline Attacks - Rule-Based](#)
- [ ] [Task 7  Deploy the VM](#)
- [ ] [Task 8  Online password attacks](#)
- [ ] [Task 9  Password spray attack](#)
- [x] [Task 10  Summary](#)

---

# [Task 1  Introduction](#)



#### This room introduces the fundamental techniques to perform a successful password attack against various services and scenarios.
- Password profiling
- Password attacks techniques
- Online password attacks

## What is a password?
Passwords are used as an authentication method for individuals to access computer systems or applications.  
Using passwords ensures the owner of the account is the only one who has access.  
However, if the password is shared or falls into the wrong hands, unauthorized changes to a given system could occur.  
Unauthorized access could potentially lead to changes in the system's overall status and health or damage the file system.  
Passwords are typically comprised of a combination of characters such as letters, numbers, and symbols.  
Thus, it is up to the user how they generate passwords!

A collection of passwords is often referred to as a dictionary or wordlist.  
Passwords with low complexity that are easy to guess are commonly found in various publicly disclosed password data breaches.  
For example, an easy-to-guess password could be `password`, `123456`, `111111`, and much more.  
Here are [the top 100 and most common and seen passwords](https://techlabuzz.com/top-100-most-common-passwords/) for your reference.  
Thus, it won't take long and be too difficult for the attacker to run password attacks against the target or service to guess the password.  
Choosing a strong password is a good practice, making it hard to guess or crack.  
Strong passwords should not be common words or found in dictionaries as well as the password should be an eight characters length at least.  
It also should contain uppercase and lower case letters, numbers, and symbol strings (ex: `*&^%$#@`).

Sometimes, companies have their own password policies and enforce users to follow guidelines when creating passwords.  
This helps ensure users aren't using common or weak passwords within their organization and could limit attack vectors such as brute-forcing.  
For example, a password length has to be eight characters and more, including characters, a couple of numbers, and at least one symbol.  
However, if the attacker figures out the password policy, he could generate a password list that satisfies the account password policy.

## How secure are passwords?
Passwords are a protection method for accessing online accounts or computer systems.  
Passwords authentication methods are used to access personal and private systems, and its main goal of using the password is to keep it safe and not share it with others. 

To answer the question: `How secure are passwords?` depends on various factors.  
Passwords are usually stored within the file system or database, and keeping them safe is essential.  
We've seen cases where companies store passwords into plaintext documents, such as the Sony breach in 2014.  
Therefore, once an attacker accesses the file system, he can easily obtain and reuse these passwords.  
On the other hand, others store passwords within the system using various techniques such as hashing functions or encryption algorithms to make them more secure.  
Even if the attacker has to access the system, it will be harder to crack. We will cover cracking hashes in the upcoming tasks.


---

# [Task 2  Password Attacking Techniques](#)
![image](https://user-images.githubusercontent.com/51442719/185889214-f2d44aa5-a720-4874-83e8-8c0f269aa2fc.png)

## Password Attack Techniques
In this room, we will discuss the techniques that could be used to perform password attacks.  
We will cover various techniques such as a dictionary, brute-force, rule-base, and guessing attacks.  
All the above techniques are considered active 'online' attacks where the attacker needs to communicate with the target machine to obtain the password in order to gain unauthorized access to the machine.

## Password Cracking vs. Password Guessing
This section discusses password cracking terminology from a cybersecurity perspective.  
Also, we will discuss significant differences between password cracking and password guessing.  
Finally, we'll demonstrate various tools used for password cracking, including Hashcat and John the Ripper.

Password cracking is a technique used for discovering passwords from encrypted or hashed data to plaintext data.  
Attackers may obtain the encrypted or hashed passwords from a compromised computer or capture them from transmitting data over the network.  
Once passwords are obtained, the attacker can utilize password attacking techniques to crack these hashed passwords using various tools.

Password cracking is considered one of the traditional techniques in pen-testing.  
The primary goal is to let the attacker escalate to higher privileges and access to a computer system or network.  
Password guessing and password cracking are often commonly used by information security professionals.  
Both have different meanings and implications.  
Password guessing is a method of guessing passwords for online protocols and services based on dictionaries.  
The following are major differences between password cracking and password guessing:

- Password guessing is a technique used to target online protocols and services. 
  - Therefore, it's considered time-consuming and opens up the opportunity to generate logs for the failed login attempts. 
  - A password guessing attack conducted on a web-based system often requires a new request to be sent for each attempt, which can be easily detected. 
  - It may cause an account to be locked out if the system is designed and configured securely.
- Password cracking is a technique performed locally or on systems controlled by the attacker.

---

# [Task 3  Password Profiling #1 - Default, Weak, Leaked, Combined , and Username Wordlists](#)
Having a good wordlist is critical to carrying out a successful password attack.  
It is important to know how you can generate username lists and password lists.  
In this section, we will discuss creating targeted username and password lists.  
We will also cover various topics, including default, weak, leaked passwords, and creating targeted wordlists.

## Default Passwords
Before performing password attacks, it is worth trying a couple of default passwords against the targeted service.  
Manufacturers set default passwords with products and equipment such as switches, firewalls, routers.  
There are scenarios where customers don't change the default password, which makes the system vulnerable.  
Thus, it is a good practice to try out `admin`:`admin`, `admin`:`123456`, etc.  
If we know the target device, we can look up the default passwords and try them out.  
For example, suppose the target server is a Tomcat, a lightweight, open-source Java application server.  
In that case, there are a couple of possible default passwords we can try: `admin`:`admin` or `tomcat`:`admin`.  

#### Here are some website lists that provide default passwords for various products.

- https://cirt.net/passwords
- https://default-password.info/
- https://datarecovery.com/rd/default-passwords/

## Weak Passwords
Professionals collect and generate weak password lists over time and often combine them into one large wordlist.  
Lists are generated based on their experience and what they see in pentesting engagements.  
These lists may also contain leaked passwords that have been published publically.  
Here are some of the common weak passwords lists :
- https://wiki.skullsecurity.org/index.php?title=Passwords - This includes the most well-known collections of passwords.
- [SecLists](https://github.com/danielmiessler/SecLists/tree/master/Passwords) - A huge collection of all kinds of lists, not only for password cracking.

## Leaked Passwords
Sensitive data such as passwords or hashes may be publicly disclosed or sold as a result of a breach.  
These public or privately available leaks are often referred to as 'dumps'.  
Depending on the contents of the dump, an attacker may need to extract the passwords out of the data.  
In some cases, the dump may only contain hashes of the passwords and require cracking in order to gain the plain-text passwords.  
The following are some of the common password lists that have weak and leaked passwords, including `webhost`, `elitehacker`,`hak5`, `Hotmail`, `PhpBB` companies' leaks:

- [SecLists/Passwords/Leaked-Databases](https://github.com/danielmiessler/SecLists/tree/master/Passwords/Leaked-Databases)

## Combined wordlists
Let's say that we have more than one wordlist.  
Then, we can combine these wordlists into one large file.  
This can be done as follows using `cat`:
```
cat file1.txt file2.txt file3.txt > combined_list.txt
```

To clean up the generated combined list to remove duplicated words, we can use sort and uniq as follows:

```
sort combined_list.txt | uniq -u > cleaned_combined_list.txt
```

## Customized Wordlists
Customizing password lists is one of the best ways to increase the chances of finding valid credentials.  
We can create custom password lists from the target website. Often, a company's website contains valuable information about the company and its employees, including emails and employee names.  
In addition, the website may contain keywords specific to what the company offers, including product and service names, which may be used in an employee's password!  

Tools such as `Cewl` can be used to effectively crawl a website and extract strings or keywords. 
`Cewl` is a powerful tool to generate a wordlist specific to a given company or target.  
Consider the following example below:

```
cewl -w list.txt -d 5 -m 5 http://thm.labs
```

`-w` will write the contents to a file. In this case, list.txt.  
`-m` 5 gathers strings (words) that are 5 characters or more  
`-d` 5 is the depth level of web crawling/spidering (default 2)  
`http://thm.labs` is the URL that will be used  


As a result, we should now have a decently sized wordlist based on relevant words for the specific enterprise, like names, locations, and a lot of their business lingo.  
Similarly, the wordlist that was created could be used to fuzz for usernames. 

Apply what we discuss using cewl against https://clinic.thmredteam.com/ to parse all words and generate a wordlist with a minimum length of 8.  
Note that we will be using this wordlist later on with another task!

## Username Wordlists
Gathering employees' names in the enumeration stage is essential.  
We can generate username lists from the target's website.  
For the following example, we'll assume we have a {first name} {last name} (ex: John Smith) and a method of generating usernames.

{first name}: `john`  
{last name}: `smith`  
{first name}{last name}:  `johnsmith`  
{last name}{first name}:  `smithjohn`  
first letter of the {first name}{last name}: `jsmith`  
first letter of the {last name}{first name}: `sjohn`  
first letter of the {first name}.{last name}: `j.smith`  
first letter of the {first name}-{last name}: `j-smith`   
and so on

Thankfully, there is a tool `username_generator` that could help create a list with most of the possible combinations if we have a first name and last name.  

```
git clone https://github.com/therodri2/username_generator.git;  cd username_generator
```

Using `python3 username_generator.py -h` shows the tool's help message and optional arguments.





---

# [Task 4  Password Profiling #2 - Keyspace Technique and CUPP](#)

---

# [Task 5  Offline Attacks - Dictionary and Brute-Force](#)

---

# [Task 6  Offline Attacks - Rule-Based](#)

---

# [Task 7  Deploy the VM](#)

---

# [Task 8  Online password attacks](#)

---

# [Task 9  Password spray attack](#)

---

# [Task 10  Summary](#)

This room introduced the basic concepts of different password attacks and how to create custom and targeted password lists.  
We covered and discussed various topics, including:

- Default, weak, leaked combined wordlists
- Password profiling
- Offline password attacks
- Online password attacks
