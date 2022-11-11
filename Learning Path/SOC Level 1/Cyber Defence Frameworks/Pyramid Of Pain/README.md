![image](https://user-images.githubusercontent.com/51442719/201240460-a3cef579-ac9c-4367-99ed-dfd583e44bde.png)

### [Pyramid Of Pain](https://tryhackme.com/room/pyramidofpainax)
#### Learn what is the Pyramid of Pain and how to utilize this model to determine the level of difficulty it will cause for an adversary to change the indicators associated with them, and their campaign.

---

- [Task 1  Introduction](#)
- [Task 2  Hash Values (Trivial)](#)
- [Task 3  IP Address (Easy)](#)
- [Task 4  Domain Names (Simple)](#)
- [Task 5  Host Artifacts (Annoying)](#)
- [Task 6  Network Artifacts (Annoying)](#)
- [Task 7  Tools (Challenging)](#)
- [Task 8  TTPs (Tough)](#)
- [Task 9  Practical: The Pyramid of Pain](#)
- [Task 10  Conclusion](#)


---

## Task 1  Introduction

![image](https://user-images.githubusercontent.com/51442719/201240599-9d5c736c-0c3f-4850-8113-478054232fbc.png)

Below is the breakdown of each indicator:

- Hash Values (`TRIVIAL`): SHA1, MD5, SHA256 or other similar hashes that identify a suspicious or malicious file. It is trivial for the adversary to change the value of the hash bypassing the defensive capability: For example, polymorphic or metamorphic techniques.

- IP Addresses (`EASY`): IP addresses are used as an identifier and can be easily hidden by using an anonymous proxy service (like Tor) or they can be changed at high frequency such as leveraging fast flux.

- Domain Names (`SIMPLE`): Domain names (e.g., “internetbadguys.com”) and/or or sub domain (e.g., “exploitkit.internetbadguys.com”). These domains are registered and hosted and can be part of the adversary’s attack infrastructure. The attackers can simply bypass these controls using techniques such as DGAs (Domain Generated Algorithms).

- Network Artifacts (`ANNOYING`): This refers to the ability to determine suspicious or malicious activity from legitimate activity. It goes beyond a user device and includes all Internet of Things (IoT) devices. Examples may include patterns based on network activity (C2 information), Uniform Resource Identifier (URI) patterns, certificates of use, and so on.

- Host Artifacts (`ANNOYING`): This may include an artifact in the registry, a scheduled task, or files dropped within the file system that indicates the presence of malicious activity.

- Tools (`CHALLENGING`): This would typically be software that the adversary brings with them to perform a variety of activities such as creating backdoors for a C2 channel, network sniffers, and password crackers.

- Tactics, Techniques and Procedures – TTPs (`TOUGH`): The tactic provides the description of the behavior, the technique provides more details of the behavior from the perspective of the tactic, and the procedure would provide deep details around the technique itself. Example: The Tactic is “Discovery” and technique being used is “Network Service Scanning.”

---

This well-renowned concept is being applied to cybersecurity solutions like [Cisco Security](https://gblogs.cisco.com/ca/2020/08/26/the-canadian-bacon-cisco-security-and-the-pyramid-of-pain/), [SentinelOne](https://www.sentinelone.com/blog/revisiting-the-pyramid-of-pain-leveraging-edr-data-to-improve-cyber-threat-intelligence/), and [SOCRadar](https://socradar.io/re-examining-the-pyramid-of-pain-to-use-cyber-threat-intelligence-more-effectively/) to improve the effectiveness of CTI (Cyber Threat Intelligence), threat hunting, and incident response exercises.

Understanding the Pyramid of Pain concept as a Threat Hunter, Incident Responder, or SOC Analyst is important.

Are you ready to explore what hides inside the Pyramid of Pain? 


---

## Task 2  Hash Values (Trivial)

As per Microsoft, the hash value is a numeric value of a fixed length that uniquely identifies data. A hash value is the result of a hashing algorithm. The following are some of the most common hashing algorithms: 

- MD5 (Message Digest, defined by [RFC 1321](https://www.ietf.org/rfc/rfc1321.txt)) - was designed by Ron Rivest in 1992 and is a widely used cryptographic hash function with a 128-bit hash value. MD5 hashes are NOT considered cryptographically secure. In 2011, the IETF published RFC 6151, "[Updated Security Considerations for the MD5 Message-Digest and the HMAC-MD5 Algorithms](https://datatracker.ietf.org/doc/html/rfc6151)," which mentioned a number of attacks against MD5 hashes, including the hash collision.
- SHA-1 (Secure Hash Algorithm 1, defined by [RFC 3174](https://tools.ietf.org/html/rfc3174)) - was invented by United States National Security Agency in 1995. When data is fed to SHA-1 Hashing Algorithm, SHA-1 takes an input and produces a 160-bit hash value string as a 40 digit hexadecimal number. [NIST deprecated the use of SHA-1 in 2011](https://csrc.nist.gov/news/2017/research-results-on-sha-1-collisions) and banned its use for digital signatures at the end of 2013 based on it being susceptible to brute-force attacks. Instead, NIST recommends migrating from SHA-1 to stronger hash algorithms in the SHA-2 and SHA-3 families.
- The SHA-2 (Secure Hash Algorithm 2) - SHA-2 Hashing Algorithm was designed by The National Institute of Standards and Technology (NIST) and the National Security Agency (NSA) in 2001 to replace SHA-1. SHA-2 has many variants, and arguably the most common is SHA-256. The SHA-256 algorithm returns a hash value of 256-bits as a 64 digit hexadecimal number.
A hash is not considered to be cryptographically secure if two files have the same hash value or digest.

Security professionals usually use the hash values to gain insight into a specific malware sample, a malicious or a suspicious file, and as a way to uniquely identify and reference the malicious artifact.

You probably read the ransomware reports in the past, where security researchers would provide the hashes related to the malicious or suspicious files used at the end of the report. You can check out The [DFIR Report](https://thedfirreport.com/) and [FireEye Threat Research Blogs](https://www.fireeye.com/blog/threat-research.html) if you’re interested in seeing an example.

Various online tools can be used to do hash lookups like [VirusTotal](https://www.virustotal.com/gui/) and [Metadefender Cloud - OPSWAT](https://metadefender.opswat.com/?lang=en).

### VirusTotal:

![image](https://user-images.githubusercontent.com/51442719/201246775-d2e995c3-9dbf-43f1-9bf9-3f87587d9d22.png)

### MetaDefender Cloud - OPSWAT:

![image](https://user-images.githubusercontent.com/51442719/201246803-886262a1-d02f-405e-9dce-a1ca2866c808.png)

As you might have noticed, it is really easy to spot a malicious file if we have the hash in our arsenal.  However, as an attacker, it’s trivial to modify a file by even a single bit, which would produce a different hash value. With so many variations and instances of known malware or ransomware, threat hunting using file hashes as the IOC (Indicators of Compromise) can become a difficult task.

Let’s take a look at an example of how you can change the hash value of a file by simply appending a string to the end of a file using echo: File Hash (Before Modification)

```powershell
PS C:\Users\THM\Downloads> Get-FileHash .\OpenVPN_2.5.1_I601_amd64.msi -Algorithm MD5
Algorithm Hash                             Path                                                 
_________ ____                             ____                                                 
MD5       D1A008E3A606F24590A02B853E955CF7 C:\Users\THM\Downloads\OpenVPN_2.5.1_I601_amd64.msi
```

```powershell
PS C:\Users\THM\Downloads> echo "AppendTheHash" >> .\OpenVPN_2.5.1_I601_amd64.msi
PS C:\Users\THM\Downloads> Get-FileHash .\OpenVPN_2.5.1_I601_amd64.msi -Algorithm MD5
Algorithm Hash                             Path                                                 
_________ ____                             ____                                                 
MD5       9D52B46F5DE41B73418F8E0DACEC5E9F C:\Users\THM\Downloads\OpenVPN_2.5.1_I601_amd64.msi
```




---

## Task 3  IP Address (Easy)

You may have learned the importance of an IP Address from the "[What is Networking](https://tryhackme.com/room/whatisnetworking)?" Room. the importance of the IP Address. An IP address is used to identify any device connected to a network. These devices range from desktops, to servers and even CCTV cameras!. We rely on IP addresses to send and receive the information over the network. But we are not going to get into the structure and functionality of the IP address. As a part of the Pyramid of Pain, we’ll evaluate how IP addresses are used as an indicator.

In the Pyramid of Pain, IP addresses are indicated with the color green. You might be asking why and what you can associate the green colour with?

From a defense standpoint, knowledge of the IP addresses an adversary uses can be valuable. A common defense tactic is to block, drop, or deny inbound requests from IP addresses on your parameter or external firewall. This tactic is often not bulletproof as it’s trivial for an experienced adversary to recover simply by using a new public IP address.

Malicious IP connections ([app.any.run](https://app.any.run/tasks/a66178de-7596-4a05-945d-704dbf6b3b90)):

![image](https://user-images.githubusercontent.com/51442719/201247070-24a33d78-77a5-477d-8d44-3f37c7bad524.png)

> `NOTE`! Do not attempt to interact with the IP addresses shown above.

One of the ways an adversary can make it challenging to successfully carry out IP blocking is by using Fast Flux.

According to [Akamai](https://blogs.akamai.com/2017/10/digging-deeper-an-in-depth-analysis-of-a-fast-flux-network-part-one.html), Fast Flux is a DNS technique used by botnets to hide phishing, web proxying, malware delivery, and malware communication activities behind compromised hosts acting as proxies. The purpose of using the Fast Flux network is to make the communication between malware and its command and control server (C&C) challenging to be discovered by security professionals. 

So, the primary concept of a Fast Flux network is having multiple IP addresses associated with a domain name, which is constantly changing. Palo Alto created a great fictional scenario to explain Fast Flux: "[Fast Flux 101: How Cybercriminals Improve the Resilience of Their Infrastructure to Evade Detection and Law Enforcement Takedowns](https://unit42.paloaltonetworks.com/fast-flux-101/)"

Use the following [any.run](https://app.any.run/tasks/a66178de-7596-4a05-945d-704dbf6b3b90/) URL to answer the questions below:


---

## Task 4  Domain Names (Simple)

---

## Task 5  Host Artifacts (Annoying)

---

## Task 6  Network Artifacts (Annoying)

---

## Task 7  Tools (Challenging)

---

## Task 8  TTPs (Tough)

---

## Task 9  Practical: The Pyramid of Pain

---

## Task 10  Conclusion
