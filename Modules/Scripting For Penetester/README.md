![image](https://user-images.githubusercontent.com/51442719/198330831-01746f52-0905-417f-9c2d-487c98ddf0e2.png)

# [Hacking with PowerShell](https://tryhackme.com/room/powershell)
#### Learn the basics of PowerShell and PowerShell Scripting

- [Task 1  Objectives](#)
- [Task 2  What is Powershell?](#)
- [Task 3  Basic Powershell Commands](#)
- [Task 4  Enumeration](#)
- [Task 5  Basic Scripting Challenge](#)
- [Task 6  Intermediate Scripting](#)

---

# Task 1  Objectives

---

# Task 2  What is Powershell?

Powershell is the Windows Scripting Language and shell environment that is built using the .NET framework.

This also allows Powershell to execute .NET functions directly from its shell. Most Powershell commands, called cmdlets, are written in .NET. Unlike other scripting languages and shell environments, the output of these cmdlets are objects - making Powershell somewhat object oriented. This also means that running cmdlets allows you to perform actions on the output object(which makes it convenient to pass output from one cmdlet to another). The normal format of a cmdlet is represented using Verb-Noun; for example the cmdlet to list commands is called `Get-Command`.

Common verbs to use include:
- Get
- Start
- Stop 
- Read
- Write
- New
- Out

To get the full list of approved verbs, visit this [link](https://docs.microsoft.com/en-us/powershell/scripting/developer/cmdlet/approved-verbs-for-windows-powershell-commands?view=powershell-7).

---

# Task 3  Basic Powershell Commands

Now that we've understood how cmdlets works - let's explore how to use them! The main thing to remember here is that Get-Command and Get-Help are your best friends! 

## Using Get-Help

`Get-Help` displays information about a cmdlet. To get help about a particular command, run the following:

`Get-Help Command-Name`

You can also understand how exactly to use the command by passing in the `-examples` flag. This would return output like the following: 

![image](https://user-images.githubusercontent.com/51442719/198332012-62370a83-c39e-4c26-97ff-1e3104b7aa7f.png)

## Using Get-Command

Get-Command gets all the cmdlets installed on the current Computer. The great thing about this cmdlet is that it allows for pattern matching like the following

`Get-Command Verb-*` or `Get-Command *-Noun`

Running `Get-Command New-*` to view all the cmdlets for the verb new displays the following: 

![image](https://user-images.githubusercontent.com/51442719/198332263-652de6f6-23ce-40c6-8348-1a3bb4c03c61.png)

## Object Manipulation

In the previous task, we saw how the output of every cmdlet is an object. If we want to actually manipulate the output, we need to figure out a few things:

- passing output to other cmdlets
- using specific object cmdlets to extract information

The Pipeline(|) is used to pass output from one cmdlet to another. A major difference compared to other shells is that instead of passing text or string to the command after the pipe, powershell passes an object to the next cmdlet. Like every object in object oriented frameworks, an object will contain methods and properties. You can think of methods as functions that can be applied to output from the cmdlet and you can think of properties as variables in the output from a cmdlet. To view these details, pass the output of a cmdlet to the Get-Member cmdlet

`Verb-Noun | Get-Member` 

An example of running this to view the members for Get-Command is:

`Get-Command | Get-Member -MemberType Method`

![image](https://user-images.githubusercontent.com/51442719/198332626-ebed10db-be1e-4078-8dab-15fb3da8aae2.png)

From the above flag in the command, you can see that you can also select between methods and properties.

## Creating Objects From Previous cmdlets

One way of manipulating objects is pulling out the properties from the output of a cmdlet and creating a new object. This is done using the `Select-Object` cmdlet. 

Here's an example of listing the directories and just selecting the mode and the name:

![image](https://user-images.githubusercontent.com/51442719/198332731-df099d8a-44bc-43c7-ae16-ef6b857c6237.png)

You can also use the following flags to select particular information:

- first - gets the first x object
- last - gets the last x object
- unique - shows the unique objects
- skip - skips x objects

## Filtering Objects

When retrieving output objects, you may want to select objects that match a very specific value. You can do this using the `Where-Object` to filter based on the value of properties. 

The general format of the using this cmdlet is 

`Verb-Noun | Where-Object -Property PropertyName -operator Value`

`Verb-Noun | Where-Object {$_.PropertyName -operator Value}`

The second version uses the $_ operator to iterate through every object passed to the Where-Object cmdlet.

Powershell is quite sensitive so make sure you don't put quotes around the command!

Where `-operator` is a list of the following operators:

- `-Contains`: if any item in the property value is an exact match for the specified value
- `-EQ`: if the property value is the same as the specified value
- `-GT`: if the property value is greater than the specified value

For a full list of operators, use [this](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/where-object?view=powershell-6) link.

Here's an example of checking the stopped processes:

![image](https://user-images.githubusercontent.com/51442719/198333262-58180825-0ebd-4eb9-8fb4-2f15eb8cdd52.png)

## Sort Object

When a cmdlet outputs a lot of information, you may need to sort it to extract the information more efficiently. You do this by pipe lining the output of a cmdlet to the `Sort-Object` cmdlet.

The format of the command would be

`Verb-Noun | Sort-Object`

Here's an example of sort the list of directories:

![image](https://user-images.githubusercontent.com/51442719/198333375-a00ce29c-b23a-4423-b314-bdb54c39b968.png)

Now that you've understood the basics of how Powershell works, let try some commands to apply this knowledge!



---

# Task 4  Enumeration

---

# Task 5  Basic Scripting Challenge

---

# Task 6  Intermediate Scripting

---
