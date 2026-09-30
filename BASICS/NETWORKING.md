---
banner: "Assets/Banners/dragonglow.jpg"
banner_y: 0.80875
banner_x: 0.45397
banner_icon: 💠
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
# Introduction to Networking
https://academy.hackthebox.com/app/module/34


### Networking Overview
Network Enables 2 computers to communicate with each other there are various ways to connect like ethernet / fiber / wireless  etc there are protocols like TCP/UDP/IPX that can be used to facilitate the network 
##### URL >> Uniform Resource Locator
Url only give the address of the building 
##### FQDN >> Fully Qualified Domain Name 
fqdn gives the everything the building address , floor , room no etc .

### Network Types
Each network is structured differently and can be set up individually. For this reason, so-called `types` and `topologies` have been developed that can be used to categorize these networks.
##### WAN >> Wide Area Network 
This is also known as THE INTERNET . Wan Is basicly just a large number of LAN connected together . Corporations also have their own Private WAN
##### LAN >> Local Area Network 
LAN or WLAN will typically assign ip add for local use . There is no difference between LAN and WLAN they both are basicly same just one work with wireless and other with Wire .
##### WLAN >> Wireless Local Area Network
##### VPN >> Virtual Private Network 
There are 3 Types of Vpn 
Vpn is basicly using the internet but from somewhere else
###### 1. Site to Site VPN
This is basicly when we connect 2 far seperate companies want to join their network over the internet they use Site to Site Vpn so all the network for both companies feels that they are on same local network . Basicly Secure tunneling but for the whole network 
###### 2.Remote Access VPN









