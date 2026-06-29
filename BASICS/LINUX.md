---
banner: "Assets/Banners/dragon.jpg"
banner_y: 0.2125
banner_x: 0.45397
banner_icon: 🐉
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


# Basic To Elite

Resources >> 
https://overthewire.org/wargames/ {ALL GAMES}
https://linuxbasecamp.com/cheat-sheets/linux {Linux Cheat Sheet}
https://www.youtube.com/watch?v=T0Db6dVYyoA&list=PLBf0hzazHTGMh2fe2MFf3lCgk0rKmS2by {Linux Essentials For Hackers}



##### Bandit Level 0 → Level 1
To Solve this challange we need to connect to a ssh server of bandit 
using the command ssh bandit@bandit.labs.overthewire.org -p 2220 
where bandit is username and the -p is used for port number 
and after connection the password is bandit0 
to solve this challange we need to find a readme file and we will use commands like (ls >> which shows the files present in current directory and) (cat readme >> for reading the content of the readme file) which give me the password of this level >> 6y2kwnwK6grgvwvpvLaa2T1cpFEKOhNR

##### Bandit Level 1 → Level 2
To Solve this level you need to connect to again to ssh but with username bandit1 and with the password from previous level and the password was in home direcotory in a file named (-)  but (-) is used in linux for a command so if we normally do cat - then it will show error so we have to tell that its not a command its a file name called(-) and to read the file we will use cat "./-" then it gives the password >> PK8fYLZg2hnHSz83plBL1iEPKdD3QToB

##### Bandit Level 2 → Level 3
To Solve this challange again we need to connect with ssh with username bandit2 and the password was in the homedirectory file named --spaces in this filename-- again we cant use the cat and then filename to show the content so we again use the same method so the spaces also count as the part of the filename so we used cat ",/--spaces in this filename--" and this gives us the password >> 7ZZ2LFrykP2zEyvBl4m3clcL7tGYJPME

##### Bandit Level 3 → Level 4
To Solve this level we just need to find an hidden directory called inhere and then find the hidden file inside it we used command ls -la becuase using only ls shows the files and directories which are not hidden but using ls -ls shows all the files or directories which are hidden too so using it and using cat command we found the password >>
xzTXq1rDJQVVAzdv5cHq1TQytTWufAMq

##### Bandit Level 4 → Level 5
To solve this level we need to find a hidden file in the inhere directory which should be human redable we can use ls -lah command but it doenst show anything so we used file ./-* command the file command cheaks everyfile that starts with - and ends with anything then it showd a file which says ASCII text and when opening the file with cat command as cat ./file07 it shows the password >> 6C7h9GD8M6ai5nr7wo1RonrzFjj9yIrG

##### Bandit Level 5 → Level 6
To Solve this challange we need to find a file which is hidden and in human-redable and in 1033bytes exactly and which is non executable 
to find the file we will use the same method as earlier and use find command that goes through everyfile in the directory and then we use 
(find . -type f -size 1033c ! -executable) so this command cheaks everyfile and see if its type is -f (file) and its size is 1033c(bytes) and its ! -executable (its executed as a programme) it skips all the files and give us the file that matches all these character and then using cat command as cat ./.file2 we get the password >> pXa26xhMWaC2SvDotA4r9EgZkulOeSBW

##### Bandit Level 6 → Level 7
