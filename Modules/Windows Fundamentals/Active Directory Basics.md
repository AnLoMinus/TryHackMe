# [Active Directory Basics](https://tryhackme.com/room/winadbasics)
- This room will introduce the basic concepts and functionality provided by Active Directory.

## Machine Information
### Title: `adbasics_v1.2`
### IP Address:  `10.10.217.144`

---

- [x] Task 1  Introduction
- [x] Task 2  Windows Domains
- [ ] Task 3  Active Directory
- [ ] Task 4  Managing Users in AD
- [ ] Task 5  Managing Computers in AD
- [ ] Task 6  Group Policies
- [ ] Task 7  Authentication Methods
- [ ] Task 8  Trees, Forests and Trusts
- [ ] Task 9  Conclusion

---

# Task 1 Introduction

## Room Objectives
#### In this room, we will learn about Active Directory and will become familiar with the following topics
Microsoft's Active Directory is the backbone of the corporate world.
It simplifies the management of devices and users within a corporate environment.
In this room, we'll take a deep dive into the essential components of Active Directory.

- What Active Directory is
- What an Active Directory Domain is
- What components go into an Active Directory Domain
- Forests and Domain Trust
- And much more!

## Room Prerequisites
General familiarity with Windows.
Check the [Windows Fundamentals module](https://tryhackme.com/module/windows-fundamentals) for more information on this.

---

# Task 2  Windows Domains
Picture yourself administering a small business network with only five computers and five employees.
In such a tiny network, you will probably be able to configure each computer separately without a problem.
You will manually log into each computer, create users for whoever will use them, and make specific configurations for each employee's accounts.
If a user's computer stops working, you will probably go to their place and fix the computer on-site.

While this sounds like a very relaxed lifestyle, let's suppose your business suddenly grows and now has 157 computers and 320 different users located across four different offices.
Would you still be able to manage each computer as a separate entity, manually configure policies for each of the users across the network and provide on-site support for everyone?
The answer is most likely no.

To overcome these limitations, we can use a Windows domain.
Simply put, a Windows domain is a group of users and computers under the administration of a given business. The main idea behind a domain is to centralise the administration of common components of a Windows computer network in a single repository called Active Directory (AD).
The server that runs the Active Directory services is known as a Domain Controller (DC).

<div align="center">
  <img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/5ed5961c6276df568891c3ea/room-content/bebe5dfec0208bf563d01fa2dd1fb7a7.png">
</div>
<br>
<br>

- #### The main advantages of having a configured Windows domain are:
  - `Centralised identity management`: All users across the network can be configured from Active Directory with minimum effort.
  - `Managing security policies`: You can configure security policies directly from Active Directory and apply them to users and computers across the network as needed.

### A Real-World Example

If this sounds a bit confusing, chances are that you have already interacted with a Windows domain at some point in your school, university or work.  

In school/university networks, you will often be provided with a username and password that you can use on any of the computers available on campus.  
Your credentials are valid for all machines because whenever you input them on a machine, it will forward the authentication process back to the Active Directory, where your credentials will be checked.   
Thanks to Active Directory, your credentials don't need to exist in each machine and are available throughout the network.

Active Directory is also the component that allows your school/university to restrict you from accessing the control panel on your school/university machines.  
Policies will usually be deployed throughout the network so that you don't have administrative privileges over those computers.

### Welcome to THM Inc.

During this task, we'll assume the role of the new IT admin at THM Inc.   
As our first task, we have been asked to review the current domain "THM.local" and do some additional configurations.  
You will have administrative credentials over a pre-configured Domain Controller (DC) to do the tasks.

Be sure to click the Start Machine button now, as you'll use the same machine for all tasks. This should open a machine in your browser.  
Should you prefer to connect to it via RDP, you can use the following credentials:

- Username	`Administrator`
- Password	`Password321`

`Note`: When connecting via RDP, use `THM\Administrator` as the username to specify you want to log in using the user `Administrator` on the `THM` domain.

Since we will be connecting to the target machine via RDP, this is also a good time to start the AttackBox (unless you are using your own machine).

---

# Task 3  Active Directory

The core of any Windows Domain is the Active Directory Domain Service (AD DS).  
This service acts as a catalogue that holds the information of all of the "objects" that exist on your network.  
Amongst the many objects supported by AD, we have users, groups, machines, printers, shares and many others.  
Let's look at some of them:

### Users

Users are one of the most common object types in Active Directory.  
Users are one of the objects known as security principals, meaning that they can be authenticated by the domain and can be assigned privileges over resources like files or printers.  
You could say that a security principal is an object that can act upon resources in the network.

##### Users can be used to represent two types of entities:
  - `People`: users will generally represent persons in your organisation that need to access the network, like employees.   

  - `Services`: you can also define users to be used by services like IIS or MSSQL. Every single service requires a user to run, but service users are different from regular users as they will only have the privileges needed to run their specific service.

### Machines

Machines are another type of object within Active Directory;  
for every computer that joins the Active Directory domain, a machine object will be created.  
Machines are also considered "security principals" and are assigned an account just as any regular user.  
This account has somewhat limited rights within the domain itself.

The machine accounts themselves are local administrators on the assigned computer, they are generally not supposed to be accessed by anyone except the computer itself, but as with any other account, if you have the password, you can use it to log in.

`Note`: Machine Account passwords are automatically rotated out and are generally comprised of 120 random characters.

Identifying machine accounts is relatively easy. They follow a specific naming scheme.  
The machine account name is the computer's name followed by a dollar sign.  
For example, a machine named `DC01` will have a machine account called `DC01$`.

### Security Groups

If you are familiar with Windows, you probably know that you can define user groups to assign access rights to files or other resources to entire groups instead of single users.  
This allows for better manageability as you can add users to an existing group, and they will automatically inherit all of the group's privileges.  
Security groups are also considered security principals and, therefore, can have privileges over resources on the network.

Groups can have both users and machines as members.  
If needed, groups can include other groups as well.

Several groups are created by default in a domain that can be used to grant specific privileges to users.  
As an example, here are some of the most important groups in a domain:


Security Group | Description
:---: | :---:
Domain Admins	| Users of this group have administrative privileges over the entire domain. By default, they can administer any computer on the domain, including the DCs.
Server Operators | Users in this group can administer Domain Controllers. They cannot change any administrative group memberships.
Backup Operators | Users in this group are allowed to access any file, ignoring their permissions. They are used to perform backups of data on computers.
Account Operators	| Users in this group can create or modify other accounts in the domain.
Domain Users	| Includes all existing user accounts in the domain.
Domain Computers	| Includes all existing computers in the domain.
Domain Controllers	| Includes all existing DCs on the domain.

You can obtain the complete list of default security groups from the [Microsoft documentation](https://docs.microsoft.com/en-us/windows/security/identity-protection/access-control/active-directory-security-groups).

## Active Directory Users and Computers
To configure users, groups or machines in Active Directory, we need to log in to the Domain Controller and run "Active Directory Users and Computers" from the start menu:

<div align="center">
  <img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/5ed5961c6276df568891c3ea/room-content/11d01963392078c1450300d2881f9160.png">
</div>
<br>
<br>

This will open up a window where you can see the hierarchy of users, computers and groups that exist in the domain.  
These objects are organised in Organizational Units (OUs) which are container objects that allow you to classify users and machines.  
OUs are mainly used to define sets of users with similar policing requirements.  
The people in the Sales department of your organisation are likely to have a different set of policies applied than the people in IT, for example.  
Keep in mind that a user can only be a part of a single OU at a time.

Checking our machine, we can see that there is already an OU called `THM` with four child OUs for the IT, Management, Marketing and Sales departments.  
It is very typical to see the OUs mimic the business' structure, as it allows for efficiently deploying baseline policies that apply to entire departments.  
Remember that while this would be the expected model most of the time, you can define OUs arbitrarily.  
Feel free to right-click the `THM` OU and create a new OU under it called `Students` just for the fun of it.

<div align="center">
  <img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/5ed5961c6276df568891c3ea/room-content/c5b1d321108bc065771eba62d24f5e83.png">
</div>
<br>
<br>

If you open any OUs, you can see the users they contain and perform simple tasks like creating, deleting or modifying them as needed.  
You can also reset passwords if needed (pretty useful for the helpdesk):

<div align="center">
  <img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/5ed5961c6276df568891c3ea/room-content/76e01efece5a00cc91f7099226130c5c.png">
</div>
<br>
<br>

##### You probably noticed already that there are other default containers apart from the THM OU. These containers are created by Windows automatically and contain the following:

- `Builtin`: Contains default groups available to any Windows host.
- `Computers`: Any machine joining the network will be put here by default. You can move them if needed.
- `Domain Controllers`: Default OU that contains the DCs in your network.
- `Users`: Default users and groups that apply to a domain-wide context.
- `Managed Service Accounts`: Holds accounts used by services in your Windows domain.

## Security Groups vs OUs
You are probably wondering why we have both groups and OUs.  
While both are used to classify users and computers, their purposes are entirely different:

OUs are handy for applying policies to users and computers, which include specific configurations that pertain to sets of users depending on their particular role in the enterprise.  
Remember, a user can only be a member of a single OU at a time, as it wouldn't make sense to try to apply two different sets of policies to a single user.  
Security Groups, on the other hand, are used to grant permissions over resources.  
For example, you will use groups if you want to allow some users to access a shared folder or network printer.  
A user can be a part of many groups, which is needed to grant access to multiple resources.




---

# Task 4  Managing Users in AD

---

# Task 5  Managing Computers in AD

---

# Task 6  Group Policies

---

# Task 7  Authentication Methods

---

# Task 8  Trees, Forests and Trusts

---

# Task 9  Conclusion
