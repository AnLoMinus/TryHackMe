![image](https://user-images.githubusercontent.com/51442719/202955252-74b0159b-d99d-492b-a132-ec124e60d24a.png)

# [Zeek Exercises](https://tryhackme.com/room/zeekbroexercises)

![image](https://user-images.githubusercontent.com/51442719/202955267-f21bcf55-9c72-4740-9f3c-ffc212cb2da3.png)

### Put your Zeek skills into practice and analyse network traffic.

---

- [Task 1  Introduction](#task-1--introduction)
- [Task 2  Anomalous DNS](#task-2--anomalous-dns)
- [Task 3  Phishing](#task-3--phishing)
- [Task 4  Log4J](#task-4--log4j)
- [Task 5  Conclusion](#task-5--conclusion)

---

## Task 1  Introduction

![image](https://user-images.githubusercontent.com/51442719/202955445-ec9af39a-3267-4295-919e-ef55e22c4a73.png)

The room invites you a challenge to investigate a series of traffic data and stop malicious activity under different scenarios. Let's start working with Zeek to analyse the captured traffic.

We recommend completing the [Zeek](https://tryhackme.com/room/zeekbro) room first, which will teach you how to use the tool in depth.

A VM is attached to this room. You don't need SSH or RDP; the room provides a "Split View" feature. Exercise files are located in the folder on the desktop. Log cleaner script "clear-logs.sh" is available in each exercise folder.

![image](https://user-images.githubusercontent.com/51442719/202955492-3c43b2d7-3259-43c9-b038-32524ed112a1.png)

---

## Task 2  Anomalous DNS


---

## Task 3  Phishing

### Answer the questions below
Investigate the logs. What is the suspicious source address? Enter your answer in defanged format.
- Answer format: `10[.]6[.]27[.]102`

Investigate the http.log file. Which domain address were the malicious files downloaded from? Enter your answer in defanged format.
- Answer format: `smart-fax[.]com`

Investigate the malicious document in VirusTotal. What kind of file is associated with the malicious document?
>
- Answer format: `Answer format: ***`

Investigate the extracted malicious .exe file. What is the given file name in Virustotal?
- Answer format: ****************.***

Investigate the malicious .exe file in VirusTotal. What is the contacted domain name? Enter your answer in defanged format.
- Answer format: ******.****

Investigate the http.log file. What is the request name of the downloaded malicious .exe file?
- Answer format: `***.***`


---

## Task 4  Log4J

---

## Task 5  Conclusion
