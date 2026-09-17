---
banner: "Assets/Banners/katana.jpg"
banner_y: 0.10022
banner_x: 0.98374
banner_icon: 🦋
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

# OWASP Top 10:2025
OWASP TOP 10 is a document for devs and the web app sec . it tells about the most current top 10 crititcal bugs and risks about the web application in the current year. 

### The Ten Most Critical Web Application Security Risks

#### A01:2025 - Broken Access Control 
>> (https://top10.owasp.org/2025/A01_2025-Broken_Access_Control/)
#### A02:2025 - Security Misconfiguration
>> (https://top10.owasp.org/2025/A02_2025-Security_Misconfiguration/)
#### A03:2025 - Software Supply Chain Failures
>> (https://top10.owasp.org/2025/A03_2025-Software_Supply_Chain_Failures/)
#### A04:2025 - Cryptographic Failures
>> (https://top10.owasp.org/2025/A04_2025-Cryptographic_Failures/)
#### A05:2025 - Injection
>> (https://top10.owasp.org/2025/A05_2025-Injection/)
#### A06:2025 - Insecure Design
>> (https://top10.owasp.org/2025/A06_2025-Insecure_Design/)
#### A07:2025 - Authentication Failures
>> (https://top10.owasp.org/2025/A07_2025-Authentication_Failures/)
#### A08:2025 - Software or Data Integrity Failures
>> (https://top10.owasp.org/2025/A08_2025-Software_or_Data_Integrity_Failures/)
#### A09:2025 - Security Logging & Alerting Failures
>> (https://top10.owasp.org/2025/A09_2025-Security_Logging_and_Alerting_Failures/)
#### A10:2025 - Mishandling of Exceptional Conditions
>> (https://top10.owasp.org/2025/A10_2025-Mishandling_of_Exceptional_Conditions/)



## A01: Broken Access Control

>> Top 1 on the list this is the most serious serious application security risk.
>> On average of 3.73 application testing 40+ CWEs (Common Weekness enumeration ) are present.
>> SSRF is also been added to this category
>> The 100% of the application tested have been found the some kind of broken access control like 
>> CWE-200 (Exposure of sensitive information to Unauthorzied Person)
>> CWE-201 (Exposure of sensitive information through sent data)
>> CWE-918 (SSRF)
>> CWE-352(CSRF)


