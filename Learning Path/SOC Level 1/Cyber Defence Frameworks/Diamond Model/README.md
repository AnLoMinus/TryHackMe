![image](https://user-images.githubusercontent.com/51442719/201397736-af7c6f30-66a3-4bb2-8b4d-39a87608107e.png)

# [Diamond Model](https://tryhackme.com/room/diamondmodelrmuwwg42)

![image](https://user-images.githubusercontent.com/51442719/201397719-3475e7e4-1da0-4dbb-aad6-071014ab9a1f.png)

### Learn about the four core features of the Diamond Model of Intrusion Analysis: adversary, infrastructure, capability, and victim.

---

- [Task 1  Introduction](#)
- [Task 2  Adversary](#)
- [Task 3  Victim](#)
- [Task 4  Capability](#)
- [Task 5  Infrastructure](#)
- [Task 6  Event Meta Features](#)
- [Task 7  Social-Political Component](#)
- [Task 8  Technology Component](#)
- [Task 9  Practice Analysis](#)
- [Task 10  Conclusion](#)

---

## Task 1  Introduction

**What is The Diamond Model?**

The Diamond Model of Intrusion Analysis was developed by cybersecurity professionals - Sergio Caltagirone, Andrew Pendergast, and Christopher Betz in 2013.

[As described by its creators](https://www.activeresponse.org/wp-content/uploads/2013/07/diamond.pdf), the Diamond Model is composed of four core features: adversary, infrastructure, capability, and victim, and establishes the fundamental atomic element of any intrusion activity.  
You might have also noticed two additional components or axes of the Diamond Model - Social, Political and Technology; we will go into a little bit more detail about them later in this room.  
Why is it called a "Diamond Model"? The four core features are edge-connected, representing their underlying relationships and arranged in the shape of a diamond. 

The Diamond Model carries the essential concepts of intrusion analysis and adversary operations while allowing the flexibility to expand and encompass new ideas and concepts.  
The model provides various opportunities to integrate intelligence in real-time for network defence, automating correlation across events, classifying events with confidence into adversary campaigns, and forecasting adversary operations while planning and gaming mitigation strategies.

> Why should you learn about The Diamond Model?

The Diamond Model can help you identify the elements of an intrusion.  
At the end of this room, you will create a Diamond Model for events such as a breach, intrusion, attack, or incident.  
You will also be able to analyze an Advanced Persistent Threat (APT). 

The Diamond Model can also help explain to other people who are non-technical about what happened during an event or any valuable information on the malicious threat actor.

---

## Task 2  Adversary

**Who is an Adversary?**

An adversary is also known as an attacker, enemy, cyber threat actor, or hacker.  
The adversary is the person who stands behind the cyberattack.  
Cyberattacks can be an instruction or a breach.

According to the creators of the Diamond Model,  an adversary is an actor or organization responsible for utilizing a capability against the victim to achieve their intent.  
Adversary knowledge can generally be mysterious, and this core feature is likely to be empty for most events – at least at the time of discovery. 

It is essential to know the distinction between adversary operator and adversary customer because it will help you understand intent, attribution, adaptability, and persistence by helping to frame the relationship between an adversary and victim pair.  

It is difficult to identify an adversary during the first stages of a cyberattack.  
Utilizing data collected from an incident or breach, signatures, and other relevant information can help you determine who the adversary might be.

Adversary Operator is the “hacker” or person(s) conducting the intrusion activity.

Adversary Customer is the entity that stands to benefit from the activity conducted in the intrusion.  
It may be the same person who stands behind the adversary operator, or it may be a separate person or group.

As an example, an adversary customer could control different operators simultaneously.  
Each operator might have its capabilities and infrastructure.

---

## Task 3  Victim

`Victim` – is a target of the adversary.  
A victim can be an organization, person, target email address, IP address, domain, etc.  
It's essential to understand the difference between the victim persona and the victim assets because they serve different analytic functions. 

A victim can be an opportunity for the attackers to get a foothold on the organization they are trying to attack.  
There is always a victim in every cyberattack.  
For example, the spear-phishing email (a well-crafted email targeting a specific person of interest) was sent to the company, and someone (victim) clicked on the link.  
In this case, the victim is the selected target of interest for an adversary. 

`Victim Personae` are the people and organizations being targeted and whose assets are being attacked and exploited.  
These can be organization names, people’s names, industries, job roles, interests, etc.

`Victim Assets` are the attack surface and include the set of systems, networks, email addresses, hosts, IP addresses, social networking accounts, etc., to which the adversary will direct their capabilities.

---

## Task 4  Capability

`Capability` – is also known as the skill, tools, and techniques used by the adversary in the event.  
The capability highlights the adversary’s tactics, techniques, and procedures (TTPs). 

The capability can include all techniques used to attack the victims, from the less sophisticated methods, such as manual password guessing, to the most sophisticated techniques, like developing malware or a malicious tool. 

`Capability Capacity` is all of the vulnerabilities and exposures that the individual capability can use. 

An `Adversary Arsenal` is a set of capabilities that belong to an adversary.  
The combined capacities of an adversary's capabilities make it the adversary's arsenal.

An adversary must have the required capabilities.  
The capabilities can be malware and phishing email development skills or, at least, access to capabilities, such as acquiring malware or ransomware as a service.


---

## Task 5  Infrastructure

---

## Task 6  Event Meta Features

---

## Task 7  Social-Political Component

---

## Task 8  Technology Component

---

## Task 9  Practice Analysis

---

## Task 10  Conclusion
