---
banner: "Assets/Banners/shinobu.jpg"
banner_y: 0.18141
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

```dataviewjs
// Define your cybersecurity learning path stages
const roadmap = [
    { section: "🛡️ Basics", items: [
        "General Sec Concepts",
        "Linux Fundamentals",
        "Networking Fundamentals",
        "Windows Fundamentals",
        "Scripting (Python & Bash)"
    ]},
    { section: "🔍 Pentesting", items: [
        "Web Security",
        "Network Security",
        "Active Directory",
        "API Pentesting",
        "Basic Cloud Sec (AWS)"
    ]}
];

// Storage key for saving state
const STORAGE_KEY = "cybersecurity_roadmap_progress";

// Load saved state or create empty object
function loadProgress() {
    try {
        const saved = localStorage.getItem(STORAGE_KEY);
        return saved ? JSON.parse(saved) : {};
    } catch {
        return {};
    }
}

// Save state to localStorage
function saveProgress(progress) {
    localStorage.setItem(STORAGE_KEY, JSON.stringify(progress));
}

// Load existing progress
let progress = loadProgress();

// Container styling
const container = dv.el("div", "", { cls: "roadmap-container" });
container.style.cssText = `
    display: flex;
    flex-direction: column;
    gap: 24px;
    font-family: var(--font-interface);
    max-width: 650px;
    padding: 20px 0;
    margin: 0 auto;
`;

// --- Header Section ---
const headerWrapper = dv.el("div", "", { container: container });
headerWrapper.style.cssText = `
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 8px;
`;

const title = dv.el("h2", "🎯 Cybersecurity Learning Path", { container: headerWrapper });
title.style.cssText = `
    margin: 0;
    color: var(--text-accent);
    font-size: 1.5em;
    font-weight: 600;
    background: linear-gradient(135deg, var(--text-accent), var(--text-accent-hover));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
`;

// --- Progress Stats Card ---
const totalItems = roadmap.reduce((acc, group) => acc + group.items.length, 0);
const completedItems = Object.values(progress).filter(v => v === true).length;
const percentage = Math.round((completedItems/totalItems)*100);

const statsCard = dv.el("div", "", { container: container });
statsCard.style.cssText = `
    background: var(--background-primary);
    border: 1px solid var(--background-modifier-border);
    border-radius: 12px;
    padding: 16px 20px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    box-shadow: 0 2px 8px rgba(0,0,0,0.06);
`;

const statsText = dv.el("span", "", { container: statsCard });
statsText.style.cssText = `
    color: var(--text-muted);
    font-size: 0.95em;
`;
statsText.textContent = `📊 Progress: ${completedItems}/${totalItems} completed`;

const statsPercent = dv.el("span", "", { container: statsCard });
statsPercent.style.cssText = `
    font-weight: 600;
    font-size: 1.1em;
    color: ${percentage >= 80 ? 'var(--text-success)' : percentage >= 50 ? 'var(--text-accent)' : 'var(--text-muted)'};
`;
statsPercent.textContent = `${percentage}%`;

// --- Progress Bar ---
const progressBarContainer = dv.el("div", "", { container: container });
progressBarContainer.style.cssText = `
    width: 100%;
    height: 8px;
    background: var(--background-modifier-border);
    border-radius: 10px;
    overflow: hidden;
    margin-top: -12px;
    margin-bottom: 8px;
`;

const progressBar = dv.el("div", "", { container: progressBarContainer });
progressBar.style.cssText = `
    width: ${percentage}%;
    height: 100%;
    background: linear-gradient(90deg, var(--text-accent), var(--text-accent-hover));
    border-radius: 10px;
    transition: width 0.6s cubic-bezier(0.34, 1.56, 0.64, 1);
`;

// --- Reset Button ---
const resetBtn = dv.el("button", "⟳ Reset All", { container: headerWrapper });
resetBtn.style.cssText = `
    padding: 8px 18px;
    background: var(--background-secondary);
    color: var(--text-muted);
    border: 1px solid var(--background-modifier-border);
    border-radius: 8px;
    font-size: 0.85em;
    cursor: pointer;
    transition: all 0.25s ease;
    font-weight: 500;
    white-space: nowrap;
