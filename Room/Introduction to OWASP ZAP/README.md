
![image](https://user-images.githubusercontent.com/51442719/172146036-5177246d-0cef-4760-8a65-71190766bffc.png)

- [ ] [Introduction to OWASP ZAP](https://tryhackme.com/room/learnowaspzap)
  > Learn how to use OWASP ZAP from the ground up. An alternative to BurpSuite.
    - [x] Task 1  Intro to ZAP
![image](https://user-images.githubusercontent.com/51442719/172452066-dbc51a6a-a015-4110-8f91-35de554bedaf.png)
    - There’s a couple of feature benefits too with using OWASP ZAP over Burp Suite:
      - Automated Web Application Scan: This will automatically passively and actively scan a web application, build a sitemap, and discover vulnerabilities. This is a paid feature in Burp. 
      - Web Spidering: You can passively build a website map with Spidering. This is a paid feature in Burp.
      - Unthrottled Intruder: You can bruteforce login pages within OWASP as fast as your machine and the web-server can handle. This is a paid feature in Burp.
      - No need to forward individual requests through Burp: When doing manual attacks, having to change windows to send a request through the browser, and then forward in burp, can be tedious. OWASP handles both and you can just browse the site and OWASP will intercept automatically. This is NOT a feature in Burp. 

    - [x] Task 2  Disclaimer
    - [x] Task 3  Installation
    - [x] Task 4  How to perform an automated scan
    - [x] Task 5  Manual Scanning
    - [x] Task 6  Scanning an Authenticated Web Application
    - [x] Task 7  Brute-force Directories
    - [x] Task 8  Bruteforce Web Login
    - [x] Task 9  ZAP Extensions\
      > Let’s install the bugcrowd HUNT extensions for OWASP ZAP. This will passively scan for known vulnerabilities in web applications.
      - https://github.com/zaproxy/zap-extensions
      - https://github.com/bugcrowd/HUNT
    - [x] Task 10  Further Reading
