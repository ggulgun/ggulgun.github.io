---
title: "Manticore Adversarial Simulation Tool"
layout: post
---

# Introduction
2020-07-13 
<br />

Red Team activities are undoubtedly one of the fastest developing solutions against the cyber attacks of today. In this talk, we'll take a look at our work on an open-source proactive machine learning powered automation tool that performs red team simulations. This automation tool provides the opportunity to try out all available attack scenarios, thereby helping the community, especially organizations, to develop mechanisms to protect against these attacks before attackers do. Currently, red, blue and purple teams are improving day by day with the contributions made by open source. We will demonstrate the scenario playbook developed to collect the scenarios prepared for the red, blue and purple team on a single scenario place. The aim of this playbook is to protect the systems from such attack vectors, to examine the attack scenarios, to protect their systems by viewing the protection mechanisms and to contribute to these scenarios. With the built-in Scenario Place, people can either run these scenarios or check the scenario configurations on their systems. All scenario titles are prepared in accordance with MITRE and Cyber Kill Chain.
All scenarios from various teams such as Atomic Red Team, Mitre and TIBER-EU are fed into the application as input. The target distribution of those scenarios has been found out to be 60% Windows, 19% Linux and 21% MacOS, which is an uneven distribution. Balancing this distribution with the support of people in the open source community can be achieved with a project like this. Our side aim is to gather and develop the attack scenarios not only for the endpoints but also for the network.Protection mechanisms will be developed on the network side with the malicious traffic and applications enriching scenarios. When commercial red team applications are examined, it is seen that they cover at most 2000 scenarios. With this built-in component, relevant open source repositories and other red-team sources that can create scenarios will be scanned and analyzed to reach a much larger number of scenarios. These scenarios would then be available to be used for a threat hunting service. Thus, this project will both contribute to the public community and help people improve their security posture.
<br />

## Red Team Problems:

- To start with, Red teams are not loved as much as blue teams in general.
- After an adversarial emulation exercise by the red team, there is the issue of how mitigations are applied by the blue team.
- After the red team work, deficiencies may occur in the management of mitigation processes.
- When attacks are initiated by automated tools or command line interfaces, the contents of the attack is not transparent for all parties, especially for blue teams.
- We have seen examples of red teams failing on the initial compromise in corporate environments and that blocks the engagement from the start.
- Depending on the team, it might take too long to plan. It depends on the red team and whole activity can take upto 3months or more. 
- All attack interfaces can not be reviewed in manual red team work. 
 

## Adversarial emulation challenges

- Emulating adversarial behavior is costly because their techniques and tactics are complex. And red teamers cannot find the tools that are created by the malicious actors easily. That's why, adversary emulation cost is expensive. 
- Blue teams can not easily spot adversarial emulation behaviour due to black-box nature of red team's attack. This causes a problem in terms of improving their incident response capabilities efficiently.
- For emulating adversarial, tool availability is also a problem.  Red teamers can not easily find tools used by malicious groups, but bringing all publically available scenarios together, we think it will be the best option for red teams.
- Repeatability is another issue in adversary emulation. Sometimes during red team engagement, a test may fail but since the device rules may be changed, it can pass on another try the next time. Therefore, adversary emulation must be continuous engagements and repeatable.
- In adversary emulation exercises, malicious softwares used by malicious groups can cause unexpected situations on corporate devices and networks.


## Simulation tool problems

- What we are trying to achieve here is to create a purple team platform, not just directed to red teams. 
- Simulation Tools does not provide transparency in some of their scenarios. That is what we want to avoid with this tool.
- With on-prem installations of simulation tools, updated attacks can not easily be imported into platforms.  
- Investigating different commercial or open source tools, you can get the general idea of how much scenario is available for security teams. There are about 2000 scenarios in the wild and all of them cannot be reached from a single place.
- Simulation tools are leaving the Blue Team in the background for prevention and detection mechanisms.
- Simulation tools also do not take advantage of the open source community.
- Simulation tools are too complex for creating, updating scenarios. They don't have general structure (a standard model) for scenarios.
- Reporting is the biggest problem for simulation tools. They don't provide enough information for understanding the attack surface and attack vectors. 

## How ideal simulation tool works

- Attack simulation provides a way to test the network’s ability to recover from advanced attacks. In a simulated attack environment, all tests are automatically run by the system.
- Real attacks usually are not time-bounded. Adversary Simulation exercises are time-bound due to resources. 
- Real attacks not bounded by Law or ethics. Adversary simulation exercises are bounded by law and ethics.
- Uncontrolled by the target organisation, simulations are Controlled by the target organisation, risk controls can be applied.
Considering all these facts, our expectations is based on three main goals: 
- Make Emulations Real is the first fact: Use the same techniques, tools, methods and motivations of an attacker 
- End-to-End: Adversary activities are performed using TTPs (Tactics, Techniques & Procedures). Main goal of the activities are completing the entire cycle 
- Repeatable: All of the performed scenarios will be repeatable for threat detection and prevention
This tool starts with a “planning phase” where the scope of the assessment is defined and described, scenario engine is created. 
-  The second phase, “attack scenario generation", involves the creation of scenarios based on the defined critical functions and threat model. 
-  The third phase, “attack scenario execution”, is execution of scenarios on the endpoint and network devices. 
-  The final phase, “report and learning" , is for reporting, cleaning-up, transferring knowledge, remediating and communicating outcomes at the conclusion of the exercise.

## Why do wee need Manticore Platform 

- We wanted to prepare a scenario environment to make it faster and less complicated for red teamers to apply the tests in various open sources like Atomic Red Team or Red Canary.
- Overall, with this tool, red teamers will be able to access the scenarios according to specific attack types as divided in MITRE's categories 
- and blue teamers will be able to see these attacks within a transparent process. i.e. they will be informed about the mitigations directly within the platform.
- And with addition of APT traffics to the scenario environment, blue teams' detection capability will also be tested in different network layers.
- Checking different commercial and open source tools, the target distribution of those scenarios has been found out to be 60% Windows, 20% for both MacOS and Linux operating systems. 
-This shows a tendency towards Windows environments due to understandable reasons. 
- However, we think that increasing scenarios on the Mac and Linux side and balancing this distribution with the support of the open source community is possible with a project like this.
- Our aim is to recreate APT scenarios and make it transparent for both red and blue teams during the engagement.
- That way, red team exercise is not going to be only something run from their command line interface but each team would have the chance to visualize and simulate the malicious traffic generated by attackers/threat groups.

## Manticore Platform

We released Manticore Platform tool on the our github repository.

Manticore Adversary Emulation Client Tool - https://github.com/Manticore-Platform/manticore-cli

Manticore Public Scenarios Repository - https://github.com/Manticore-Platform/public-scenarios

Manticore Public Threats Repository - https://github.com/Manticore-Platform/public-threats

Manticore Sample Ransomware Emulation Repository - https://github.com/Manticore-Platform/ransomware-emulation


