---
banner: "Assets/Banners/flowergirl.png"
banner_y: 0.5185
banner_x: 0.37512
banner_icon: 🌸
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

https://portswigger.net/web-security/learning-paths/path-traversal/reading-arbitrary-files-via-path-traversal/file-path-traversal/reading-arbitrary-files-via-path-traversal
### What is Path Traversal ? 
--> Path Traversal is also known as directory traversal means going to differnet folders or directories in an server by doing that we are able to read the data or see the data that wasnt intended for normal client to see we try to guess or run a automated scanner for path traversal that scans all the available path or we can do manually the data reaveled can be application code , client data etc 

In Some cases some attackers are able to overwrite or add data into existing file to change the functions or behaviour of the applications and by that take full control over the application

### Reading arbitrary files via path traversal

Suppose your website is showing an image using this html code 
`<img src="/loadImage?filename=218.png">`
and to load the image in the url it shows `/var/www/images/218.png`
so this tells us that which directory is the web using to display the image and that might also be an root directory so to exploit this we will use `https://insecure-website.com/loadImage?filename=../../../etc/passwd` this is basicly we use to get 3 steps up in the directory and then if its a root access then we are able to read the password from /etc/passwd the sequence ../ means getting a step up in the directory . On windows based server both `../` and `..\` are both directory traversal sequence so we can use this in case of it "`insecure-website.com/loadImage?filename=..\..\..\windows\win.ini"

### Common obstacles to exploiting path traversal vulnerabilities
To prevent the file traversal many applications write an code that cheaks that if the file travel is allowed or not so they write that not to allow the things so even if u try it will get blocked so to bypass that we might sometimes use encoding to do that like convert the file path int something else means encode the path like this This results in `%2e%2e%2f` and `%252e%252e%252f` respectively. Various non-standard encodings, such as `..%c0%af` or `..%ef%bc%8f`, may also work. and then do same thing or just do nested loops like `....//` or `....\/`  or directly tying to get the root folder like filename=/etc/passwd 

An application may require the user-supplied filename to start with the expected base folder, such as `/var/www/images`. In this case, it might be possible to include the required base folder followed by suitable traversal sequences. For example: `filename=/var/www/images/../../../etc/passwd`. not only that it also can be something like filename=../../../etc/passwd%00.png 
becuase the application may expect the filename so we used nullbyte as %00 before putting the filename becuase nullbyte terminates file path before the required extension

### How to prevent a path traversal attack
The most effective way to prevent path traversal vulnerabilities is to avoid passing user-supplied input to filesystem APIs altogether. Many application functions that do this can be rewritten to deliver the same behavior in a safer way.


There are 2 ways to protect or we can say we can use both the defense technique
1>We can whitelist the input values and block the values other than those or blacklist the values that are not intended and then block them when the input comes from the user 
2>We can cheak the filepath of the input before before returning any information the system will cheak if the filepath matches to the system 
eg> U have to reach building A u ask someone ask that where is building A and you say go straight take 3 u-turn and then enter the bank so its basicly  `A Building/../../../Bank Vault` . but if u see your home was just A Building so the system cheaks that is the bank vault path comes from A building if its No then server blocks the user and its request. 


