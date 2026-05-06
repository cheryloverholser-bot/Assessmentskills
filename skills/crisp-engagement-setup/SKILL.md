---
name: crisp-engagement-setup
description: >
  Sets up the Crisp Assessment HTML site for a new client engagement — populates the
  project name, engagement lead, and recommended feature toggles. Use when starting a
  new assessment, onboarding a new client, or when the user says "set up a new engagement",
  "configure the site for [client]", or "start an assessment for [client name]."
---

# Crisp Engagement Setup

## Step 0 — Find the HTML file

Search for the file in this order:
1. Current working directory: `Crisp-Assessment-AI-Process-Plan.html`
2. Recursively in cwd: any file matching `*Assessment*Process*.html`
3. Known default: `C:\Users\COverholser\Documents\Cantactix\Templates\Crisp-Assessment-AI-Process-Plan.html`

If not found, ask the user.

---

## TODO: Implement this skill

**What it should do:**
1. Ask for: client name, engagement lead name, and optionally which features to enable
   (Progress Tracker, Print View, Search, Changelog)
2. Read `Crisp-Assessment-AI-Process-Plan.html`
3. Pre-fill the setup modal defaults in the JS so the site opens ready for that client
4. Optionally generate a localStorage JSON snippet the user can paste into browser console
   to skip the setup modal entirely on first open

**Target file:** `Crisp-Assessment-AI-Process-Plan.html (search cwd first, fall back to known path)`

**Key JS object to populate:**
```javascript
projectData = {
  client: "CLIENT NAME",
  lead: "LEAD NAME",
  features: { progress: true, print: true, search: false, changelog: false },
  progress: { 1: {}, 2: {}, 3: {}, 4: {} }
}
```

**Notes:**
- The setup modal is at `id="setupModal"` in the HTML
- Default input values can be set via `document.getElementById('clientName').value`
- localStorage key is `crispAssessment`
