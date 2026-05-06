---
name: crisp-engagement-generator
description: >
  Spins up a complete new client engagement package from the Crisp Assessment templates —
  copies the HTML site, names it for the client, and prepares a folder structure. Use when
  starting a brand new engagement, when the user says "create an engagement for [client]",
  "spin up a new assessment for [client name]", or "set up the files for a new client."
---

# Crisp Engagement Generator

## Step 0 — Find the HTML file

Search for the file in this order:
1. Current working directory: `Crisp-Assessment-AI-Process-Plan.html`
2. Recursively in cwd: any file matching `*Assessment*Process*.html`
3. Known default: `C:\Users\COverholser\Documents\Cantactix\Templates\Crisp-Assessment-AI-Process-Plan.html`

If not found, ask the user.

---

## TODO: Implement this skill

**What it should do:**
1. Ask for: client name, engagement lead, start date, and engagement folder location
2. Create a new engagement folder: `[ClientName] Assessment [YYYY-MM]/`
3. Copy `Crisp-Assessment-AI-Process-Plan.html` into it, renamed to `[ClientName]-Assessment-Process.html`
4. Pre-configure the copied HTML with the client name and lead baked into the JS defaults
5. Create subfolders: `Templates/`, `Deliverables/`, `Notes/`
6. Summarize what was created and how to open it

**Source file:** `Crisp-Assessment-AI-Process-Plan.html (search cwd first, fall back to known path)`
**Templates source:** `[assessment templates directory]Assessments Templates\`
**Default engagement root:** `[engagements root directory]`

**Folder structure to create:**
```
[ClientName] Assessment [YYYY-MM]/
├── [ClientName]-Assessment-Process.html   ← pre-configured copy
├── Templates/                              ← copies of all assessment templates
│   ├── CMS.QUESTIONNAIRE.docx
│   ├── Assessment Workshop Guide.pptx
│   └── [all other templates]
├── Deliverables/                           ← empty, for outputs
└── Notes/                                  ← empty, for raw notes
```

**JS to pre-configure in the copied HTML:**
```javascript
// Pre-fill setup modal defaults
document.getElementById('clientName').value = 'CLIENT NAME';
document.getElementById('engagementLead').value = 'LEAD NAME';
```

**Notes:**
- Client name should be sanitized for use in filenames (no special chars)
- Do not modify the source HTML — always work on the copy
- Confirm the folder location with the user before creating
