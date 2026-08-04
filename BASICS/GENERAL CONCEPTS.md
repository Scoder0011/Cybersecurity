---
banner: "Assets/Banners/skull.png"
banner_y: 0.3785
banner_x: 0.3582
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