`;
resetBtn.onmouseenter = () => {
    resetBtn.style.background = "var(--background-modifier-error)";
    resetBtn.style.color = "var(--text-on-accent)";
    resetBtn.style.borderColor = "var(--background-modifier-error)";
};
resetBtn.onmouseleave = () => {
    resetBtn.style.background = "var(--background-secondary)";
    resetBtn.style.color = "var(--text-muted)";
    resetBtn.style.borderColor = "var(--background-modifier-border)";
};
resetBtn.onclick = () => {
    if (confirm("⚠️ Reset all progress?")) {
        progress = {};
        saveProgress(progress);
        location.reload();
    }
};

// --- Roadmap Sections ---
roadmap.forEach(group => {
    // Section Header
    const groupTitle = dv.el("h3", group.section, { container: container });
    groupTitle.style.cssText = `
        margin: 4px 0 12px 0;
        color: var(--text-accent);
        font-size: 1.05em;
        font-weight: 600;
        border-bottom: 2px solid var(--background-modifier-border);
        padding-bottom: 8px;
        letter-spacing: 0.3px;
    `;

    const listWrapper = dv.el("div", "", { container: container });
    listWrapper.style.cssText = `
        display: flex;
        flex-direction: column;
        gap: 10px;
        margin-bottom: 4px;
    `;

    group.items.forEach((item) => {
        // Create unique key for this item
        const itemKey = `${group.section}-${item}`;
        const isCompleted = progress[itemKey] || false;

        const btnWrapper = dv.el("div", "", { container: listWrapper });
        btnWrapper.style.cssText = `
            position: relative;
            transition: all 0.3s ease;
            transform: ${isCompleted ? 'scale(0.98)' : 'scale(1)'};
        `;

        const btn = dv.el("button", "", { container: btnWrapper });
        
        // Create content with icon
        const icon = isCompleted ? '✅' : '○';
        btn.innerHTML = `
            <span style="margin-right: 12px; font-size: 1.1em; opacity: ${isCompleted ? '1' : '0.5'}">${icon}</span>
            <span style="flex: 1;">${item}</span>
            ${isCompleted ? '<span style="font-size: 0.8em; opacity: 0.6;">✓ done</span>' : ''}
        `;
        
        // Base button style
        btn.style.cssText = `
            display: flex;
            align-items: center;
            justify-content: flex-start;
            padding: 14px 20px;
            width: 100%;
            background: ${isCompleted ? 'var(--background-primary)' : 'var(--background-secondary)'};
            color: var(--text-normal);
            border: 2px solid ${isCompleted ? 'var(--text-success)' : 'var(--background-modifier-border)'};
            border-radius: 12px;
            font-size: 0.95em;
            font-weight: ${isCompleted ? '400' : '500'};
            cursor: pointer;
            transition: all 0.3s cubic-bezier(0.34, 1.56, 0.64, 1);
            text-align: left;
            box-shadow: ${isCompleted ? '0 2px 8px rgba(0,0,0,0.04)' : '0 2px 4px rgba(0,0,0,0.04)'};
            opacity: ${isCompleted ? '0.85' : '1'};
            text-decoration: ${isCompleted ? 'line-through' : 'none'};
            font-family: var(--font-interface);
            position: relative;
            overflow: hidden;
        `;

        // Add subtle glow effect for completed items
        if (isCompleted) {
            btn.style.boxShadow = '0 0 0 1px var(--text-success), 0 2px 8px rgba(0,0,0,0.06)';
        }

        // Add hover effect background gradient
        const hoverBg = document.createElement('div');
        hoverBg.style.cssText = `
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: linear-gradient(135deg, var(--interactive-accent), var(--interactive-accent-hover));
            opacity: 0;
            transition: opacity 0.3s ease;
            pointer-events: none;
        `;
        btn.prepend(hoverBg);

        // Toggle click handler
        btn.onclick = () => {
            const newState = !progress[itemKey];
            progress[itemKey] = newState;
            saveProgress(progress);
            
            // Animate button press
            btn.style.transform = 'scale(0.95)';
            setTimeout(() => {
                btn.style.transform = 'scale(1)';
            }, 150);
            
            // Reload to update all stats
            setTimeout(() => {
                location.reload();
            }, 200);
        };

        // Hover effects
        btn.onmouseenter = () => {
            if (!isCompleted) {
                btn.style.borderColor = "var(--interactive-accent)";
                btn.style.transform = "translateY(-2px)";
                btn.style.boxShadow = "0 8px 16px rgba(0,0,0,0.08)";
                hoverBg.style.opacity = "0.05";
            } else {
                btn.style.transform = "translateY(-1px)";
                btn.style.boxShadow = "0 4px 12px rgba(0,0,0,0.06)";
            }
        };
        
        btn.onmouseleave = () => {
            if (!isCompleted) {
                btn.style.borderColor = "var(--background-modifier-border)";
                btn.style.transform = "translateY(0)";
                btn.style.boxShadow = "0 2px 4px rgba(0,0,0,0.04)";
                hoverBg.style.opacity = "0";
            } else {
                btn.style.transform = "translateY(0)";
                btn.style.boxShadow = "0 0 0 1px var(--text-success), 0 2px 8px rgba(0,0,0,0.06)";
            }
        };
    });
});

// --- Footer ---
const footer = dv.el("div", "", { container: container });
footer.style.cssText = `
    margin-top: 20px;
    padding-top: 16px;
    border-top: 1px solid var(--background-modifier-border);
    display: flex;
    justify-content: space-between;
    align-items: center;
    color: var(--text-faint);
    font-size: 0.8em;
`;

const footerLeft = dv.el("span", "💾 Progress saved locally", { container: footer });
const footerRight = dv.el("span", `Last updated: ${new Date().toLocaleTimeString()}`, { container: footer });
```