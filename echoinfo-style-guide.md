# echoinfo.org — Complete Style Guide & Card Creation Manual
*Reference this document before building any new card. Last updated: May 2026.*

---

## 1. Repo Structure

```
akhilnarangmd.github.io/
├── index.html                    ← Homepage (card grid)
├── echoinfo-style-guide.md       ← This file
├── chamber-quantification/
│   └── index.html
├── ase-diastolic-2026-1/
│   └── index.html
├── right-heart-ph/
│   └── index.html
├── strain-guidelines/
│   └── index.html
├── prosthetic-valve-function/
│   └── index.html
├── hcm-guidelines/
│   └── index.html
├── mr-tr-calculator/
│   └── index.html
├── aortic-stenosis/
│   └── index.html
└── echo-swan/
    └── index.html
```

Each card is a **single self-contained `index.html`** file — all CSS and JS inline, no external dependencies except the system font stack.

**Current card order on homepage (maintain this order):**
1. Chamber Quantification
2. Right Heart & PH
3. Diastolic Function
4. Strain
5. Prosthetic Valve
6. Stress Echo
7. HCM

---

## 2. Starting a New Card — Checklist

Before writing any code:
- [ ] Identify the guideline source (journal, authors, DOI, year)
- [ ] Read the full guideline document — clinical accuracy is paramount
- [ ] Plan the tab structure (typically 5–8 tabs)
- [ ] Note any algorithms/flowcharts that need to be reproduced
- [ ] Check whether any other cards cover overlapping content → add cross-reference banners (see Section 14)
- [ ] Create folder `card-name/index.html` in the repo
- [ ] Add the card to root `index.html` homepage (see Section 11)
- [ ] Add card name to feedback modal dropdown in root `index.html`

---

## 3. Full HTML Shell — Copy This to Start Every Card

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Card Title · echoinfo.org</title>
<style>
  /* paste full CSS from Section 4 here */
</style>
</head>
<body>

<header>
  <div class="icon">🫀</div>
  <h1>Card Title</h1>
  <p class="subtitle">Guideline subtitle — Comprehensive Reference</p>
  <div class="guideline-badge">JASE 20XX · Author et al. · DOI 10.xxxx/xxxxx · Society Names</div>
</header>

<div class="nav-wrapper">
  <nav>
    <button class="nav-btn active" onclick="showTab('overview', event)">Overview</button>
    <button class="nav-btn" onclick="showTab('diagnosis', event)">Diagnosis</button>
    <!-- add more tabs as needed, max ~8 -->
  </nav>
</div>

<div class="content">

  <div class="panel active" id="panel-overview">
    <div class="section-intro">
      <h2>Section Heading</h2>
      <p>One or two sentence summary of what this tab covers.</p>
    </div>
    <!-- cards go here -->
  </div>

  <div class="panel" id="panel-diagnosis">
    <!-- content -->
  </div>

</div>

<footer>
  Card Name &nbsp;·&nbsp; <a href="https://echoinfo.org">echoinfo.org</a> &nbsp;·&nbsp; Created by Akhil Narang, MD
</footer>

<script>
function showTab(id, event) {
  document.querySelectorAll('.panel').forEach(p => p.classList.remove('active'));
  document.querySelectorAll('.nav-btn').forEach(b => b.classList.remove('active'));
  document.getElementById('panel-' + id).classList.add('active');
  event.currentTarget.classList.add('active');
  window.scrollTo({top: 0, behavior: 'smooth'});
}
function toggleAcc(header) {
  header.parentElement.classList.toggle('open');
}
</script>
</body>
</html>
```

**Note:** `showTab` now takes `event` as a second argument — this is required. Always write `onclick="showTab('overview', event)"`. The old single-argument form breaks active-state highlighting on nav buttons.

---

## 4. Complete CSS — Paste Into Every Card

```css
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

:root {
  --navy:      #1a365d;
  --blue:      #2b6cb0;
  --blue-lt:   #ebf8ff;
  --teal:      #276749;
  --teal-lt:   #f0fff4;
  --red:       #742a2a;
  --red-lt:    #fff5f5;
  --amber:     #744210;
  --amber-lt:  #fffaf0;
  --purple:    #44337a;
  --purple-lt: #faf5ff;
  --gray-50:   #f7fafc;
  --gray-100:  #edf2f7;
  --gray-200:  #e2e8f0;
  --gray-400:  #a0aec0;
  --gray-500:  #718096;
  --gray-700:  #2d3748;
  --gray-900:  #1a202c;
  --white:     #ffffff;
  --bg:        #f8f9fa;
  --radius:    10px;
}

