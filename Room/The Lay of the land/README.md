# [The Lay of the land](https://tryhackme.com/room/thelayoftheland)
#### Learn about and get hands-on with common technologies and security products used in corporate environments; both host and network-based security solutions are covered.

- [Task 1  Introduction](#)
- [Task 2  Deploy the VM](#)
- [Task 3  Network Infrastructure](#)
- [Task 4  Active Directory (AD) environment](#)
- [Task 5  Users and Groups Management](#)
- [Task 6  Host Security Solution #1](#)
- [Task 7  Host Security Solution #2](#)
- [Task 8  Network Security Solutions](#)
- [Task 9  Applications and Services](#)
- [Task 10  Conclusion](#)

---

# Task 1  Introduction

It is essential to be familiar with the environment where you have initial access to a compromised machine during a red team engagement. Therefore, performing reconnaissance and enumeration is a significant part, and the primary goal is to gather as much information as possible to be used in the next stage. 

With an initial foothold established, the post-exploitation process begins! 

This room introduces commonly-used concepts, technologies, and security products that we need to be aware of.

In this room, the assumption is that we have already gained access to the machine, and we are ready to expand our knowledge more about the environment by performing enumerating for the following:

- Network infrastrucutre
- Active Directory Environment
- Users and Groups
- Host-based security solutions
- Network-based security solutions
- Applications and services


---

# Task 2  Deploy the VM

---

# Task 3  Network Infrastructure

Once arriving onto an unknown network, our first goal is to identify where we are and what we can get to. During the red team engagement, we need to understand what target system we are dealing with, what service the machine provides, what kind of network we are in. Thus, the enumeration of the compromised machine after getting initial access is the key to answering these questions. This task will discuss the common types of networks we may face during the engagement.

Network segmentation is an extra layer of network security divided into multiple subnets. It is used to improve the security and management of the network. For example, it is used for preventing unauthorized access to corporate most valuable assets such as customer data, financial records, etc.

The Virtual Local Area Networks (VLANs) is a network technique used in network segmentation to control networking issues, such as broadcasting issues in the local network, and improve security. Hosts within the VLAN can only communicate with other hosts in the same VLAN network. 

If you want to learn more about network fundamentals, we suggest trying the following TryHackMe module: [Network Fundamentals](https://tryhackme.com/module/network-fundamentals).

## Internal Networks

Internal Networks are subnetworks that are segmented and separated based on the importance of the internal device or the importance of the accessibility of its data.  
The main purpose of the internal network(s) is to share information, faster and easier communications, collaboration tools, operational systems, and network services within an organization. In a corporate network, the network administrators intend to use network segmentation for various reasons, including controlling network traffic, optimizing network performance, and improving security posture. 

![image](https://user-images.githubusercontent.com/51442719/197808136-3261bf20-c954-4367-aa84-9dcf6c9739fb.png)

The previous diagram is an example of the simple concept of network segmentation as the network is divided into two networks. The first one is for employee workstations and personal devices. The second is for private and internal network devices that provide internal services such as DNS, internal web, email services, etc.

## A Demilitarized Zone (DMZ)

A DMZ Network is an edge network that protects and adds an extra security layer to a corporation's internal local-area network from untrusted traffic. A common design for DMZ is a subnetwork that sits between the public internet and internal networks.

Designing a network within the company depends on its requirements and need. For example, suppose a company provides public services such as a website, DNS, FTP, Proxy, VPN, etc. In that case, they may design a DMZ network to isolate and enable access control on the public network traffic, untrusted traffic.

![image](https://user-images.githubusercontent.com/51442719/197808228-c85796bc-bb84-4ecc-b590-f8736506c70c.png)

In the previous diagram, we represent the network traffic to the DMZ network in red color, which is untrusted ( comes directly from the internet). The green network traffic between the internal network is the controlled traffic that may go through one or more than one network security device(s).

Enumerating the system and the internal network is the discovering stage, which allows the attacker to learn about the system and the internal network. Based on the gained information, we use it to process lateral movement or privilege escalation to gain more privilege on the system or the AD environment.

## Network Enumeration

There are various things to check related to networking aspects such as TCP and UDP ports and established connections, routing tables, ARP tables, etc.

Let's start checking the target machine's TCP and UDP open ports. This can be done using the `netstat` command as shown below.

```cmd
PS C:\Users\thm> netstat -na
```

The output reveals the open ports as well as the established connections. Next, let's list the ARP table, which contains the IP address and the physical address of the computers that communicated with the target machines within the network. This could be helpful to see the communications within the network to scan the other machines for open ports and vulnerabilities.

```cmd
PS C:\Users\thm> arp -a
```

## Internal Network Services

It provides private and internal network communication access for internal network devices. An example of network services is an internal DNS, web servers, custom applications, etc. It is important to note that the internal network services are not accessible outside the network. However, once we have initial access to one of the networks that access these network services, they will be reachable and available for communications. 

We will discuss more Windows applications and services in Task 9, including DNS and custom web applications.


---

# Task 4  Active Directory (AD) environment

What is the Active Directory (AD) environment?

![image](https://user-images.githubusercontent.com/51442719/197809098-d13e4300-454e-49ca-bc1b-52043afe891a.png)

It is a Windows-based directory service that stores and provides data objects to the internal network environment. It allows for centralized management of authentication and authorization. The AD contains essential information about the network and the environment, including users, computers, printers, etc. For example, AD might have users' details such as job title, phone number, address, passwords, groups, permission, etc.

![image](https://user-images.githubusercontent.com/51442719/197809137-cca8d681-eb23-451b-91f8-7f9a6864dae7.png)

The diagram is one possible example of how Active Directory can be designed. The AD controller is placed in a subnet for servers (shown above as server network), and then the AD clients are on a separate network where they can join the domain and use the AD services via the firewall.

The following is a list of Active Directory components that we need to be familiar with:

- Domain Controllers
- Organizational Units
- AD objects
- AD Domains
- Forest
- AD Service Accounts: Built-in local users, Domain users, Managed service accounts
- Domain Administrators

A Domain Controller is a Windows server that provides Active Directory services and controls the entire domain. It is a form of centralized user management that provides encryption of user data as well as controlling access to a network, including users, groups, policies, and computers. It also enables resource access and sharing. These are all reasons why attackers target a domain controller in a domain because it contains a lot of high-value information.

![image](https://user-images.githubusercontent.com/51442719/197809299-e8dfadf5-92cf-4faf-8480-55cb9af97cd4.png)

Organizational Units (OU's) are containers within the AD domain with a hierarchical structure.

Active Directory Objects can be a single user or a group, or a hardware component, such as a computer or printer. Each domain holds a database that contains object identity information that creates an AD environment, including:

- Users - A security principal that is allowed to authenticate to machines in the domain
- Computers - A special type of user accounts
- GPOs - Collections of policies that are applied to other AD objects

AD domains are a collection of Microsoft components within an AD network. 

AD Forest is a collection of domains that trust each other. 

![image](https://user-images.githubusercontent.com/51442719/197809456-74f14c3f-41d6-479e-be66-91b8bc715bdb.png)

For more information about the basics of Active Directory, we suggest trying the following TryHackMe room: [Active Directory Basics](https://tryhackme.com/room/activedirectorybasics).


---

# Task 5  Users and Groups Management

In this task, we will learn more about users and groups, especially within the Active Directory. Gathering information about the compromised machine is essential that could be used in the next stage. Account discovery is the first step once we have gained initial access to the compromised machine to understand what we have and what other accounts are in the system. 

![image](https://user-images.githubusercontent.com/51442719/197810064-8286a71e-a548-487c-9390-ab1d9de38d3c.png)

An Active Directory environment contains various accounts with the necessary permissions, access, and roles for different purposes. Common Active Directory service accounts include built-in local user accounts, domain user accounts, managed service accounts, and virtual accounts. 

- The built-in local users' accounts are used to manage the system locally, which is not part of the AD environment.
- Domain user accounts with access to an active directory environment can use the AD services (managed by AD).
- AD managed service accounts are limited domain user account with higher privileges to manage AD services.
- Domain Administrators are user accounts that can manage information in an Active Directory environment, including AD configurations, users, groups, permissions, roles, services, etc. One of the red team goals in engagement is to hunt for information that leads to a domain administrator having complete control over the AD environment.

The following are Active Directory Administrators accounts:

| BUILTIN\Administrator | Local admin access on a domain controller |
|:---:|:---:|
| Domain Admins | Administrative access to all resources in the domain |
| Enterprise Admins | Available only in the forest root |
| Schema Admins | Capable of modifying domain/forest; useful for red teamers |
| Server Operators | Can manage domain servers |
| Account Operators | Can manage users that are not in privileged groups |

Now that we learn about various account types within the AD environment. Let's enumerate the Windows machine that we have access to during the initial access stage. As a current user, we have specific permissions to view or manage things within the machine and the AD environment. 

## Active Directory (AD) Enum

Now, enumerating in the AD environment requires different tools and techniques. Once we confirm that the machine is part of the AD environment, we can start hunting for any variable info that may be used later. In this stage, we are using PowerShell to enumerate for users and groups.

The following PowerShell command is to get all active directory user accounts. Note that we need to use  `-Filter` argument.

```cmd
PS C:\Users\thm> Get-ADUser  -Filter *
DistinguishedName : CN=Administrator,CN=Users,DC=thmredteam,DC=com
Enabled           : True
GivenName         :
Name              : Administrator
ObjectClass       : user
ObjectGUID        : 4094d220-fb71-4de1-b5b2-ba18f6583c65
SamAccountName    : Administrator
SID               : S-1-5-21-1966530601-3185510712-10604624-500
Surname           :
UserPrincipalName :
PS C:\Users\thm>
```

We can also use the [LDAP hierarchical tree structure](http://www.ietf.org/rfc/rfc2253.txt) to find a user within the AD environment. The Distinguished Name (DN) is a collection of comma-separated key and value pairs used to identify unique records within the directory. The DN consists of Domain Component (DC), OrganizationalUnitName (OU), Common Name (CN), and others. The following `"CN=User1,CN=Users,DC=thmredteam,DC=com"` is an example of DN, which can be visualized as follow:

![image](https://user-images.githubusercontent.com/51442719/197810680-a866152f-0a97-4100-871d-c110e375b7a8.png)

Using the `SearchBase` option, we specify a specific Common-Name `CN` in the active directory. For example, we can specify to list any user(s) that part of `Users`.

```cmd
PS C:\Users\thm> Get-ADUser -Filter * -SearchBase "CN=Users,DC=THMREDTEAM,DC=COM"


DistinguishedName : CN=Administrator,CN=Users,DC=thmredteam,DC=com
Enabled           : True
GivenName         :
Name              : Administrator
ObjectClass       : user
ObjectGUID        : 4094d220-fb71-4de1-b5b2-ba18f6583c65
SamAccountName    : Administrator
SID               : S-1-5-21-1966530601-3185510712-10604624-500
Surname           :
UserPrincipalName :
```

Note that the result may contain more than one user depending on the configuration of the CN. Try the command to find all users within the THM `OU` and answer question 1 below.


---

# Task 6  Host Security Solution #1

---

# Task 7  Host Security Solution #2

---

# Task 8  Network Security Solutions

---

# Task 9  Applications and Services

---

# Task 10  Conclusion

---
