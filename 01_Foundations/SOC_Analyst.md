# SOC Analyst

SOC (Security Operations Center) adalah bidang atau jabatan dari cybersecurity. yang mana tugas utamanya adalah memantau dan mengamati seluruh lalu lintas jaringan, terutama jaringan yang mencurigakan yang masuk pada
area coverage jaringan yang dilindunginya.

A SOC (Security Operations Center) is a dedicated facility operated by a specialized security team. This team aims to continuously monitor an organization’s network and resources and identify suspicious activity to prevent damage.
This team works 24 hours a day, seven days a week.

The main focus of the SOC team is to keep Detection and Response intact. The SOC team has some resources available in the form of security solutions that help them achieve this.
These solutions integrate the whole company’s network and all the systems to monitor them from one centralized location. Continuous monitoring is required to detect and respond to any security incident.

## Detection
* Detect vulnerabilities: A vulnerability is a weakness that an attacker can exploit to carry out things beyond their permission level. A vulnerability might be discovered in any device’s software (operating system and programs), such as a server or computer.
For instance, the SOC might discover a set of MS Windows computers that must be patched against a specific published vulnerability. Strictly speaking,
vulnerabilities are not necessarily the SOC’s responsibility; however, unfixed vulnerabilities affect the security level of the entire company.
* Detect unauthorized activity: Consider the case where an attacker discovered the username and password of one of the employees and used them to log in to the company system.
It is crucial to detect this kind of unauthorized activity quickly before it causes any damage. Many clues, such as geographic location, can help us detect this.
* Detect policy violations: A security policy is a set of rules and procedures created to help protect a company against security threats and ensure compliance.
What is considered a violation would vary from company to company; examples include downloading pirated media files and sending confidential company files insecurely.
* Detect intrusions: Intrusions refer to unauthorized access to systems and networks. One scenario would be an attacker successfully exploiting our web application.
Another would be a user visiting a malicious site and getting their computer infected.

## Response
Support with the incident response: Once an incident is detected, certain steps are taken to respond to it. This response includes minimizing its impact and performing the root cause analysis of the incident.
The SOC team also helps the incident response team carry out these steps.

There are three pillars of a SOC. With all these pillars, a SOC team becomes mature and efficiently detects and responds to different incidents. **These pillars are People, Process, and Technology.**

People, Process, and Technology coexist in a SOC environment. A team of professional individuals working on state-of-the-art security tools in the presence of proper processes is what makes a mature SOC environment.

In the upcoming tasks, we will discuss each of these pillars individually and examine how they are important parts of SOC.
---

# Process

We discussed the roles and responsibilities of different individuals working in the SOC team. Each role has its own Processes, just as we saw the role of Level 1 SOC Analysts as the first responders to carry out alert triage and determine if it is harmful. Let’s discuss some important processes involved in a SOC.

## Alert Triage
The alert triage is the basis of the SOC team. The first response to any alert is to perform the triage. The triage is focused on analyzing the specific alert. This determines the severity of the alert and helps us prioritize it. The alert triage is all about answering the 5 Ws. What are these 5 Ws?

Following are some questions that need to be answered during the triage of an alert. 

Alert: Malware detected on Host: GEORGE PC

| 5 Ws |	Answers |
| --- | --- |
| What?	| A malicious file was detected on one of the hosts inside the organization’s network. |
| When?	| The file was detected at 13:20 on June 5, 2024. |
| Where?	| The file was detected in the directory of the host: "GEORGE PC". |
| Who?	| The file was detected for the user George. |
| Why?	|After the investigation, it was found that the file was downloaded from a pirated software-selling website. The investigation with the user revealed that they downloaded the file as they wanted to use a software for free. |

## Reporting
The detected harmful alerts need to be escalated to higher-level analysts for a timely response and resolution. These alerts are escalated as tickets and assigned to the relevant people. The report should discuss all the 5 Ws along with a thorough analysis, and screenshots should be used as evidence of the activity.

## Incident Response and Forensics
Sometimes, the reported detections point to highly malicious activities that are critical. In these scenarios, high-level teams initiate an incident response. The incident response process is discussed in detail in the Incident Response room. A few times, a detailed forensics activity also needs to be performed. This forensic activity aims to determine the incident’s root cause by analyzing the artifacts from a system or network.

