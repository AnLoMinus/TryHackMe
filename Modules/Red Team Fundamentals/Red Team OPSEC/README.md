## 🔶 `VIP` [Red Team OPSEC](https://tryhackme.com/jr/opsec)
> Learn how to apply Operations Security (OPSEC) process for Red Teams.
- [x] [Task 1  Introduction](#task-1--introduction)
- [ ] [Task 2  Critical Information Identification](task-2--critical-information-identification)
- [ ] [Task 3  Threat Analysis](#task-3--threat-analysis)
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

---

## [Task 3  Threat Analysis]()

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
