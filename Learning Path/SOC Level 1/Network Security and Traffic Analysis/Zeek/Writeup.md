ZEEK TryHackMe writeup
======================

Zeek is a free and open-source software network analysis framework.

Zeek is a network security monitor (NSM) but can also be used as a network intrusion detection system (NIDS).[(More)](https://en.wikipedia.org/wiki/Zeek)

Go Desktop/Exercise-Files/TASK-2
--------------------------------

_What is the installed Zeek instance version number?_

![](https://miro.medium.com/max/1324/1*IKrwhowoAxlzEys9L1fSMg.png)

> 4.2.1

_What is the version of the ZeekControl module?_

![](https://miro.medium.com/max/1350/1*TQcJPrhacH-cMiNXO3VBrQ.png)

> 2.4.0

_Investigate the “sample.pcap” file. What is the number of generated alert files?_

![](https://miro.medium.com/max/1304/1*IxJBHsvkYQSptThJQ2fj7g.png)

> 8

Zeek Logs
=========

Go Desktop/Exercise-Files/TASK-3
--------------------------------

_Investigate the sample.pcap file. Investigate the_ **_dhcp.log_** _file. What is the available hostname?_

*   Dhcp é um servidor que fornece ips a pcs quando se ligam á rede.

![](https://miro.medium.com/max/1400/1*fMPE4imUtbOa08Lm1B2s8A.png)

_Investigate the_ **_dns.log_** _file. What is the number of unique DNS queries?_

> 2

_Investigate the_ **_conn.log_** _file. What is the longest connection duration?_

> cat conn.log | zeek-cut id.orig\_h id.resq\_h duration | sort -rn

332.319364

Zeek Signatures
===============

Go Desktop/Exercise-Files/TASK-5
--------------------------------

_Investigate the http.pcap file. Create the HTTP signature shown in the task and investigate the pcap. What is the source IP of the first event?_

> cd Desktop/Exercise-Files/TASK-5/http
> 
> nano http-password.sig

HTTP signature:

![](https://miro.medium.com/max/870/1*A8lB3dveVNECH0rStb8bqQ.png)

Command: Save and exit

CRTL+S  
CRTL+x

Run zeek command:

> zeek -C -r http.pcap -s http-password.sig

_Investigate the http.pcap file. Create the HTTP signature shown in the task and investigate the pcap. What is the source IP of the first event?_

> cat signatures.log | zeek-cut src\_addr

10.10.57.178

_What is the source port of the second event?_

> cat signatures.log | zeek-cut src\_port

38712

_Investigate the_ **_conn.log_**_.  
What is the total number of the sent and received packets from source port 38706?_

> cat conn.log | zeek-cut id.orig\_p id.resp\_h id.resp\_p proto service orig\_pkts orig\_ip\_bytes resp\_pkts

20

_Create the global rule shown in the task and investigate the ftp.pcap file.Investigate the_ **_notice.log_**_. What is the number of unique events?_

Rule: ftp-bruteforce.sig:

![](https://miro.medium.com/max/1400/1*U6RehaZ45k_CObfbCKe-0Q.png)

> zeek -C -r ftp.pcap -s ftp-bruteforce.sig

_I_

_Investigate the_ **_notice.log_**_. What is the number of unique events?_

> cat notice.log | zeek-cut uid | sort | uniq | wc -l

1413

_What is the number of_ **_ftp-brute_** _signature matches?_

> cat signatures.log | grep “ftp-brute” | wc -l

1410

**Tip**: to see the top of the file run:

**cat notice.log | head -10**

Zeek Scripts | Fundamentals
===========================

Go Desktop/Exercise-Files/TASK-6
--------------------------------

_Investiga_t_e the smallFlows.pcap file. Investigate the_ **_dhcp.log_** _file. What is the domain value of the “vinlap01” host?_

> zeek -C -r smallFlows.pcap dhcp-hostname.zeek
> 
> cat dhcp.log

astaro\_vineyard

_Investigate the bigFlows.pcap file. Investigate the_ **_dhcp.log_** _file. What is the number of identified unique hostnames?_

> cat dhcp.log | zeek-cut host\_name | sort -rn | uniq | wc -l

18 -1

_Investigate the_ **_dhcp.log_** _file. What is the identified domain value?_

> cat dhcp.log | zeek-cut domain

jaalam.net

_Investigate the_ **_dns.log_** _file. What is the number of unique queries?_

> cat dns.log | zeek-cut query | grep -v -e’\*’ -e’-’ | sort -rn | uniq | wc -l

1109

Zeek Scripts | Scripts and Signatures
=====================================

Go to folder Desktop/Exercise-Files/TASK-5/101.
-----------------------------------------------

_Investigate the sample.pcap file with 103.zeek script. Investigate the terminal output. What is the number of the detected new connections?_

> zeek -C -r sample.pcap 103.zeek | grep “New Connection Found”| wc -l

Go to folder TASK-7/201.
------------------------

_Investigate the ftp.pcap file with ftp-admin.sig signature and 201.zeek script. Investigate the_ **_signatures.log_** _file. What is the number of signature hits?_

> zeek -C -r ftp.pcap -s ftp-admin.sig 201.zeek
> 
> cat signatures.log | grep “ftp-admin” | wc -l

1401

_Investigate the_ **_signatures.log_** _file. What is the total number of “administrator” username detections?_

> cat signatures.log | grep “administrator” | wc -l

731

_Investigate the ftp.pcap file with all local scripts, and investigate the_ **_loaded\_scripts.log_** _file. What is the total number of loaded scripts?_

> zeek -C -r ftp.pcap local
> 
> cat loaded\_scripts.log | grep “.zeek” | wc -l

498

Go to folder TASK-7/202.
------------------------

_Investigate the ftp-brute.pcap file with “/opt/zeek/share/zeek/policy/protocols/ftp/detect-bruteforcing.zeek” script. Investigate the_ **_notice.log_** _file. What is the total number of brute-force detections?_

> zeek -C -r ftp.pcap /opt/zeek/share/zeek/policy/protocols/ftp/detect-bruteforcing.zeek

2

Zeek Scripts | Frameworks
=========================

Go Desktop/Exercise-Files/TASK-8
--------------------------------

_Investigate the case1.pcap file with intelligence-demo.zeek script. Investigate the_ **_intel.log_** _file. Look at the second finding, where was the intel info found?_

> zeek -C -r case1.pcap intelligence-demo.zeek
> 
> cat intel.log

IN\_HOST\_HEADER

_Investigate the_ **_http.log_** _file. What is the name of the downloaded .exe file?_

> cat http.log | zeek-cut uri

knr.exe

_Investigate the case1.pcap file with_ **_hash-demo.zeek_** _script. Investigate the files.log file. What is the_ **_MD5_** _hash of the downloaded .exe file?_

> zeek -C -r case1.pcap hash-demo.zeek
> 
> cat files.log | zeek-cut md5

cc28e40b46237ab6d5282199ef78c464

_Investigate the case1.pcap file with_ **_file-extract-demo.zeek_** _script. Investigate the “_**_extract\_files_**_” folder. Review the contents of the text file._ **_What is written_** _in the file?_

> zeek -C -r case1.pcap /opt/zeek/share/zeek/policy/frameworks/files/extract-all-files.zeek
> 
> ls extract\_files | nl
> 
> cd extract\_files/
> 
> cat The\_Extract\_File

Microsoft NCSI

Zeek Scripts | Packages
=======================

**Go Desktop/Exercise-Files/TASK-9**
------------------------------------

_Investigate the http.pcap file with the zeek-sniffpass module. Investigate the_ **_notice.log_** _file. Which username has more module hits?_

> zeek -Cr http.pcap /opt/zeek/share/zeek/site/zeek-sniffpass

brozeek

_Investigate the case2.pcap file with geoip-conn module. Investigate the_ **_conn.log_** _file. What is the name of the identified City?_

> zeek -Cr case2.pcap /opt/zeek/share/zeek/site/geoip-conn
> 
> cat conn.log

chicago

_Which IP address is associated with the identified City?_

23.77.86.54

_Investigate the case2.pcap file with_ **_sumstats-counttable.zeek_** _script. How many types of status codes are there in the given traffic capture?_

> zeek -Cr case2.pcap sumstats-counttable.zeek

![](https://miro.medium.com/max/1400/1*YGyBrpHdrocrP3bWQFKJvA.png)
