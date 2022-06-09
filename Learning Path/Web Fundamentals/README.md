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

## The Learning Path

- [x] [How The Web Works](#how-the-web-works)
  - To become a better hacker it's vital to understand the underlying functions of the world wide web and what makes it work.

- [x] [Introduction to Web Hacking](#introduction-to-web-hacking)
  - Get hands-on, learn about and exploit some of the most popular web application vulnerabilities seen in the industry today.

- [x] [Burp Suite](#burp-suite)
  - Burp Suite is the industry standard tool for web application hacking, and is essential in any web penetration test

- [ ] [Web Hacking Fundamentals](#web-hacking-fundamentals)
  - Understand the core security issues with web applications, and learn how to exploit them using industry tools and techniques.


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
