---
banner: "Assets/Banners/frer.jpeg"
banner_y: 0.4285
banner_x: 0.45397
banner_icon: ☸️
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

Access to the Game https://overthewire.org/wargames/natas/
WebSec Learning https://portswigger.net/web-security


### Natas Level 0
For The level 0 we need to just go on the web link provided 
http://natas0.natas.labs.overthewire.org and just put the username and password as natas0 and natas0 to actually access next levels the password was found in the page source>> scfWG6qNEIdzqVyfRwEGXyNUfFZkZeQ7

### Natas Level 0 → Level 1
To solve this level just go to http://natas1.natas.labs.overthewire.org/
already given and use the username as natas1 and password found in the previous level to get the flag its same in the source code but unlinke last time we got by doing the right click its blocked so we will use f12 to open the source panel or can do ctrl + u to open all the source code and we get the password >> vsDOxoXyq3wckCP1ZmTZ71ngIA606odB

### Natas Level 1 → Level 2
To Solve this level same work flow as earlier login as username and password on this level on viewing the source code we see an directory of png linked as img src=files/pixel.png after visiting there was nothing but as it was linked with files directory we were able to visit it and find out the flag in users.txt as >> K30JrSRHzjxq3paUQuwozY4MNvmNFyhI

### Natas Level 2 → Level 3
To Solve this level we need to go on a directory called /robots.txt which actually helps other bot crawllers tell that what not to scan so they can scan actuall content of the webiste  (in real website) so we get a folder called /secret/ and going there we get the next password >> JDrPnuZAKyl6MkiqQGFIddrqpvgOASth

### Natas Level 3 → Level 4
To Solve this level we need to make a response header which will tell the browser we are coming from a certain path we can install any custom header changer i m using requestly as mod header was banned as an extension then add an rule to and reload the page and we get the password >> e4z2Noy3oqwPJUWzJH0dseN67Cn1sy2M

### Natas Level 4 → Level 5
To Solve this level we will put the id pass as usuall and as it said not logged in we cheak the cookie session in application tab and found out that it said logged true 0 then we changed that 0 to 1 and then reload the page and we get the password for next level >> 
7mhjtShJAcld2NYbKHEadnhEwRn2P8VT

### Natas Level 5 → Level 6
To Solve this level we need to cheak the source code and it says if we go th /include/secret.inc we will get the secret input and when entered in the box we will get the password >> B1szg95UcTnrzwnF3i3TzYHlyYh8iBV0

### Natas Level 6 → Level 7
The Hint is clearly given in the source code that the password is in the /etc/natas_webpass/natas8 but even without the hint as its using php
we can see its rendered as index.php?page=home so we can access other pages or directories by just changing the page=/etc/natas_webpass/natas8 and get the password >> ugXL95KQmUAJJj6bMezOlBNDyI9Imwkc

### Natas Level 7 → Level 8
To Solve this level we see in the source code there is an php code that says that the input we will give in the page should be equal to the given code in the source code after processing the processing is that the input first converts bintohex() but its not normal binary to hex but in php its a function so we will use an php converter hextobin() becuase there is one more function that just reverse the converted strings strrev() so instead of doing bintohex in php we will reverse it as hextobin as the given secret is in hex format after conversion we will get base64(== QcCtmMml1ViV3b) we will reverse this base64 into b3ViV1lmMmtCcQ==
then we will use from base64 converter to text we will get the final input to put in the page oubWYf2kBq (we just reversed the code in the php to get the input secret) after putting this as input we will receave the password for next level >> UdxmI27dTaXmnd1rxKQTfws6jihTdcQ9 

### Natas Level 8 → Level 9
To Solve this level we will see the source code in the source code we can see that a php code is given as whatever key we will enter it will process as an needle but there is also something called grep -i means whatever we are entering as a key in the input it is going in the server and doing grep -i ; key and returning whatever it found it so we just input ; cat /etc/natas_webpass/natas10 it will go in the server and do grep -i ; cat /etc/natas_webpass/natas10 it so it will not only give all the words but also the password as we used cat to print the password as most of the secret things ppl store for server side is in /etc/ folder so we get the password as >> EgjlkzB6E8LJyf2Obt4q7q4ewt5ZWSNv

### Natas Level 9 → Level 10



