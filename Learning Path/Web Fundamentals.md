# 🔰 [Web Fundamentals](https://tryhackme.com/path-action/web/join)

![Image not set yet](https://assets.tryhackme.com/img/paths/web.jpg)

### A pathway to web application security.
- The aim of this path is to teach you how to attack web applications. 
- To successfully attack and exploit web applications, you need to understand how they work. 
- The first section (Web Fundamentals) will give you all the pre-requisite knowledge on this. 
- The second section (Security Tools) focuses on learning how to use Industry Standard tooling to interact with your targets. 
- The third section (Vulnerabilities) covers various vulnerabilities found in web applications today. 
- This section will go over root causes of these vulnerabilities and give you hands on experience on exploiting them.
- The final section (Practise Makes Perfect) will help you apply what you've learnt in previous sections.

### After completing this path, you should be able to:
*   Understand web fundamentals
*   Major vulnerabilities explained
*   Learn industry-used tools
*   Web application assessments

- 32 Hours

- Easy

---

## How The Web Works

![image](https://user-images.githubusercontent.com/51442719/172670421-d86f8c8d-ec79-439b-bf5a-f69c5d64ff1f.png)

### To become a better hacker it's vital to understand the underlying functions of the world wide web and what makes it work.

![image](https://user-images.githubusercontent.com/51442719/172670840-00013d99-52df-44c6-a2df-830345c19928.png)
- [x] [DNS in detail](https://tryhackme.com/room/dnsindetail)
    - Learn how DNS works and how it helps you access internet services.
        - [x] Task 1  What is DNS?
        - [x] Task 2  Domain Hierarchy
        - [x] Task 3  Record Types
        - [x] Task 4  Making A Request
        - [x] Task 5  Practical

![image](https://user-images.githubusercontent.com/51442719/172670979-568a9f49-75fe-4544-b0b1-9c62481b8daa.png)
- [x] [HTTP in detail](https://tryhackme.com/room/httpindetail)
    - Learn about how you request content from a web server using the HTTP protocol
        - [x] Task 1  What is HTTP(S)?
        - [x] Task 2  Requests And Responses
        - [x] Task 3  HTTP Methods
        - [x] Task 4  HTTP Status Codes
        - [x] Task 5  Headers
        - [x] Task 6  Cookies
        - [x] Task 7  Making Requests

![image](https://user-images.githubusercontent.com/51442719/172671009-e5b5c093-5414-4966-a836-44d0c5a26266.png)
- [x] [How websites work](https://tryhackme.com/room/howwebsiteswork)
    - To exploit a website, you first need to know how they are created.
      - [x] Task 1  How websites work
      - [x] Task 2  HTML
      - [x] Task 3  JavaScript
      - [x] Task 4  Sensitive Data Exposure
      - [x] Task 5  HTML Injection

![image](https://user-images.githubusercontent.com/51442719/172671036-28090dd7-b737-427e-a2de-3687d0cbd503.png)
- [x] [Putting it all together](https://tryhackme.com/room/puttingitalltogether)
    - Learn how all the individual components of the web work together to bring you access to your favourite web sites.
      - [x] Task 1  Putting It All Together
      - [x] Task 2  Other Components
      - [x] Task 3  How Web Servers Work
      - [x] Task 4  Quiz

---
    
## Introduction to Web Hacking

![image](https://user-images.githubusercontent.com/51442719/172674865-3c734a9d-20a8-4c41-8b0a-923f9030481e.png)

### Get hands-on, learn about and exploit some of the most popular web application vulnerabilities seen in the industry today.

![image](https://user-images.githubusercontent.com/51442719/172674912-dedcdfb8-41ba-4e51-9a34-74d7cc9b4d09.png)
- [x] [Walking An Application](https://tryhackme.com/jr/walkinganapplication)
  - Manually review a web application for security issues using only your browsers developer tools. Hacking with just your browser, no tools or scripts.
    - [x] Task 1  Walking An Application
    - [x] Task 2  Exploring The Website
    - [x] Task 3  Viewing The Page Source
    - [x] Task 4  Developer Tools - Inspector
    - [x] Task 5  Developer Tools - Debugger
    - [x] Task 6  Developer Tools - Network
  
- [x] [Content Discovery](https://tryhackme.com/room/contentdiscovery)
  - Learn the various ways of discovering hidden or private content on a webserver that could lead to new vulnerabilities.
      - [x] Task 1  What Is Content Discovery?
      - [x] Task 2  Manual Discovery - Robots.txt
      - [x] Task 3  Manual Discovery - Favicon
      - [x] Task 4  Manual Discovery - Sitemap.xml
      - [x] Task 5  Manual Discovery - HTTP Headers
      - [x] Task 6  Manual Discovery - Framework Stack
      - [x] Task 7  OSINT - Google Hacking / Dorking
      - [x] Task 8  OSINT - Wappalyzer
      - [x] Task 9  OSINT - Wayback Machine
      - [x] Task 10  OSINT - GitHub
      - [x] Task 11  OSINT - S3 Buckets
      - [x] Task 12  Automated Discovery

- [x] [Subdomain Enumeration](https://tryhackme.com/room/subdomainenumeration)
  - Learn the various ways of discovering subdomains to expand your attack surface of a target.
      - [x] Task 1  Brief
      - [x] Task 2  OSINT - SSL/TLS Certificates
      - [x] Task 3  OSINT - Search Engines
      - [x] Task 4  DNS Bruteforce
      - [x] Task 5  OSINT - Sublist3r
      - [x] Task 6  Virtual Hosts

- [x] [Authentication Bypass](https://tryhackme.com/room/authenticationbypass)
  - Learn how to defeat logins and other authentication mechanisms to allow you access to unpermitted areas.
      - [x] Task 1  Brief
      - [x] Task 2  Username Enumeration
      - [x] Task 3  Brute Force
      - [x] Task 4  Logic Flaw
      - [x] Task 5  Cookie Tampering

- [x] [IDOR](https://tryhackme.com/room/idor)
  - Learn how to find and exploit IDOR vulnerabilities in a web application giving you access to data that you shouldn't have.
      - [x] Task 1  What is an IDOR?
      - [x] Task 2  An IDOR Example
      - [x] Task 3  Finding IDORs in Encoded IDs
      - [x] Task 4  Finding IDORs in Hashed IDs
      - [x] Task 5  Finding IDORs in Unpredictable IDs
      - [x] Task 6  Where are IDORs located
      - [x] Task 7  A Practical IDOR Example

- [x] [File Inclusion](https://tryhackme.com/room/fileinc)
  - This room introduces file inclusion vulnerabilities, including Local File Inclusion (LFI), Remote File Inclusion (RFI), and directory traversal.
      - [x] Task 1  Introduction
      - [x] Task 2  Deploy the VM
      - [x] Task 3  Path Traversal
      - [x] Task 4  Local File Inclusion - LFI
      - [x] Task 5  Local File Inclusion - LFI #2
      - [x] Task 6  Remote File Inclusion - RFI
      - [x] Task 7  Remediation
      - [x] Task 8  Challenge

- [x] [SSRF](https://tryhackme.com/room/ssrfqi)
  - Learn how to exploit Server-Side Request Forgery (SSRF) vulnerabilities, allowing you to access internal server resources.
      - [x] Task 1  What is an SSRF?
      - [x] Task 2  SSRF Examples
      - [x] Task 3  Finding an SSRF
      - [x] Task 4  Defeating Common SSRF Defenses
      - [x] Task 5  SSRF Practical

- [x] [Cross-site Scripting](https://tryhackme.com/room/xssgi)
  - Learn how to detect and exploit XSS vulnerabilities, giving you control of other visitor's browsers.
      - [x] Task 1  Room Brief
      - [x] Task 2  XSS Payloads
      - [x] Task 3  Reflected XSS
      - [x] Task 4  Stored XSS
      - [x] Task 5  DOM Based XSS
      - [x] Task 6  Blind XSS
      - [x] Task 7  Perfecting your payload
      - [x] Task 8  Practical Example (Blind XSS)

- [x] [Command Injection](https://tryhackme.com/room/oscommandinjection)
  - Learn about a vulnerability allowing you to execute commands through a vulnerable app, and its remediations.
      - [x] Task 1  Introduction (What is Command Injection?)
      - [x] Task 2  Discovering Command Injection
      - [x] Task 3  Exploiting Command Injection
      - [x] Task 4  Remediating Command Injection
      - [x] Task 5  Practical: Command Injection (Deploy)
      - [x] Task 6  Conclusion

- [x] [SQL Injection](https://tryhackme.com/room/sqlinjectionlm)
  - Learn how to detect and exploit SQL Injection vulnerabilities
      - [x] Task 1  Brief
      - [x] Task 2  What is a Database?
      - [x] Task 3  What is SQL?
      - [x] Task 4  What is SQL Injection?
      - [x] Task 5  In-Band SQLi
      - [x] Task 6  Blind SQLi - Authentication Bypass
      - [x] Task 7  Blind SQLi - Boolean Based
      - [x] Task 8  Blind SQLi - Time Based
      - [x] Task 9  Out-of-Band SQLi
      - [x] Task 10  Remediation

## Burp Suite
![image](https://user-images.githubusercontent.com/51442719/172675426-3fd167f5-cd3e-4359-960f-9747837f05d5.png)
### Burp Suite is the industry standard tool for web application hacking, and is essential in any web penetration test

- [x] [Burp Suite: The Basics](https://tryhackme.com/jr/burpsuitebasics)
  - An introduction to using Burp Suite for Web Application pentesting

- [x] [Burp Suite: Repeater](https://tryhackme.com/jr/burpsuiterepeater)
  - Learn how to use Repeater to duplicate requests in Burp Suite

- [x] [Burp Suite: Intruder](https://tryhackme.com/jr/burpsuiteintruder)
  - Learn how to use Intruder to automate requests in Burp Suite

- [x] [Burp Suite: Other Modules](https://tryhackme.com/jr/burpsuiteom)
  - Take a dive into some of Burp Suite's lesser known modules

- [x] [Burp Suite: Extender](https://tryhackme.com/jr/burpsuiteextender)
  - Learn how to use Extender to broaden the functionality of Burp Suite
  
## Web Hacking Fundamentals
![image](https://user-images.githubusercontent.com/51442719/172675447-16ccf585-7630-4df4-bd4e-58c3efa78784.png)
### Understand the core security issues with web applications, and learn how to exploit them using industry tools and techniques.

![image](https://user-images.githubusercontent.com/51442719/172671009-e5b5c093-5414-4966-a836-44d0c5a26266.png)
- [x] [How websites work](https://tryhackme.com/room/howwebsiteswork)
    - To exploit a website, you first need to know how they are created.
      - [x] Task 1  How websites work
      - [x] Task 2  HTML
      - [x] Task 3  JavaScript
      - [x] Task 4  Sensitive Data Exposure
      - [x] Task 5  HTML Injection

![image](https://user-images.githubusercontent.com/51442719/172670979-568a9f49-75fe-4544-b0b1-9c62481b8daa.png)
- [x] [HTTP in detail](https://tryhackme.com/room/httpindetail)
    - Learn about how you request content from a web server using the HTTP protocol
        - [x] Task 1  What is HTTP(S)?
        - [x] Task 2  Requests And Responses
        - [x] Task 3  HTTP Methods
        - [x] Task 4  HTTP Status Codes
        - [x] Task 5  Headers
        - [x] Task 6  Cookies
        - [x] Task 7  Making Requests

![image](https://user-images.githubusercontent.com/51442719/172676701-fd7908c6-9ef7-404d-a02f-fbc699e3eb51.png)
- [x] [Burp Suite: The Basics](https://tryhackme.com/room/burpsuitebasics)
  - An introduction to using Burp Suite for Web Application pentesting
      - [x] Task 1  Introduction Outline
      - [x] Task 2  `Getting Started` What is Burp Suite?
      - [x] Task 3  `Getting Started` Features of Burp Community
      - [x] Task 4  `Getting Started` Installation
      - [x] Task 5  `Getting Started` The Dashboard
      - [x] Task 6  `Getting Started` Navigation
      - [x] Task 7  `Getting Started` Options
      - [x] Task 8  `Proxy` Introduction to the Burp Proxy
      - [x] Task 9  `Proxy` Connecting through the Proxy (FoxyProxy)
      - [x] Task 10  `Proxy` Proxying HTTPS
      - [x] Task 11  `Proxy` The Burp Suite Browser
      - [x] Task 12  `Proxy` Scoping and Targeting
      - [x] Task 13  `Proxy` Site Map and Issue Definitions
      - [x] Task 14  `Practical` Example Attack
      - [x] Task 15  `Conclusion` Room Conclusion

![image](https://user-images.githubusercontent.com/51442719/172677070-25439260-d06c-40d1-b75d-f25a76e1d17e.png)
- [x] [OWASP Top 10](https://tryhackme.com/room/owasptop10)
  - Learn about and exploit each of the OWASP Top 10 vulnerabilities; the 10 most critical web security risks.
      - [x] Task 1  Introduction
      - [x] Task 2  Accessing machines
      - [x] Task 3  [Severity 1] Injection
      - [x] Task 4  [Severity 1] OS Command Injection
      - [x] Task 5  [Severity 1] Command Injection Practical
      - [x] Task 6  [Severity 2] Broken Authentication
      - [x] Task 7  [Severity 2] Broken Authentication Practical
      - [x] Task 8  [Severity 3] Sensitive Data Exposure (Introduction)
      - [x] Task 9  [Severity 3] Sensitive Data Exposure (Supporting Material 1)
      - [x] Task 10  [Severity 3] Sensitive Data Exposure (Supporting Material 2)
      - [x] Task 11  [Severity 3] Sensitive Data Exposure (Challenge)
      - [x] Task 12  [Severity 4] XML External Entity
      - [x] Task 13  [Severity 4 XML External Entity - eXtensible Markup Language
      - [x] Task 14  [Severity 4] XML External Entity - DTD
      - [x] Task 15  [Severity 4] XML External Entity - XXE Payload
      - [x] Task 16  [Severity 4] XML External Entity - Exploiting
      - [x] Task 17  [Severity 5] Broken Access Control
      - [x] Task 18  [Severity 5] Broken Access Control (IDOR Challenge)
      - [x] Task 19  [Severity 6] Security Misconfiguration
      - [x] Task 20  [Severity 7] Cross-site Scripting
      - [x] Task 21  [Severity 8] Insecure Deserialization
      - [x] Task 22  [Severity 8] Insecure Deserialization - Objects
      - [x] Task 23  [Severity 8] Insecure Deserialization - Deserialization
      - [x] Task 24  [Severity 8] Insecure Deserialization - Cookies
      - [x] Task 25  [Severity 8] Insecure Deserialization - Cookies Practical
      - [x] Task 26  [Severity 8] Insecure Deserialization - Code Execution
      - [x] Task 27  [Severity 9] Components With Known Vulnerabilities - Intro
      - [x] Task 28  [Severity 9] Components With Known Vulnerabilities - Exploit
      - [x] Task 29  [Severity 9] Components With Known Vulnerabilities - Lab
      - [x] Task 30  [Severity 10] Insufficient Logging and Monitoring
      - [x] Task 31  What Next?

![image](https://user-images.githubusercontent.com/51442719/172683987-ab31ba4f-3a27-4076-a55a-df3f60c1a92a.png)
- [x] [OWASP Juice Shop](https://tryhackme.com/room/owaspjuiceshop)
  - This room uses the Juice Shop vulnerable web application to learn how to identify and exploit common web application vulnerabilities.
      - [x] Task 1  Open for business!
      - [x] Task 2  Let's go on an adventure!
      - [x] Task 3  Inject the juice
      - [x] Task 4  Who broke my lock?!
      - [x] Task 5  AH! Don't look!
      - [x] Task 6  Who's flying this thing?
      - [x] Task 7  Where did that come from?
      - [x] Task 8  Exploration!

![image](https://user-images.githubusercontent.com/51442719/172671036-28090dd7-b737-427e-a2de-3687d0cbd503.png)
- [ ] [Upload Vulnerabilities](https://tryhackme.com/room/uploadvulns)
  - Tutorial room exploring some basic file-upload vulnerabilities in websites
      - [x] Task 1  Getting Started
      - [x] Task 2  Introduction
      - [x] Task 3  General Methodology
      - [x] Task 4  Overwriting Existing Files
      - [x] Task 5  Remote Code Execution
      - [x] Task 6  Filtering
      - [ ] Task 7  Bypassing Client-Side Filtering
      - [ ] Task 8  Bypassing Server-Side Filtering: File Extensions
      - [ ] Task 9  Bypassing Server-Side Filtering: Magic Numbers
      - [ ] Task 10  Example Methodology
      - [ ] Task 11  Challenge
      - [ ] Task 12  Conclusion

![image](https://user-images.githubusercontent.com/51442719/172684156-362eba73-1a44-415d-9bb2-5b5f28efa3ac.png)
- [x] [Pickle Rick](https://tryhackme.com/room/picklerick)
  - A Rick and Morty CTF. Help turn Rick back into a human!
    - [x] Task 1  Pickle Rick
