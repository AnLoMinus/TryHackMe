![image](https://user-images.githubusercontent.com/51442719/200470757-30173478-b9d7-4f16-bb82-3287f2658603.png)

# [Phishing Analysis Fundamentals](https://tryhackme.com/room/phishingemails1tryoe)

## Learn all the components that make up an email.

---

- [Task 1  Introduction](#task-1--introduction)
- [Task 2  The Email Address](#task-2--the-email-address)
- [Task 3  Email Delivery](#task-3--email-delivery)
- [Task 4  Email Headers](#task-4--email-headers)
- [Task 5  Email Body](#task-5--email-body)
- [Task 6  Types of Phishing](#task-6--types-of-phishing)
- [Task 7  Conclusion](#task-7--conclusion)

---

## Task 1  Introduction


Spam and Phishing are common social engineering attacks.  
In social engineering, phishing attack vectors can be a phone call, a text message, or an email.  
As you should have already guessed, our focus is on email as the attack vector.  

We all should be somewhat familiar with what spam is.  
No matter what, these emails somehow find their way into our inboxes. 

The first email classified as spam dates back to 1978, and it's still thriving today. 

Phishing is a serious attack vector that you, as a defender, will have to defend against.

An organization can follow all the recommended guidelines when it comes to building a layered defense strategy.  
Still, all it takes is an inexperienced and unsuspecting user within your corporate environment to click on a link or download and run a malicious attachment which may provide an attacker a foothold into the network. 

Many products help combat spam and phishing, but realistically these emails still can get through.  
When they do, as a Security Analyst, you need to know how to analyze these emails to determine if they're malicious or benign.

Furthermore, you will need to gather information about the email to update your security products to prevent malicious emails from making their way back into a user's inbox. 

In this room, we'll look at all the components involved with sending emails across the Internet and how to analyze email headers. 


---

## Task 2  The Email Address

It's only appropriate to start this room by mentioning the man who invented the concept of emails and made the @ symbol famous. The person responsible for the contribution to the way we communicate was `Ray Tomlinson`. 

The invention of the email dates back to the 1970s for [ARPANET](https://www.britannica.com/topic/ARPANET).  
Yep, probably before you were born. Definitely, before I was born. :) 

So, what makes up an email address?
1. User Mailbox (or Username)
2. @
3. Domain

Let's look at the following email address, billy@johndoe.com.

1. The user mailbox is billy
2. @ (thanks Ray)
3. The domain is johndoe.com

To simplify this even further, think about the street on which you live on.

- You can think of your street as the domain. 
- The recipient's first/last name, along with the house number in this scenario, represents the user mailbox. 

With this information, the postal worker delivering the mail knows into which mailbox to put the letter(s). 

Next, let's look at the network protocols used to send an email from the sender to the recipient.



---

## Task 3  Email Delivery

A handful of protocols are involved with the "magic" that takes place when you hit SEND in an email client. 

By now, you should already know that certain protocols were created to handle specific network-related tasks, such as email. 

There are 3 specific protocols involved to facilitate the outgoing and incoming email messages, and they are briefly listed below.

- `SMTP` (`Simple Mail Transfer Protocol`) - It is utilized to handle the sending of emails. 
- `POP3` (`Post Office Protocol`) - Is responsible transferring email between a client and a mail server. 
- `IMAP` (`Internet Message Access Protocol`) - Is responsible transferring email between a client and a mail server. 


---

## Task 4  Email Headers

---

## Task 5  Email Body

---

## Task 6  Types of Phishing

---

## Task 7  Conclusion

