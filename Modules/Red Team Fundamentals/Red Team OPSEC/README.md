## 🔶 `VIP` [Red Team OPSEC](https://tryhackme.com/jr/opsec)
> Learn how to apply Operations Security (OPSEC) process for Red Teams.
- [x] [Task 1  Introduction](#task-1--introduction)
- [x] [Task 2  Critical Information Identification](#task-2--critical-information-identification)
- [x] [Task 3  Threat Analysis](#task-3--threat-analysis)
- [ ] [Task 4  Vulnerability Analysis](#task-4--vulnerability-analysis)
- [ ] [Task 5  Risk Assessment](#task-5--risk-assessment)
- [ ] [Task 6  Countermeasures](#task-6--countermeasures)
- [ ] [Task 7  More Practical Examples](#task-7--more-practical-examples)
- [ ] [Task 8  Summary](#task-8--summary)

---
- (`OPSEC`) - Operational Security 
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

---

## [Task 5  Risk Assessment]()

---

## [Task 6  Countermeasures]()

---

## [Task 7  More Practical Examples]()

---

## [Task 8  Summary]()

---
