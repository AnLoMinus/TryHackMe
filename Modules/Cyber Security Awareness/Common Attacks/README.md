## 🔶 `Free` - [Common Attacks](https://tryhackme.com/room/commonattacks)
![image](https://user-images.githubusercontent.com/51442719/172191250-ff82edc6-b5bd-4264-aeaf-8ab6118495f3.png)
> With practical exercises see how common attacks occur, and improve your cyber hygiene to stay safer online.
- [x] [Task 1  `Information` Introduction](#task-1--information-introduction)
- [x] [Task 2  `Common Attacks` Social Engineering](#task-2--common-attacks-social-engineering)
- [ ] [Task 3  `Common Attacks` Social Engineering: Phishing](#task-3--common-attacks-social-engineering-phishing)
- [ ] [Task 4  `Common Attacks` Malware and Ransomware](#task-4--common-attacks-malware-and-ransomware)
- [ ] [Task 5  `Common Attacks` Passwords and Authentication](#task-5--common-attacks-passwords-and-authentication)
- [ ] [Task 6  `Staying Safe` Multi-Factor Authentication and Password Managers](#task-6--staying-safe-multi-factor-authentication-and-password-managers)
- [ ] [Task 7  `Staying Safe` Public Network Safety](#task-7--staying-safe-public-network-safety)
- [ ] [Task 8  `Staying Safe` Backups](#task-8--staying-safe-backups)
- [ ] [Task 9  `Staying Safe` Updates and Patches](#task-9--staying-safe-updates-and-patches)
- [ ] [Task 10  `Information` Conclusion](#task-10--information-conclusion)

---
- (`Phishing`) -  When emails are sent to a target(s) purporting to be from a trusted entity to lure individuals into providing sensitive information.
---

# [Task 1  `Information` Introduction]()

- Our existence in a digital world makes it imperative that we understand and can protect against common attacks.
- This room will discuss some of the most common techniques used by attackers to target people online. 
- It will also teach some of the best ways to prevent the success of each technique.
- Without further ado, let's begin!

### Answer the questions below
- Let's get started!
  > `No answer needed`

---

# [Task 2  `Common Attacks` Social Engineering]()

### What is Social Engineering?
- Social Engineering is the term used to describe any cyberattack where a human (rather than a computer) is the target; 
  - for this reason, it is sometimes referred to as "`People Hacking`". 
- For example, if an attacker wishes to obtain a victim's password, they could attempt to guess or brute-force the password — or they could [`simply ask you`](https://youtu.be/opRMrEfAIiI?t=42).
- Whilst the example linked above is relatively straightforward, social engineering attacks can become very complex and often result in an attacker gaining significant control over a target's life — both online and offline. 
- Social engineering attacks are often multi-layered and escalate due to the snowball effect. 
- For example, an attacker may start off by obtaining a small amount of publicly available information from a victim's social media presence, which they could then use to get more information from, say, your phone or broadband provider. 
- The information obtained from the second stage could then be used to gain more useful information, then escalate step-by-step to something like the victim's bank account.
- The best way to understand social engineering is to see it in action! 
- These videos from [`Defcon23`](https://youtu.be/fHhNWAKw0bY?t=100) (one of the largest hacking conferences in the world) and [`CNN`](https://youtu.be/PWVN3Rq4gzw) demonstrate some of the immense power in social engineering.
- They are both well worth a watch!

### Other Forms of Social Engineering
- Charismatic hackers calling your phone company and taking possession of your account is one form of social engineering; however, there are many Decorative image of a USB driveother types. 
- Social engineering is a vast topic, encompassing any attack that relies on tricking humans into giving the attacker access, rather than attacking the technology directly. 
- Whilst direct interaction with targets is the most common style of social engineering, other examples include dropping USB storage devices in public (e.g. in company car parks) in the hope that someone (often a company employee) will pick one up and plug it into a sensitive computer. 
- In a similar vein, attackers may leave a "charging cable" plugged into a socket in a public place. 
- In actuality, the cable contains malicious software such as keyloggers or tools to take control of the victim's device.

<details>
  <summary>
Case Study: Stuxnet (`Click to Read`)
  </summary>

Stuxnet was the name given to a particularly nasty computer virus (allegedly developed by the governments of the United States and Israel) that was originally used to target the Iran nuclear programme in 2009. Due to its ability as a "worm" to self-replicate (i.e. clone itself across networks — including the internet), the virus escaped and became much more widespread than was intended. Multiple variants now also exist, making Stuxnet a particularly hard-hitting and notorious weapon. You can read more about the background of Stuxnet here.

</details>

- In short, the limits to social engineering are at the bounds of an attacker's imagination. 
- A good social engineer can (and will) use a plethora of psychological tricks under any plausible context to "hack" their targets.

### Staying Safe from Social Engineering Attacks
- In many ways, it is very tricky to stay safe from social engineering as it won't always be you who the attacker is talking to, but rather someone who can give them what they need without your consent (e.g. calling your bank whilst pretending to be you, so as to access your bank account). 
- That said, there are still measures you can take to protect yourself from Social Engineering attacks:
  - Always make sure to set up multiple forms of authentication, and ensure that providers respect these. 
    - For example, set difficult to guess — or otherwise incorrect — answers to security questions (making sure to store the answers somewhere safe!), and make sure that these questions are asked when you try to access accounts over the phone.
  - Never plug external media (e.g. USBs/CDs/etc) into a computer that you care about or that is connected to any other devices. 
    - Ideally, don't plug the media in at all, and instead give it to your local police for safekeeping.
  - Always insist on proof of identity when a stranger calls or messages you claiming to work for a company whose services you use. 
    - Where possible, confirm with a known phone number or email address that the call or message you received was legitimate (i.e. use a trusted method to get in contact with the company to confirm). 
    - Remember that no legitimate employee will ever ask for your password or other information that protects your account.

### Answer the questions below
- Read the task information and watch the attached videos
  > `No answer needed`
- What was the original target of Stuxnet?
  > Answer format: [`*** **** ******* *********`](#the_Iran_nuclear_programme)


---

# [Task 3  `Common Attacks` Social Engineering: Phishing]()

### Overview
- Phishing is one of the most common cyber attack types employed by scammers and bad actors, targeting individuals and businesses indiscriminately. 
- In many cases, phishing is the initial attack vector used to gain access to a company's infrastructure before performing further attacks against the corporate network. 
- Whilst there are many automated tools now available to help combat phishing threats, phishing is still one of the most prolific attack vectors around.

### What is Phishing?
- Phishing is a sub-section of social engineering. 
- Whereas social engineering is a very general term used to describe any attack that takes advantage of a human rather than a computer system, phishing specifically describes attacks whereby a scammer or other attacker tricks a victim into opening a malicious webpage by sending them a text message, email, or another form of online correspondence. 
- Traditionally, "phishing" simply referred to emails; however, in the days of instant messaging, text messages, and voice/video calling, the term has evolved to blanket these other categories. 
- These other forms are sometimes referred to individually as "smishing" — phishing over SMS — and "vishing" — phishing over voice chat — respectively.
- These attacks are very widespread (indeed, the chances of you not having been on the receiving end of such an attack are slim!) and are frequently deployed on massive scales using lists of leaked or stolen phone numbers and email addresses.
- Phishing messages usually deploy psychological trickery (for example, inducing a false sense of urgency to make victims act rashly) and nearly always involve getting a victim to click on a link to a web application owned by the attacker. 
- The victim is then often asked to enter sensitive information — for example, login details or credit card information — at which point the malicious site stores the information and the attack is complete. 
- Alternatively, the victim may inadvertently install malware from the malicious page, thus giving an attacker an entry point into their device and network.

#### There are three primary types of phishing attacks:

|    **Attack Type**   |                                                                                                                                                                                        **Definition**                                                                                                                                                                                       |
|:---------------------:|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| **General Phishing** | A simple, mass phishing attack which doesn't target anyone in particular, although they may aim for large groups (e.g. PayPal users, or Amazon customers). <br> These large-scale campaigns are usually simple and are generally (but not always) fairly easy to spot as the messages and malicious sites are often not very well crafted and frequently contain many immediately visible errors. |
|   **Spearphishing**  |         More targeted than general phishing, spearphishing aims for an individual or small group (e.g. employees of a specific company). <br> Spearphishing campaigns are generally better crafted than the correspondence and malicious sites used in general phishing as they are designed to target a particular group, often as part of a more extensive campaign against the target.         |
|      **Whaling**     |                                                                                       Even more specific than spearphishing, whaling targets high-value individuals (e.g. a C-Suite executive in a target company). <br> The messages are generally extremely well crafted and tend to be very hard to spot.                                                                                      |

- Be aware that you are much more likely to encounter a general phishing attack than a spearphishing or whaling attack in your day-to-day life. 
- This may not be the case in your work life, however — especially if you are a high-ranking member of a company.
- An example of a popular general phishing scenario (or "pretext") would be receiving an email purportedly from "Amazon", informing you that your account has been used to buy a very costly item (e.g. the latest iPad). 
- You are then provided with a link to view your purchase history. 
- The link looks like it goes to https://amazon.co.uk but will actually take you to an attacker-controlled web application (that looks identical to the Amazon login page), asking you to enter your Amazon credentials. 
- When you enter your credentials, you get redirected to the real Amazon orders page, where you find that there are no unauthorised purchases... yet. 
- The attacker will then use your duly provided credentials to actually order expensive items with your account.

#### This process is shown in the following diagram:






---

# [Task 4  `Common Attacks` Malware and Ransomware]()

---

# [Task 5  `Common Attacks` Passwords and Authentication]()

---

# [Task 6  `Staying Safe` Multi-Factor Authentication and Password Managers]()

---

# [Task 7  `Staying Safe` Public Network Safety]()

---

# [Task 8  `Staying Safe` Backups]()

---

# [Task 9  `Staying Safe` Updates and Patches]()

---

# [Task 10  `Information` Conclusion]()

---