body {
  font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
  background: var(--bg);
  color: var(--gray-900);
  min-height: 100vh;
  font-size: 15px;
  line-height: 1.6;
}

/* ── HEADER ── */
header {
  background: linear-gradient(135deg, #1a365d 0%, #2b6cb0 100%);
  color: white;
  padding: 28px 20px 24px;
  text-align: center;
}
header .icon { font-size: 2rem; display: block; margin-bottom: 8px; }
header h1 {
  font-size: clamp(1.35rem, 3vw, 1.65rem);
  font-weight: 700; letter-spacing: -0.01em; margin-bottom: 4px;
}
header .subtitle { font-size: 0.85rem; opacity: 0.82; margin-bottom: 12px; }
.guideline-badge {
  display: inline-block;
  background: rgba(255,255,255,0.15);
  border: 1px solid rgba(255,255,255,0.35);
  border-radius: 999px;
  padding: 4px 16px;
  font-size: 0.74rem; letter-spacing: 0.03em; color: white;
}

/* ── NAV ── */
.nav-wrapper {
  background: white;
  border-bottom: 2px solid var(--gray-200);
  position: sticky; top: 0; z-index: 100; overflow-x: auto;
}
nav {
  display: flex; justify-content: center; gap: 8px; flex-wrap: wrap;
  max-width: 1100px; margin: 0 auto; padding: 14px 20px;
}
.nav-btn {
  padding: 9px 18px;
  border: 2px solid var(--gray-200);
  background: white; border-radius: 8px;
  font-size: 0.82rem; font-weight: 700; color: var(--gray-500);
  cursor: pointer; white-space: nowrap; font-family: inherit;
  transition: all 0.15s;
}
.nav-btn:hover:not(.active) {
  border-color: var(--blue); color: var(--blue); background: var(--blue-lt);
}
.nav-btn.active {
  background: var(--navy); border-color: var(--navy); color: white;
  box-shadow: 0 2px 8px rgba(26,54,93,0.25);
}

/* ── LAYOUT ── */
.content { max-width: 1100px; margin: 0 auto; padding: 28px 20px 64px; }
.panel { display: none; }
.panel.active { display: block; }

/* ── SECTION INTRO ── */
.section-intro { margin-bottom: 20px; }
.section-intro h2 {
  font-size: 1.25rem; font-weight: 700; color: var(--gray-900); margin-bottom: 6px;
}
.section-intro p { font-size: 0.88rem; color: var(--gray-500); line-height: 1.65; }

/* ── CARDS ── */
.card {
  background: white; border-radius: var(--radius);
  padding: 20px 24px; margin-bottom: 14px; border: 1px solid var(--gray-200);
}
.card-title {
  font-size: 0.95rem; font-weight: 700; color: var(--gray-900);
  margin-bottom: 12px; display: flex; align-items: center; gap: 8px;
}

/* ── GRIDS ── */
.grid-2 { display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 16px; }
.grid-3 { display: grid; grid-template-columns: repeat(auto-fit, minmax(260px, 1fr)); gap: 16px; }

/* ── INFO ROWS ── */
.info-row {
  display: flex; gap: 10px; font-size: 0.82rem;
  padding: 8px 0; border-bottom: 1px solid var(--gray-100);
}
.info-row:last-child { border-bottom: none; }
.info-dot {
  width: 7px; height: 7px; border-radius: 50%;
  background: var(--navy); flex-shrink: 0; margin-top: 6px;
}
.info-dot.teal   { background: var(--teal); }
.info-dot.red    { background: #e53e3e; }
.info-dot.amber  { background: #d69e2e; }
.info-dot.purple { background: #6b46c1; }

/* ── THRESHOLD PILLS ── */
.thresh-row { display: flex; flex-wrap: wrap; gap: 8px; margin-top: 10px; }
.thresh {
  display: inline-flex; align-items: center; gap: 5px;
  padding: 5px 12px; border-radius: 6px; font-size: 0.78rem; font-weight: 600;
}
.thresh-normal { background: #f0fff4; color: #276749; border: 1px solid #9ae6b4; }
.thresh-warn   { background: #fffaf0; color: #744210; border: 1px solid #f6ad55; }
.thresh-danger { background: #fff5f5; color: #742a2a; border: 1px solid #fc8181; }
.thresh-info   { background: #ebf8ff; color: #2c5282; border: 1px solid #90cdf4; }
.thresh-purple { background: #faf5ff; color: #44337a; border: 1px solid #b794f4; }

/* ── ALERTS ── */
.alert {
  border-radius: 8px; padding: 12px 16px; font-size: 0.81rem;
  line-height: 1.55; display: flex; gap: 10px;
  align-items: flex-start; margin-top: 10px;
}
.alert-blue   { background: var(--blue-lt);   border-left: 3px solid var(--blue);   color: #2c5282; }
.alert-amber  { background: var(--amber-lt);  border-left: 3px solid #c05621;       color: var(--amber); }
.alert-red    { background: var(--red-lt);    border-left: 3px solid #c53030;       color: var(--red); }
.alert-green  { background: var(--teal-lt);   border-left: 3px solid var(--teal);   color: #22543d; }
.alert-purple { background: var(--purple-lt); border-left: 3px solid #6b46c1;       color: var(--purple); }

/* ── RECOMMENDATION BOX ── */
.rec-box {
  background: linear-gradient(135deg, #ebf8ff, #f0fff4);
  border: 1.5px solid #90cdf4; border-radius: var(--radius);
  padding: 16px 20px; margin-top: 14px;
}
.rec-box h4 {
  font-size: 0.82rem; font-weight: 700; color: var(--navy);
  margin-bottom: 8px; text-transform: uppercase; letter-spacing: 0.05em;
}
.rec-item { font-size: 0.81rem; color: var(--gray-700); padding: 5px 0; display: flex; gap: 8px; }
.rec-num { font-weight: 700; color: var(--blue); flex-shrink: 0; }

/* ── ACCORDION ── */
.accordion { border: 1px solid var(--gray-200); border-radius: var(--radius); overflow: hidden; }
.acc-item { border-bottom: 1px solid var(--gray-100); }
.acc-item:last-child { border-bottom: none; }
.acc-header {
  display: flex; justify-content: space-between; align-items: center;
  padding: 14px 18px; cursor: pointer; font-weight: 700; font-size: 0.85rem;
  color: var(--navy); background: white; user-select: none;
}
.acc-header:hover { background: var(--gray-50); }
.acc-arrow { transition: transform .2s; font-size: 0.75rem; color: var(--gray-400); }
.acc-item.open .acc-arrow { transform: rotate(180deg); }
.acc-body { display: none; padding: 14px 18px; background: var(--gray-50); border-top: 1px solid var(--gray-100); }
.acc-item.open .acc-body { display: block; }

/* ── DATA TABLES ── */
.data-table { width: 100%; border-collapse: collapse; font-size: 0.82rem; }
.data-table th {
  background: var(--navy); color: white; padding: 9px 12px;
  text-align: left; font-size: 0.75rem; letter-spacing: 0.04em; text-transform: uppercase;
}
.data-table td { padding: 9px 12px; border-bottom: 1px solid var(--gray-100); vertical-align: top; }
.data-table tr:hover td { background: var(--gray-50); }
.data-table tr:last-child td { border-bottom: none; }
.data-table .sub-head td { background: #edf2f7; font-weight: 700; font-size: 0.78rem; color: var(--navy); }

/* ── CALCULATOR INPUTS ── */
.field-group { display: flex; flex-direction: column; gap: 4px; }
.field-label { font-size: 0.78rem; font-weight: 600; color: var(--gray-700); }
.field-label .unit { font-weight: 400; color: var(--gray-500); }
.field-input {
  border: 1.5px solid var(--gray-200); border-radius: 7px;
  padding: 8px 12px; font-size: 0.88rem; color: var(--gray-900);
  background: white; width: 100%; transition: border-color .15s, box-shadow .15s;
}
.field-input:focus {
  outline: none; border-color: var(--blue);
  box-shadow: 0 0 0 3px rgba(43,108,176,0.15);
}
.btn-calc {
  background: var(--navy); color: white; border: none; border-radius: 8px;
  padding: 11px 24px; font-size: 0.88rem; font-weight: 700;
  cursor: pointer; width: 100%; margin-top: 4px; font-family: inherit;
}
.btn-calc:hover { background: var(--blue); }
.btn-clear {
  background: white; color: var(--gray-500); border: 1.5px solid var(--gray-200);
  border-radius: 8px; padding: 10px 24px; font-size: 0.82rem; font-weight: 600;
  cursor: pointer; width: 100%; margin-top: 6px; font-family: inherit;
}

/* ── CROSS-REFERENCE BANNERS ── */
/* See Section 14 for full usage rules */
.xref-banner {
  display: flex; align-items: center; gap: 14px;
  background: linear-gradient(135deg, #1a365d 0%, #2b6cb0 100%);
  border-radius: 10px; padding: 14px 18px; margin-bottom: 18px;
  border: none; cursor: pointer; width: 100%; text-align: left;
  text-decoration: none; color: white; font-family: inherit;
  box-shadow: 0 2px 10px rgba(26,54,93,0.18);
  transition: opacity 0.15s, transform 0.15s;
}
.xref-banner:hover { opacity: 0.92; transform: translateY(-1px); }
.xref-icon {
  font-size: 1.8rem; flex-shrink: 0;
  background: rgba(255,255,255,0.15); border-radius: 50%;
  width: 48px; height: 48px; display: flex; align-items: center; justify-content: center;
}
.xref-body { flex: 1; }
.xref-label {
  font-size: 0.65rem; font-weight: 700; text-transform: uppercase;
  letter-spacing: 0.1em; color: rgba(255,255,255,0.65); margin-bottom: 2px;
}
.xref-title { font-size: 0.95rem; font-weight: 800; color: white; margin-bottom: 2px; }
.xref-sub { font-size: 0.78rem; color: rgba(255,255,255,0.75); line-height: 1.4; }
.xref-arrow { font-size: 1.2rem; color: rgba(255,255,255,0.6); flex-shrink: 0; }
.xref-banner.xref-purple {
  background: linear-gradient(135deg, #44337a 0%, #6b46c1 100%);
  box-shadow: 0 2px 10px rgba(68,51,122,0.22);
}
.xref-banner.xref-teal {
  background: linear-gradient(135deg, #1a4a4a 0%, #2c7a7b 100%);
  box-shadow: 0 2px 10px rgba(26,74,74,0.22);
}

/* ── CITATION FOOTER ── */
.citation-footer {
  margin-top: 2.5rem; padding: 1.5rem 2rem;
  background: var(--navy); border-radius: 12px;
  color: rgba(255,255,255,0.7); font-size: 0.79rem; line-height: 1.65;
}
.citation-footer strong { color: rgba(255,255,255,0.9); }
.citation-footer a { color: #f6ad55; text-decoration: none; }
.citation-footer a:hover { text-decoration: underline; }
.citation-footer em { opacity: 0.65; font-size: 0.74rem; }

/* ── PAGE FOOTER ── */
footer {
  border-top: 1px solid var(--gray-200); text-align: center;
  padding: 16px 24px; font-size: 0.76rem; color: var(--gray-400);
  max-width: 1100px; margin: 0 auto;
}
footer a { color: var(--gray-500); text-decoration: none; }

/* ── RESPONSIVE ── */
@media(max-width: 600px) {
  header { padding: 20px 16px 18px; }
  .content { padding: 16px 12px 48px; }
  .nav-btn { padding: 8px 12px; font-size: 0.78rem; }
  .card { padding: 16px 14px; }
  .grid-2, .grid-3 { grid-template-columns: 1fr; }
}
```

---

## 5. Color Palette

### UI Colors (CSS variables)
| Token | Hex | Use |
|---|---|---|
| `--navy` | `#1a365d` | Header gradient start, active nav, headings |
| `--blue` | `#2b6cb0` | Header gradient end, links, hover states |
| `--blue-lt` | `#ebf8ff` | Blue hover background |
| `--teal` | `#276749` | Normal/good values, Class I green |
| `--teal-lt` | `#f0fff4` | Green background tints |
| `--red` | `#742a2a` | Danger, high-risk content |
| `--red-lt` | `#fff5f5` | Red background tints |
| `--amber` | `#744210` | Warning, borderline values |
| `--amber-lt` | `#fffaf0` | Amber background tints |
| `--purple` | `#44337a` | Special categories |
| `--purple-lt` | `#faf5ff` | Purple background tints |
| `--gray-900` | `#1a202c` | Primary body text |
| `--gray-700` | `#2d3748` | Secondary text |
| `--gray-500` | `#718096` | Muted text, section intros |
| `--gray-200` | `#e2e8f0` | Borders, dividers |
| `--bg` | `#f8f9fa` | Page background |

### SVG Flowchart Colors
| Element | Hex | Notes |
|---|---|---|
| Arrow lines & box borders | `#2c4a73` | All lines, all box strokes |
| Default box fill | `#e7edf3` | All question/content boxes |
| Class I header strip | `#7fb98b` | Sage green |
| Class IIb header strip | `#e89a4a` | Warm orange |
| Class III header strip | `#e89a4a` | Same orange as IIb |
| Phenotype / Yes / No pills | `#ffffff` | White fill, `#2c4a73` stroke |
| Divider lines inside boxes | `#9eb2cc` | Light blue |
| Dashed routing lines | `#2c4a73` | `stroke-dasharray="6,3"` |
| Arrow polygon fill | `#2c4a73` | Matches line stroke |
| Citation text | `#94a3b8` | Bottom of SVG |

---

## 6. Header Pattern

```html
<header>
  <div class="icon">🫀</div>
  <h1>Hypertrophic Cardiomyopathy</h1>
  <p class="subtitle">2022 ASE Multimodality Imaging Guidelines — Comprehensive Reference</p>
  <div class="guideline-badge">
    JASE 2022 · Nagueh et al. · DOI 10.1016/j.echo.2022.03.012 · ASE · ASNC · SCMR · SCCT
  </div>
</header>
```

**Rules:**
- Dark blue gradient (`#1a365d → #2b6cb0`)
- One single pill badge — all citation info on one line
- Emoji icon above h1, not inline with text
- No multiple badges

---

## 7. Navigation Tabs

- Justify center, wrap on mobile
- Inactive: white bg, gray border, gray text
- Hover: blue border, blue text, light blue bg
- Active: solid navy bg, white text, subtle shadow
- Max ~8 tabs; combine related topics if more content needed
- Tab labels should be short (1–3 words)

---

## 8. Citation Footer

Place at the bottom of the last tab panel:

```html
<div class="citation-footer">
  <strong>Citation:</strong> Nagueh SF et al. Recommendations for Multimodality Cardiovascular
  Imaging of Patients with HCM. <em>J Am Soc Echocardiogr.</em> 2022;35:533–569.
  <br><br>
  📄 <a href="https://doi.org/10.1016/j.echo.2022.03.012" target="_blank">
    DOI: 10.1016/j.echo.2022.03.012
  </a> &nbsp;|&nbsp;
  <a href="https://www.asecho.org" target="_blank">American Society of Echocardiography</a>
  <br><br>
  <em>Educational reference only. Does not replace clinical judgment or individualized patient assessment.</em>
</div>
```

---

## 9. SVG Flowcharts — Complete Rules

### When to use SVG
- **Always use SVG** for any branching algorithm or flowchart
- Never use HTML flexbox for flowcharts — impossible to control arrow positioning
- Always wrap SVG in `<div style="overflow-x:auto; -webkit-overflow-scrolling:touch;">`

### Canvas sizing
```html
<div style="overflow-x:auto; -webkit-overflow-scrolling:touch;">
<svg viewBox="0 0 1200 1100" xmlns="http://www.w3.org/2000/svg"
     style="width:100%; min-width:760px; display:block;
            font-family:'Segoe UI',system-ui,sans-serif;">
```

**Rules:**
- **Make the viewBox wider than you think you need** — 1200px minimum for two-column algorithms
- Height: bottom-most element y + height + 80px for citation line
- `min-width: 760px` ensures mobile scrolls horizontally rather than squishing
- Always verify: `rightmost element right edge + 15px ≤ viewBox width`

### Arrow marker — always include in `<defs>`
```svg
<defs>
  <marker id="hcmArr" markerWidth="11" markerHeight="8" refX="10" refY="4" orient="auto">
    <polygon points="0 0, 11 4, 0 8" fill="#2c4a73"/>
  </marker>
</defs>
```
Usage on lines: `stroke="#2c4a73" stroke-width="2" marker-end="url(#hcmArr)"`

### Standard box sizes
| Element | Width | Height | Font sizes |
|---|---|---|---|
| Entry/title box (full width) | 800–1000px | 50–60px | 17px title, 14px subtitle |
| Phenotype pill | 200–220px | 40–44px | 15–16px |
| Question box | 220–240px | 80–110px | 14–15px |
| Yes/No pill | 100–140px | 34–40px | 14–15px |
| Class I / IIb box | 220–240px | 180–210px | 17px header, 14–15px body |
| Comprehensive eval box | 600–700px | 210–240px | 16–18px title, 13–14px body |
| Class III box | 220–240px | 100–140px | 15px header, 13px body |

### CRITICAL: Branch line arrow rules

```
✅ CORRECT:
   Horizontal branch lines → NO arrowhead
   Vertical drop lines    → YES arrowhead pointing DOWN

❌ WRONG:
   Arrowhead on horizontal branch → looks like it points INTO the label pill
```

```svg
<!-- Horizontal branches from entry box — NO marker-end -->
<line x1="600" y1="125" x2="180" y2="125" stroke="#2c4a73" stroke-width="2"/>
<line x1="600" y1="125" x2="1020" y2="125" stroke="#2c4a73" stroke-width="2"/>

<!-- Vertical drops — YES marker-end -->
<line x1="180" y1="125" x2="180" y2="196" stroke="#2c4a73" stroke-width="2" marker-end="url(#hcmArr)"/>
<line x1="1020" y1="125" x2="1020" y2="196" stroke="#2c4a73" stroke-width="2" marker-end="url(#hcmArr)"/>
```

### CRITICAL: Phenotype pill centering rule

The phenotype pill cx must match the cx of all content below it. Calculate column cx first, then set pill position.

```
✅ CORRECT: column content cx=890 → pill cx=890 → branch ends at x=890
❌ WRONG:   branch ends at x=1020 → pill cx=1020 → content below cx=890 (off-center)
```

### "No" routing pattern (two questions → same Class III box)

```svg
<!-- Q1 No: dashed right from Q1 right edge to merge vertical -->
<line x1="260" y1="133" x2="440" y2="133" stroke="#2c4a73" stroke-width="1.8" stroke-dasharray="6,3"/>
<rect x="322" y="121" width="58" height="22" rx="11" fill="white" stroke="#2c4a73" stroke-width="1.5"/>
<text x="351" y="136" text-anchor="middle" fill="#2c4a73" font-size="13" font-weight="600">No</text>

<!-- Q2 No: dashed right to same merge vertical -->
<line x1="260" y1="235" x2="440" y2="235" stroke="#2c4a73" stroke-width="1.8" stroke-dasharray="6,3"/>
<rect x="322" y="223" width="58" height="22" rx="11" fill="white" stroke="#2c4a73" stroke-width="1.5"/>
<text x="351" y="238" text-anchor="middle" fill="#2c4a73" font-size="13" font-weight="600">No</text>

<!-- Shared vertical merge line down to Class III entry point -->
<line x1="440" y1="133" x2="440" y2="308" stroke="#2c4a73" stroke-width="1.8" stroke-dasharray="6,3"/>
<!-- Arrow right into Class III left edge -->
<line x1="440" y1="308" x2="448" y2="308" stroke="#2c4a73" stroke-width="1.8" marker-end="url(#hcmArr)"/>
```

**Class III box must be tall enough** to span both No entry y-values:
- Top = first No y − 20px
- Bottom = second No y + 20px

### Bracket / cross-connector pattern (two boxes → two pills)

```svg
<!-- Both class boxes drop to shared horizontal bar -->
<line x1="760"  y1="788" x2="760"  y2="806" stroke="#2c4a73" stroke-width="2"/>
<line x1="1020" y1="788" x2="1020" y2="806" stroke="#2c4a73" stroke-width="2"/>
<!-- Horizontal bar connecting them -->
<line x1="760" y1="806" x2="1020" y2="806" stroke="#2c4a73" stroke-width="2"/>
<!-- Arrows down from each end to respective pills -->
<line x1="760"  y1="806" x2="760"  y2="818" stroke="#2c4a73" stroke-width="2" marker-end="url(#hcmArr)"/>
<line x1="1020" y1="806" x2="1020" y2="818" stroke="#2c4a73" stroke-width="2" marker-end="url(#hcmArr)"/>
```

### Colored header strip inside box

```svg
<!-- Box background -->
<rect x="640" y="578" width="240" height="210" rx="12" fill="#e7edf3" stroke="#2c4a73" stroke-width="1.6"/>
<!-- Header strip — use path to round only top corners -->
<path d="M 640 590 L 640 578 Q 640 578 652 578 L 868 578 Q 880 578 880 590 L 880 614 L 640 614 Z" fill="#7fb98b"/>
<!-- Header text -->
<text x="760" y="602" text-anchor="middle" fill="white" font-size="17" font-weight="800">Class I</text>
<!-- Body text below -->
<text x="760" y="635" text-anchor="middle" fill="#1a2942" font-size="15" font-weight="700">Every 1–2 years</text>
```

**Strip colors:**
- Class I: `#7fb98b` (sage green)
- Class IIb: `#e89a4a` (warm orange)
- Class III No Benefit: `#e89a4a` (same orange)
- Entry boxes: `#1a365d` (navy) or `#2b6cb0` (blue)

### SVG text rules
- Always `text-anchor="middle"` with x at box centre for centred text
- Left-aligned text: `x = box_left_edge + 14` with no text-anchor
- **Never** put two text sub-columns inside a narrow SVG half-width — overflow is invisible and hard to debug
- For divided content inside one box, use a `<line>` divider and ensure each half has ≥280px width
- Verify: `text_x + (character_count × 8px) < box_right_edge` (rough check at font-size 14)

### Pre-flight coordinate check
Before finalising any SVG, verify:
```
Gap between adjacent boxes = right_box_x − (left_box_x + left_box_width) ≥ 8px
Right margin = viewBox_width − (rightmost_box_x + rightmost_box_width) ≥ 15px
Arrow entry point y is between box_top and box_bottom
Text cx matches box cx (for centred text)
Phenotype pill cx matches column cx below it
```

---

## 10. Clinical Accuracy Rules

### Nuclear imaging — modality specificity
- **PET** → quantitative myocardial blood flow (MBF) / stress perfusion imaging
- **Tc-based bone scintigraphy (Tc-PYP)** → ATTR amyloidosis (NOT PET)
- These are different modalities for different questions — never conflate them

### EF thresholds — use strict less-than
- Systolic dysfunction: **EF <50%** (strictly less than)
- Never write ≤50% in SCD risk contexts — use `<50%` throughout
- Source: 2022 ASE HCM guidelines; 2020 AHA/ACC HCM guidelines

### ICD indications — name the specific risk factor
- Specify the exact finding: "Apical aneurysm → Class IIa ICD consideration"
- Do NOT write: "MVO → Class IIa ICD" — MVO itself is not the ICD trigger
- MVO can be complicated by apical aneurysm — the aneurysm drives ICD consideration
- Always use UEA or CMR to evaluate for apical aneurysm in MVO/apical HCM

### Recommendation class wording
| Class | Meaning | Phrasing |
|---|---|---|
| Class I | Strongly recommended | Benefit >>> Risk |
| Class IIa | Reasonable | Benefit >> Risk |
| Class IIb | May be considered (weak) | Benefit ≥ Risk |
| Class III | Not recommended | Benefit = Risk or Risk > Benefit |

### General rule
When in doubt, quote the guideline text directly rather than paraphrasing. Always include the DOI and publication year. If using a poster/summary document, cross-reference with the primary guideline paper.

---

## 11. Homepage Card (root index.html)

Add this block inside the appropriate `.tool-grid` div in root `index.html`:

```html
<a class="tool-card" href="folder-name/">
  <div class="card-top top-blue"></div>
  <div class="card-body">
    <span class="card-icon">🫀</span>
    <div class="card-name">Card Name</div>
    <div class="card-desc">
      2–3 sentence description of the guideline and key interactive features.
    </div>
  </div>
  <div class="card-footer">
    <span>Author et al., Journal Year</span>
    <span class="card-launch">Open →</span>
  </div>
</a>
```

**Stripe classes:** `top-blue` `top-green` `top-purple` `top-red` `top-amber` `top-teal`

`top-teal` is defined in root `index.html` as:
```css
.top-teal { background: linear-gradient(90deg, #1a4a4a, #2c7a7b); }
```

Also add to the feedback modal `<select>` dropdown:
```html
<option>New Card Name</option>
```

---

## 12. Deployment Steps

1. Create folder `card-name/` in the repo root
2. Upload `index.html` into that folder (for large files >10KB use the .txt rename method — see Section 13)
3. Edit root `index.html` — add card block to the correct `.tool-grid` in the correct homepage order
4. Edit root `index.html` — add card name to feedback modal `<select>`
5. Commit all changes
6. Verify at `https://echoinfo.org/card-name/`
7. Verify root homepage shows the new card in the correct position
8. Check mobile layout: nav wraps, cards stack, SVG scrolls horizontally

---

## 13. Known Gotchas & Lessons Learned

**GitHub Pages CDN caching:** After committing, check `raw.githubusercontent.com` to confirm the commit landed. The live site may lag a few minutes. If stale content persists, contact GitHub Support.

**Large file injection via GitHub editor:** GitHub's CodeMirror editor lazy-loads files >2–3KB. For files over ~10KB, use the manual paste method: rename `.html` → `.txt`, open in TextEdit (Mac), copy all, paste into GitHub editor, rename back.

**SVG text overflow is invisible:** Text that overflows a box still renders — it just appears on top of adjacent elements. Always calculate character-width estimates before finalising. At font-size 14px, allow ~8px per character.

**Phenotype pill off-center:** Calculate the entire right column's cx first (based on box positions), then set the phenotype pill and branch endpoint to that same cx. Not the other way around.

**Two sub-columns inside a narrow SVG half:** Don't attempt this. If the half-width is less than ~320px, use a single column. If you need two sub-columns for risk factors etc., ensure each sub-column's text width fits within its allocated pixels.

**EF threshold:** Always `<50%` not `≤50%` for HCM systolic dysfunction.

**Mobile nav with many tabs:** More than 6 tabs will wrap to two lines on narrow screens. This is acceptable — `flex-wrap: wrap` handles it. Keep labels short to minimize wrapping.

**SVG on mobile:** The `min-width: 760px` + `overflow-x: auto` pattern works well. Do not try to make complex flowcharts fully responsive — horizontal scrolling is acceptable and expected for algorithm diagrams.

**showTab requires event argument:** The JS tab function signature is `showTab(id, event)`. Always pass `event` from the onclick: `onclick="showTab('overview', event)"`. The old single-argument form breaks active-state highlighting on the nav buttons.

---

## 14. Cross-Reference Banners

Use when a card's content overlaps with, or has been superseded by, another card. Two formats — pick one per reference per page, never both.

### Format A — Full banner (top of a tab panel)

Use when an entire tab's subject is better covered in a dedicated card. Place as the **first element inside the panel div**, before any `.card` blocks.

```html
<a class="xref-banner xref-teal" href="../right-heart-ph/">
  <div class="xref-icon">💜</div>
  <div class="xref-body">
    <div class="xref-label">See dedicated guideline card</div>
    <div class="xref-title">Right Heart &amp; Pulmonary Hypertension</div>
    <div class="xref-sub">2025 ASE guidelines — comprehensive RV function grading, PH probability,
    RAP algorithm, RV strain thresholds, WSPH classification, and updated normal values
    (Mukherjee et al., JASE 2025)</div>
  </div>
  <div class="xref-arrow">→</div>
</a>
```

**Color variants:**
| Class | Gradient | Use for |
|---|---|---|
| *(none)* | Navy → blue | General / LV references |
| `.xref-teal` | Dark teal → teal | Right Heart / RV references |
| `.xref-purple` | Dark purple → purple | Strain references |

### Format B — Inline pill (inside a table sub-head row)

Use when only a specific table section is outdated, not the whole tab.

```html
<tr class="sub-head">
  <td colspan="4">
    <div style="display:flex; align-items:center; justify-content:space-between; flex-wrap:wrap; gap:8px;">
      Right Ventricle — 2015 ASE Reference Values
      <a href="../right-heart-ph/"
         style="font-size:0.72rem; font-weight:700; color:#2c7a7b;
                background:#e6fffa; border:1px solid #81e6d9;
                border-radius:999px; padding:2px 10px;
                white-space:nowrap; text-decoration:none; letter-spacing:0.02em;">
        Updated 2025 guidelines →
      </a>
    </div>
  </td>
</tr>
```

**Pill color pairs by topic:**
| Topic | Text | Background | Border |
|---|---|---|---|
| RV / Right Heart | `#2c7a7b` | `#e6fffa` | `#81e6d9` |
| Strain | `#6b46c1` | `#faf5ff` | `#b794f4` |
| General / LV | `#2b6cb0` | `#ebf8ff` | `#90cdf4` |

**Rules:**
- Never use both Format A and Format B for the same reference on the same page — pick one
- Format A for whole-tab supersession; Format B for specific table rows only
- The `colspan` value must match the number of columns in that table

---

## 15. Data Table Patterns

### Standard sub-head row
```html
<tr class="sub-head"><td colspan="4">Section Label</td></tr>
```
Renders as a gray-background divider with navy bold text. Adjust `colspan` to match column count.

### Highlighted "featured" column
Use when one column represents newer or preferred data (e.g. WASE 2022 alongside older normative studies):

```html
<!-- Header cell -->
<th style="background:#1e4d8c; border-left:3px solid #90cdf4;">
  WASE 2022 ★<br>
  <span style="font-weight:400; font-size:0.7rem; opacity:0.85;">Global · n=1,589</span>
</th>

<!-- Data cells in that column — apply to every row including sub-heads -->
<td style="background:#f0f7ff; font-weight:600; border-left:3px solid #90cdf4;">
  70 ± 15<br>
  <span style="font-size:0.75rem; color:#4a7db5;">(LLN–ULN: 45–79)</span>
</td>
```

The `border-left:3px solid #90cdf4` on both `<th>` and every `<td>` in the column creates a continuous left-edge accent. Apply consistently to every row in that column.

### Inline note cards below a table

When a table needs source attribution or a clinical caveat, use two side-by-side note divs:

```html
<div style="margin-top:10px; display:flex; flex-wrap:wrap; gap:8px; align-items:flex-start;">
  <div style="background:#ebf8ff; border:1px solid #90cdf4; border-radius:6px;
              padding:8px 12px; font-size:0.78rem; color:#2c5282;
              flex:1; min-width:220px;">
    <strong>★ Source note</strong> — Study name, n, method, key finding.
  </div>
  <div style="background:#fffaf0; border:1px solid #f6ad55; border-radius:6px;
              padding:8px 12px; font-size:0.78rem; color:#744210;
              flex:1; min-width:220px;">
    <strong>⚠️ Clinical caveat</strong> — Important limitation or context.
  </div>
</div>
```

Use blue (`#ebf8ff` / `#90cdf4`) for source/citation notes and amber (`#fffaf0` / `#f6ad55`) for warnings. Both boxes flex to fill the row and stack on mobile via `flex-wrap:wrap`.

---

*echoinfo.org · Created by Akhil Narang, MD · Last updated May 2026*
