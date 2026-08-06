---
banner: "Assets/Banners/astro.png"
banner_y: 0.2065
banner_x: 0.35074
banner_icon: 🦄
---

```dataviewjs
const container = dv.container;
container.style.cssText = `margin: 0 0 24px 0;`;

const style = document.createElement('style');
style.textContent = `
  @keyframes borderFlow {
    0%   { background-position: 0% 50%; }
    50%  { background-position: 100% 50%; }
    100% { background-position: 0% 50%; }
  }
  @keyframes glowPulse {
    0%, 100% { box-shadow: 0 0 8px #00f0ff44, 0 0 20px #00f0ff22; }
    50%       { box-shadow: 0 0 16px #00f0ff88, 0 0 40px #00f0ff44; }
  }
  @keyframes scanline {
    0%   { left: -100%; }
    100% { left: 200%; }
  }
  .home-btn-wrap {
    display: inline-block;
    padding: 2px;
    border-radius: 10px;
    background: linear-gradient(270deg, #00f0ff, #7928ca, #ff0080, #00f0ff);
    background-size: 400% 400%;
    animation: borderFlow 4s ease infinite, glowPulse 2.5s ease-in-out infinite;
    cursor: pointer;
  }
  .home-btn-inner {
    display: flex;
    align-items: center;
    gap: 10px;
    padding: 10px 22px;
    border-radius: 8px;
    background: rgba(0, 0, 0, 0.75);
    position: relative;
    overflow: hidden;
  }
  .home-btn-inner::after {
    content: '';
    position: absolute;
    top: 0; height: 100%;
    width: 40%;
    background: linear-gradient(to right, transparent, rgba(0,240,255,0.08), transparent);
    animation: scanline 3s ease-in-out infinite;
  }
  .home-btn-icon {
    font-size: 1.1em;
    line-height: 1;
  }
  .home-btn-label {
    font-family: 'Courier New', monospace;
    font-size: 0.88em;
    font-weight: 400;
    letter-spacing: 3px;
    text-transform: uppercase;
    color: #00f0ff;
    text-shadow: 0 0 8px #00f0ff88;
  }
  .home-btn-arrow {
    font-family: 'Courier New', monospace;
    font-size: 0.9em;
    color: #7928ca;
    text-shadow: 0 0 6px #7928caaa;
    transition: transform 0.2s ease;
  }
  .home-btn-wrap:hover .home-btn-arrow {
    transform: translateX(4px);
  }
  .home-btn-wrap:hover .home-btn-inner {
    background: rgba(0, 240, 255, 0.06);
  }
`;
document.head.appendChild(style);

const btnWrap = container.createEl('div');
btnWrap.className = 'home-btn-wrap';

btnWrap.onclick = () => {
    app.workspace.openLinkText('Homepage', '', false);
};

const btnInner = btnWrap.createEl('div');
btnInner.className = 'home-btn-inner';

const icon = btnInner.createEl('span');
icon.className = 'home-btn-icon';
icon.textContent = '⌂';

const label = btnInner.createEl('span');
label.className = 'home-btn-label';
label.textContent = 'Go to Homepage';

const arrow = btnInner.createEl('span');
arrow.className = 'home-btn-arrow';
arrow.textContent = '→';
```

# Introduction to Information Security

### Module >>> https://academy.hackthebox.com/app/module/293


##### Structure of InfoSec

InfoSec is all about guarding the crucial data from the people who shouldnt have access to the data this includes changing in the data or destorying or even viewing the data.

This is how the things work


![[Pasted image 20260804230223.png]]

There are different Teams 
Red Team >> Which behaves like an attacker to attack the company infra to find bugs or vulnarabilities
Blue Team >> Which protects the data from not leakning or strenghtening the infra so attackers cant get data 
Purple Team >> Mix of both red and blue team 

Pentesters(also a part of red teaming (offensive security))
>> These ppl find vulnarabilites in a system or weekness in a system and inform the developers to fix them before an unethical hacker can exploit them 

In the world of cybersecurity the most important assets is data of person its a treasure for an ethical or unethical hacker so we must protect it by differnte methods like
Firewalls 
Encryptions 
Security Protocols

##### Areas of Information Security
Infosec plays a role in protecting organizations data from various threats so that the CIA trait is maintained 
CIA >> Confidentiality (means that the data should be confedential)
    >> Intigrity (the data shouldnt be tempered by any cause)
    >> Availability (data should be available when needed by the authorized user)

There are alot of types of attack some of them which are common are 
DDoS, ransomware , apts , insider etc 

A risk in context of infosec refers to an potential for a malicious event to occour which could cause damage to an organizations assets , such as its data or infra.

There are some roles in infosec
>CISO (Cheif info sec officer) 
>Sec Architect
>Pentester
>Incident response specialist
>Sec Analyst
>Compliance specialist 


##### Principles of Information Security
>>CONFIDENTIALITY
 -> Ensures that information is confidential and accessable to those which are authorized for that information
>INTEGRITY
 -> Maintains that the information stored are accurate and it shouldnt be tempered
>AVAILABILITY
 -> Ensures that the information is accessiable to the authorized user and available when needed 
>NON-REPUDIATION
 -> Ensures that a party cant deny the authenticity of the signature on a doct that the sending of a message that they originated 
>AUTHENTICATION
 -> Verify the identity of the use process and the device used 
>PRIVACY
 -> Focuses on handing of the private and personal information carefully


##### Processes in Information Security
>>RISK-ASSESMENET
 -> Identifying the potential threats and vulnerabilities or determine potential breach 
>SECURITY PLANNING
 -> Develop an stategies to tackel the risks 
>IMPLEMENTATION OF SECURITY CONTROLS
 -> make security plans and actions to protect the infra
>MONITORING AND DETECTION
 -> Continously watches for security events and anomalies 
>INCIDENT RESPONSE
 -> React to detected security incidents to prevent further leaks
>DISASTER RECOVERY 
 -> Focuses on restoring systems and data after major incidents
>CONTINOUS IMPROVEMENTS 
 -> Learn from incidents and improve the infra so no similar attacks happen

##### Purpose of Information Security
`Protecting sensitive data from unauthorized access`
`Ensuring business continuity`
`Maintaining regulatory compliance`
`Preserving brand reputation`
`Safeguarding intellectual property`
`Enabling secure digital transformation`

##### Tools in Information Security
Firewalls
Intrusion Detection/Prevention Systems (IDS/IPS)
Security Information and Event Management (SIEM) systems
Vulnerability scanners
Penetration testing tools
Encryption tools
Access control systems
Security awareness training platforms

##### Network Security
Network security is like the security system of a house, but instead of protecting your home, it protects a computer network from threats.

##### Internet of Things Security
The `Internet of Things`, or `IoT`, refers to the network of everyday objects connected to the internet, allowing them to send and receive data. This includes everything from smart home devices to wearable fitness trackers, industrial sensors, and even connected cars

##### Distributed Denial of Service (D-DOS)
A `Distributed Denial of Service` (`DDoS`) attack is a malicious attempt to interrupt the normal functioning of a website, server, or online service by overwhelming it with a flood of internet traffic. Unlike a traditional `Denial of Service` (`DoS`) attack, which originates from a single source, a DDoS attack comes from multiple sources simultaneously. These sources are often compromised computers or devices infected with malware, collectively known as a "botnet.”

##### Ransomware
Ransomware is a type of malicious software (or malware) that infiltrates servers, computers, and networks, encrypting valuable files so they become inaccessible. The attackers then demand a ransom payment, often in cryptocurrency like Bitcoin, in exchange for a decryption key that promises to restore access to the locked data. It's similar to a digital hostage situation, where your important files are held captive.

##### Social Engineering
Social engineering is similar to the tactics of a con artist, relying on `psychological manipulation` to deceive individuals into revealing confidential information or taking actions that compromise security. Instead of using technical methods to breach systems, social engineers take advantage of human nature—our tendencies to trust and assist others.

In the realm of cybersecurity, social engineering is a significant threat because it targets the human element, often considered the weakest link in security defenses

1. Phishing
2. Pretexting
3. Baiting
4. Tailgating
5. Quid Pro Quo

##### Insider Threat
An `insider threat` refers to the danger that comes from individuals who have authorized access to an organization's resources, such as employees, contractors, or business partners.
1. Malicious Insiders
2. Negligent Insiders
3. Compromised Insiders


##### Advanced Persistent Threats
An `Advanced Persistent Threat` (`APT`) is a sophisticated and continuous cyberattack where an intruder gains unauthorized access to a company’s network and remains undetected for an extended period.


##### Threat Actors
A `Threat Actor` "team" is an organized group of individuals with specialized skills collaborating to carry out cyber attacks. Red Teams apply the same techniques but with the intention to secure the company instead of harming it.

##### Red Team
A Red Team is a specialized group of cybersecurity professionals who simulate real-world attacks on an organization's systems, networks, and even its people. Their goal is to test the organization's defenses comprehensively.

##### Blue Team
The Blue Team serves as the frontline defense in the cybersecurity, comprising a diverse group of specialists who collaborate to protect an organization's digital infrastructure.

|Security Analysts|Incident Responders|Threat Hunters|Security Engineers|
|---|---|---|---|

##### Purple Team
Imagine a medieval kingdom preparing its defenses against invaders. On one side, you have a group of knights (the Blue Team) who dedicate their time to guarding the castle walls and learning how to repel attacks. On the other side, there's a band of expert attackers within the kingdom's own military (the Red Team) who understand how invaders think and train the knights by launching simulated assaults
`Penetration Testers` / `Ethical Hackers` (`Red Team`)
`Incident Responders` and `Security Analysts` (`Blue Team`)

##### Chief Information Security Officer
Imagine you are responsible for protecting a vast, bustling city from various threats. This city is filled with citizens (employees), buildings (technologies), and valuable treasures (data). As its protector, you must anticipate attacks, ensure the city’s defenses are strong, and coordinate with other leaders to keep everything running smoothly. In the cybersecurity world, this role is akin to the `Chief Information Security Officer` (`CISO`).

##### Penetration Testers
A `Penetration Tester` (also known as `Ethical Hacker`) is a cybersecurity professional who acts like a malicious hacker to find vulnerabilities in an organization's computer systems, networks, or web applications `but` without the malicious intent

##### Security Operations Center
A `Security Operations Center` (`SOC`) is a centralized unit that acts as the core of an organization's cybersecurity operations. It’s a place where skilled professionals work continuously to monitor, detect, analyze, and respond to cyber threats and security incidents.

##### Bug Bounty Hunter
Bug bounty hunters are skilled cybersecurity professionals who operate independently to uncover vulnerabilities in various digital assets belonging to organizations. These assets may include software applications, websites, or complex network systems.

