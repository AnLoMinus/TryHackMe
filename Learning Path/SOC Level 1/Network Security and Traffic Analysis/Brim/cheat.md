### File: task4-sample-b.pcap
#### Exercise: Threat Hunting with Brim | Malware C2 Detection

Investigate the files. What is the name of the detected GIF file?

- `filename!=null | cut _path, tx_hosts, rx_hosts, conn_uids, mime_type, filename, md5, sha1`


Investigate the conn logfile. What is the number of the identified city names?

- `_path==”conn” | put classnet := network_of(id.resq_h) | cut geo.resq.region,geo.resp.city`

Cities:

- 1.Eppelborn
- 2.Frankfurt am Main

Investigate the Suricata alerts. What is the Signature id of the alert category “Potential Corporate Privacy Violation”?

---

### File:task6-malware-c2.pcap
#### Exercise: Threat Hunting with Brim | Malware C2 Detection

What is the name of the file downloaded from the CobaltStrike C2 connection?

- `_path==”http” | cut id.orig_h, id.resp_h, id.resp_p, method, host, uri | uniq -c`

4564.exe

What is the number of CobaltStrike connections using port 443?

- `_path==”conn” | 104.168.44.45 | 443 | count()`

328

There is an additional C2 channel in used the given case. What is the name of the secondary C2 channel?

Icedid

---

### File: task7-crypto-mine.pcapng
#### Exercise: Threat Hunting with Brim | Crypto Mining

How many connections used port 19999?

- `_path==”conn” | 19999 | count()`

What is the name of the service used by port 6666?

- `_path==”conn” | 6666 | cut service`

What is the amount of transferred total bytes to “101.201.172.235:8888”?

- `_path==”conn” | 101.201.172.235 | 8888`

What is the detected MITRE tactic id?

- `event_type==”alert”`
