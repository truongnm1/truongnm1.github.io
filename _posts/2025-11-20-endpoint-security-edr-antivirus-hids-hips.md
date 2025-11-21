---
title: "Endpoint Security: EDR & AV & HIDS/HIPS"
date: 2025-11-20 12:32:15 +0800
categories: [blog]
tags: [edr,antivirus,hids,hips,endpoint]     # TAG names should always be lowercase
---


## Introduction

In security world that consists of different layers of protection, we, or at least me, might be overwhelming about how many solutions out there that we can put in our system to enhance security. It can take tremendous time to evaluate and decide the appropriate solutions based on where they should be at, ranging from different networks to endpoints. In this blog, I will introduce three solutions, which are Endpoint Detection and Response (EDR), Antivirus (AV) and Host-based IDS/IPS and clarify the difference between them.

## Antivirus (AV)

I think this is one of the first concepts in securing endpoints. As the name suggests, it hates viruses, but who doesn’t! An antivirus is software installed on the endpoint, and here’s what a typical one does:

- Works with files: Most antiviruses operate at the file-system level, performing actions such as reading, scanning, and deleting files.
- Generates warnings: If any file is flagged as malicious, the AV will alert the user.
- Takes actions: The user can choose what to do with a detected threat. Depending on the antivirus, you can delete, quarantine, or allow the file.
- Offers custom scans: Antivirus products let you scan specific folders, entire drives, or the whole endpoint. They also support scheduled and periodic scans.

These tasks rely on a database of known malware signatures. This database contains a vast number of virus patterns that help the antivirus recognize threats on your system. However, if a new type of malware appears and its signature hasn’t been added to the database yet, the antivirus may fail to detect it. This mechanism of the AV is called signature-based detection. Attackers started creating new variants faster than signature databases could update, AV needed to evolve, and that’s where EDR come in.

Some antivirus solutions there are: the famous Windows Defender, ClamAV

## Endpoint Detection and Response (EDR)

Let's move onto another solution, EDR sounds kind of general, though, but it provides a powerful security to the endpoint. The EDR is more in-depth into your system rather than just works at file-system level like the AV. Some features can be listed:

- Constantly monitor: EDR acts as a watcher, once installed, it monitors everything happens in an endpoint and records it in real time. 
- In-depth level: The EDR captures way more detailed events than traditional AV—things like processes, registry changes, user actions, network connections, and even in-memory activity. Both EDR and AV can use signatures, but EDR goes deeper by monitoring actual system behaviors to catch threats that signatures might miss.
- Take actions: When a threat is detected, EDR doesn't just alert you, it can respond automatically or let analysts take remote actions. This includes isolating the infected endpoint from the network to contain the threat, killing suspicious processes, deleting or quarantining malicious files, and even rolling back changes made by malware.
- Centralized management: EDR works by distributing agents to all of the endpoints. These agents will start their job by collecting telemetry and send it to a master console. The console provides a clean dashboard and comprehensive insights for the admin to easily keep track and make sure every endpoints are in control. 
- Match with standardized TTPs: It matches actions and malicious behaviours with a standardized cybersecurity framework like MITRE ATT&CK that helps analysts to recognize and correlate events, also for standardized reporting.
- Machine learning integrated: Artificial Intelligence emerges and helps EDR so much in detecting anomaly of malicious behaviours.

Quite a impressive pack of features, isn't it? EDR does more than antivirus. The target audience of EDR is enterprise and in large companies where there are hundred of endpoints that need to be secured, hence most of EDR solutions are paid plans. For a home PC, it would be an overkill if you implement an EDR solution for a home PC, and this is when antivirus sounds better. 

Some enterprises EDR solutions like: [CrowdStrike Falcon](https://www.crowdstrike.com/wp-content/uploads/2022/03/crowdstrike-falcon-insight-data-sheet.pdf), [Microsoft Defender for Endpoint](https://learn.microsoft.com/en-us/defender-endpoint/microsoft-defender-endpoint), [SentinelOne ActiveEDR](https://sentinelone.com/resources/datasheets/assets/usecase/sentinel-one-active-#page=1), [Wazuh](https://wazuh.com/platform/xdr/) (open source - for non-enterprise EDR experience)



# Host-based IDS & IPS

Another fighter that roams the endpoint battlefield. In this solution, we call it a host instead of an endpoint. HIDS (Host-based Intrusion Detection System) monitors a single machine for suspicious activity and alerts when something sketchy is detected. HIPS (Host-based Intrusion Prevention System) goes a step further—it actively blocks threats in real time. Think of HIDS as the alarm system that warns you, and HIPS as the bouncer that kicks threats out before they cause damage.

- Rule-based detection: HIDS/HIPS rely heavily on rules defined by administrators or security teams. You write rules to detect specific behaviors like "alert if someone accesses this sensitive file" or "block any process trying to modify the registry in this way."
- Monitors host activity: They watch for suspicious behavior like unauthorized file changes, unusual processes, privilege escalation attempts, or policy violations based on your rules.
- Detection vs Prevention: HIDS alerts you when it detects rule violations, while HIPS actively blocks the action before it executes.
- Customizable policies: Unlike AV or EDR which come with built-in detections, HIDS/HIPS require more manual configuration. You define what's normal and what triggers an alert or block.
- Log analysis: HIDS often analyzes system logs, file integrity, and configuration changes to spot rule violations or signs of compromise.

The main difference here is control, you're writing the rules and defining what counts as suspicious, rather than relying on vendor signatures or machine learning.

We also have several solutions for HIDS/HIPS: OSSEC, Wazuh, Tripwire

# Thoughts 

In my opinion, Endpoint Detection and Response (EDR) is the most comprehensive solution but of course it comes with a price. Antivirus is the simplest form of endpoint protection that focuses on eliminating virus using known signatures. Host-based IDS & IPS does not really focus on detecting virus but in a broader and more general events,it also relies on rules that are written by the user, the more proficient the rules, the more effective it works. 

I once thought that why don't we just combine these solutions into one thing. But I realized that each solution is for different target, ranging from home user to enterprises and also finance, plus it would use a lot computer resource if there are too many functions in one software that roams the endpoint. 

In conclusion, having a insightful understanding of different endpoint protection methods help us to be less time-consuming in planning stage of securing our beloved system. 










