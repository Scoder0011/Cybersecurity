---
banner: "Assets/Banners/mount.jpg"
banner_y: 0.3465
banner_x: 0.45397
banner_icon: ⏱️
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

```dataviewjs
// Define your cybersecurity learning path stages
const roadmap = [
    { section: "Basics", items: [
        "General Sec Concepts",
        "Linux Fundamentals",
        "Networking Fundamentals",
        "Windows Fundamentals",
        "Scripting (Python & Bash)"
    ]},
    { section: "Pentesting", items: [
        "Web Security",
        "Network Security",
        "Active Directory",
        "API Pentesting",
        "Basic Cloud Sec (AWS)"
    ]}
];

// Container styling
const container = dv.el("div", "", { cls: "roadmap-container" });
container.style.cssText = "display: flex; flex-direction: column; gap: 20px; font-family: var(--font-interface); max-width: 600px; padding: 10px 0;";

roadmap.forEach(group => {
    // Section Header
    const groupTitle = dv.el("h3", group.section, { container: container });
    groupTitle.style.cssText = "margin: 0 0 10px 0; color: var(--text-accent); font-size: 1.1em; border-bottom: 1px solid var(--background-modifier-border); padding-bottom: 5px;";

    const listWrapper = dv.el("div", "", { container: container });
    listWrapper.style.cssText = "display: flex; flex-direction: column; gap: 10px;";

    group.items.forEach((item, idx) => {
        const btn = dv.el("button", item, { container: listWrapper });
        
        // Base button style
        btn.style.cssText = `
            display: flex;
            align-items: center;
            justify-content: flex-start;
            padding: 12px 18px;
            background: var(--background-secondary);
            color: var(--text-normal);
            border: 1px solid var(--background-modifier-border);
            border-radius: 8px;
            font-size: 0.95em;
            font-weight: 500;
            cursor: pointer;
            transition: all 0.2s ease;
            text-align: left;
            box-shadow: 0 2px 4px rgba(0,0,0,0.05);
        `;

        // Toggle click handler (strike-through and style change)
        let isCompleted = false;
        btn.onclick = () => {
            isCompleted = !isCompleted;
            if (isCompleted) {
                btn.style.textDecoration = "line-through";
                btn.style.opacity = "0.45";
                btn.style.background = "var(--background-primary)";
                btn.style.borderColor = "transparent";
            } else {
                btn.style.textDecoration = "none";
                btn.style.opacity = "1.0";
                btn.style.background = "var(--background-secondary)";
                btn.style.borderColor = "var(--background-modifier-border)";
            }
        };

        // Hover animation
        btn.onmouseenter = () => { if(!isCompleted) btn.style.borderColor = "var(--interactive-accent)"; };
        btn.onmouseleave = () => { if(!isCompleted) btn.style.borderColor = "var(--background-modifier-border)"; };
    });
});
```