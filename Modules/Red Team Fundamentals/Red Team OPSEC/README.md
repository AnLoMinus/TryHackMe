## 🔶 `VIP` [Red Team OPSEC](https://tryhackme.com/jr/opsec)
> Learn how to apply Operations Security (OPSEC) process for Red Teams.
- [x] [Task 1  Introduction](#task-1--introduction)
- [x] [Task 2  Critical Information Identification](#task-2--critical-information-identification)
- [x] [Task 3  Threat Analysis](#task-3--threat-analysis)
- [x] [Task 4  Vulnerability Analysis](#task-4--vulnerability-analysis)
- [x] [Task 5  Risk Assessment](#task-5--risk-assessment)
- [ ] [Task 6  Countermeasures](#task-6--countermeasures)
- [ ] [Task 7  More Practical Examples](#task-7--more-practical-examples)
- [ ] [Task 8  Summary](#task-8--summary)

---
- (`OPSEC`) - Operational Security 
- (`SIEM`) - Security Information and Event Management 
- (`IDS`) - Intrusion Detection System 
---

## [Task 1  Introduction]()
- Operations Security (OPSEC) is a term coined by the United States military. 
- In the field of cybersecurity, let’s start with the definition provided by [`NIST`](https://csrc.nist.gov/glossary/term/opsec):

- Systematic and proven process by which potential adversaries can be denied information about capabilities and intentions by identifying, controlling, and protecting generally unclassified evidence of the planning and execution of sensitive activities. 
- The process involves five steps: 
  - identification of critical information
  - analysis of threats
  - analysis of vulnerabilities
  - assessment of risks
  - and application of appropriate countermeasures

- Let’s dive into the definition from a red team perspective. 
- As a red team member, your potential adversaries are the blue team and third parties. 
- The blue team is considered an adversary as we are attacking the systems they are hired to monitor and defend. 
- Red vs. blue team exercises are common to help an organization understand what threats exist in a given environment and better prepare their blue team if a real malicious attack occurs. 
- As red teamers, even though we are abiding by the law and authorized to attack systems within a defined scope, it does not change the fact that we are acting against the blue team's objectives and trying to circumvent their security controls. 
- The blue team wants to protect their systems, while we want to penetrate them.

- Denying any potential adversary the ability to gather information about our capabilities and intentions is critical to maintaining OPSEC. 
- OPSEC is a process to identify, control and protect any information related to the planning and execution of our activities. 
- Frameworks such as [`Lockheed Martin's Cyber Kill Chain`](https://www.lockheedmartin.com/en-us/capabilities/cyber/cyber-kill-chain.html) and [`MITRE ATT&CK`](https://attack.mitre.org/) help defenders identify the objectives an adversary is trying to accomplish. 
- MITRE ATT&CK is arguably at the forefront of reporting and classifying adversary tactics, techniques, and procedures (TTPs) and offers a publicly accessible knowledge base as publicly available threat intelligence and incident reporting as its primary data source.

<div align="center">
  <img src="https://user-images.githubusercontent.com/51442719/180426984-5b214f55-4eff-46fd-8af3-eb2aa9fc78a9.png" width="555">
</div>

- The OPSEC process has five steps:
  - Identify critical information
  - Analyse threats
  - Analyse vulnerabilities
  - Assess risks
  - Apply appropriate countermeasures
- If the adversary discovers that you are scanning their network with Nmap (the blue team in our case), they should easily be able to discover the IP address used. 
- For instance, if you use this same IP address to host a phishing site, it won’t be very difficult for the blue team to connect the two events and attribute them to the same actor.

- OPSEC is not a solution or a set of rules; OPSEC is a five-step process to deny adversaries from gaining access to any critical information (defined in Task 2). 
- We will dive into each step and see how we can improve OPSEC as part of our red team operations.

### Answer the questions below
- Aim to memorize the five steps of the OPSEC process as we explain each one in its own task.
  > `No answer needed`

---

## [Task 2  Critical Information Identification]()

- What a red teamer considers critical information worth protecting depends on the operation and the assets or tooling used. 
- In this setting, critical information includes, but is not limited to, the red team’s intentions, capabilities, activities, and limitations. 
- Critical information includes any information that, once obtained by the blue team, would hinder or degrade the red team’s mission.

![image](https://user-images.githubusercontent.com/51442719/180427966-8f38a378-4d4f-4358-9352-41e3dce6a0b7.png)

- To identify critical information, the red team needs to use an adversarial approach and ask themselves what information an adversary, the blue team, in this case, would want to know about the mission. 
- If obtained, the adversary will be in a solid position to thwart the red team’s attacks. 
- Therefore, critical information is not necessarily sensitive information; however, it is any information that might jeopardise your plans if leaked to an adversary. 
- The following are some examples:
  - Client information that your team has learned. 
    - It's unacceptable to share client specific information such as employee names, roles, and infrastructure that your team has discovered. 
    - Sharing this type of information should kept on need-to-know basis as it could compromise the integrity of the operation. 
    - The Principle of Least Privilege (PoLP) dictates that any entity (user or process) must be able to access only the information necessary to carry out its task. 
    - PoLP should be applied in every step taken by the Red Team.
  - Red team information, such as identities, activities, plans, capabilities and limitations. 
    - The adversary can use such information to be better prepared to face your attacks.
  - Tactics, Techniques, and Procedures (TTP) that your team uses in order to emulate an attack.
  - OS, cloud hosting provider, or C2 framework utilised by your team. 
    - Let’s say that your team uses [`Pentoo`](https://pentoo.github.io/) for penetration testing, and the defender knows this. 
    - Consequently, they can keep an eye for logs exposing the OS as Pentoo. 
    - Depending on the target, there is a possibility that other attackers are also using Pentoo to launch their attacks; however, there is no reason to expose your OS if you don’t have to.
  - Public IP addresses that your red team will use. 
    - If the blue team gains access to this kind of information, they could quickly mitigate the attack by blocking all inbound and outbound traffic to your IP addresses, leaving you to figure out what has happened.
  - Domain names that your team has registered. 
    - Domain names play a significant role in attacks such as phishing. Likewise, if the blue team figures out the domain names you will be using to launch your attacks, they could simply block or sinkhole your malicious domains to neutralize your attack.
  - Hosted websites, such as phishing websites, for adversary emulation.

### Answer the questions below
- Click on View Site and follow through till you get the flag.
- (Please note that some browser extensions, such as NoScript, might prevent the site from loading correctly.)
  > Answer format: [`***{*******************}`](#THM{OPSEC_CRITICAL_INFO})


---

## [Task 3  Threat Analysis]()
- After we identify critical information, we need to analyse threats. 
- Threat analysis refers to identifying potential adversaries and their intentions and capabilities. 
- Adapted from the US Department of Defense [`(DoD) Operations Security (OPSEC) Program Manual`](https://www.esd.whs.mil/Portals/54/Documents/DD/issuances/dodm/520502m.pdf), threat analysis aims to answer the following questions:
  - Who is the adversary is?
  - What are the adversary’s goals?
  - What tactics, techniques, and procedures does the adversary use?
  - What critical information has the adversary obtained, if any?
  > ![image](https://user-images.githubusercontent.com/51442719/180429730-fb208a7d-20d6-4a79-a123-de7531c8478b.png)

- The task of the red team is to emulate an actual attack so that the blue team discovers its shortcomings, if any, and becomes better prepared to face incoming threats. 
- The blue team’s main objective is to ensure the security of the organization’s network and systems. 
- The intentions of the blue team are clear; they want to keep the red team out of their network. 
- Consequently, considering the task of the red team, the blue team is considered our adversary as each team has conflicting objectives. 
- We should note that the blue team’s capabilities might not always be known at the beginning.

- Malicious third-party players might have different intentions and capabilities and might pause a threat as a result. 
- This party can be someone with humble capabilities scanning the systems randomly looking for low-hanging fruit, such as an unpatched exploitable server, or it can be a capable adversary targeting your company or your client systems. 
- Consequently, the intentions and the capabilities of this third party can make them an adversary as well.
- We consider any adversary with the intent and capability to take actions that would prevent us from completing our operation as a threat:
> `Adversary` + `Intent` + `Capability` = `Threat` 
- In other words, an adversary without the intent or capability does not pose a threat for our purposes.

### Answer the questions below
- Try to think of at least one adversary who is not a threat and one who is a threat.
  > `No answer needed`

---

## [Task 4  Vulnerability Analysis]()

- After identifying critical information and analysing threats, we can start with the third step: analysing vulnerabilities. 
- This is not to be confused with vulnerabilities related to cybersecurity. 
> An OPSEC vulnerability exists when an adversary can obtain critical information, analyse the findings, and act in a way that would affect your plans.
- To better understand an OPSEC vulnerability as related to red teaming, we'll consider the following scenario. 
  - You use Nmap to discover live hosts on a target subnet and find open ports on live hosts. 
  - Moreover, you send various phishing emails leading the victim to a phishing webpage you're hosting. 
  - Furthermore, you're using the Metasploit framework to attempt to exploit certain software vulnerabilities. 
  - These are three separate activities; however, if you use the same IP address(es) to carry out these different activities, this would lead to an OPSEC vulnerability. 
  - Once any hostile/malicious activity is detected, the blue team is expected to take action, such as blocking the source IP address(es) temporarily or permanently. 
  - Consequently, it would take one source IP address to be blocked for all the other activities use this IP address to fail. 
  - In other words, this would block access to the destination IP address used for the phising server, and the source IP address using by Nmap and Metasploit Framework.
- Another example of an OPSEC vulnerability would be an unsecured database that's used to store data received from phishing victims. 
- If the database is not properly secured, it may lead to a malicious third party compromising the operation and could result in data being exfiltrated and used in an attack against your client's network. 
- As a result, instead of helping your client secure their network, you would end up helping expose login names and passwords.
- Lax OPSEC could also result in less sophisticated vulnerabilities. 
  - For instance, consider a case where one of your red team members posts on social media revealing your client's name. 
  - If the blue team monitors such information, it will trigger them to learn more about your team and your approaches to better prepare against expected penetration attempts.

### Answer the questions below
- Your red team uses THC-Hydra to find the password for a specific login page. Moreover, they are using the Metasploit framework on the same system as THC-Hydra. Would you consider this an OPSEC vulnerability? (Y/N)
  > [`x`](#Y)

- One of the red team members posts a photo of his cat every day. Would this be considered an OPSEC vulnerability? (Y/N)
  > [`x`](#N)

- Your red team went for dinner, took a photo, and tagged every team member on a popular social media platform. Would you consider this an OPSEC vulnerability? (Y/N)
  > [`x`](#Y)

- Your red team posts on its website a list of clients you regularly conduct red team exercises with. Would you consider this an OPSEC vulnerability? (Y/N)
  > [`x`](#Y)

- One of your red team members posted a photo of her morning coffee. Would you consider this an OPSEC vulnerability? (Y/N)
  > [`x`](#N)

---

## [Task 5  Risk Assessment]()

- We finished analysing the vulnerabilities, and now we can proceed to the fourth step: conducting a risk assessment. 
- [`NIST`](https://csrc.nist.gov/glossary/term/risk_assessment) defines a risk assessment as 
  - "The process of identifying risks to organizational operations (including mission, functions, image, reputation), organizational assets, individuals, other organizations, and the Nation, resulting from the operation of an information system." 
- In OPSEC, risk assessment requires learning the possibility of an event taking place along with the expected cost of that event. 
- Consequently, this involves assessing the adversary’s ability to exploit the vulnerabilities.
- Once the level of risk is determined, countermeasures can be considered to mitigate that risk. 
- We need to consider the following three factors:
  - The efficiency of the countermeasure in reducing the risk
  - The cost of the countermeasure compared to the impact of the vulnerability being exploited.
  - The possibility that the countermeasure can reveal information to the adversary
- Let’s revisit the two examples from the previous task. 
- In the first example, we considered the vulnerability of scanning the network with Nmap, using the Metasploit framework, and hosting the phishing pages using the same public IP address. 
- We analysed that this is a vulnerability as it makes it easier for the adversary to block our three activities by simply detecting one activity. 
- Now let’s assess this risk. 
- To evaluate the risk related to this vulnerability, we need to learn the possibility of one or more of these activities being detected. 
- We cannot answer this without obtaining some information about the adversary’s capabilities. 
- Let’s consider the case where the client has a Security Information and Event Management (SIEM) in place. 
  - A SIEM is a system that allows real-time monitoring and analysis of events related to security from different sources across the network. 
  - We can expect that a SIEM would make it reasonably uncomplicated to detect suspicious activity and connect the three events. 
  - As a result, we would assess the related risk as high. 
  - On the other hand, if we know that the adversary has minimal resources for detecting security events, we can assess the risk related to this vulnerability as low.
- Let’s consider the second example of an unsecured database used to store data received from a phishing page. 
- Based on data collected from several research groups using honeypots, we can expect various malicious bots to actively target random IP addresses on the Internet. 
- Therefore, it is only a matter of time before a system with weak security is discovered and exploited.

### Answer the questions below
- Your red team uses THC-Hydra to find the password for a specific login page. 
- Moreover, they are using the Metasploit framework on the same system as THC-Hydra. 
- Knowing that your target uses a properly configured Intrusion Detection System (IDS), would you consider this vulnerability as high risk? (Y/N)
  > [`X`](#Y)


---

## [Task 6  Countermeasures]()

---

## [Task 7  More Practical Examples]()

---

## [Task 8  Summary]()

---
