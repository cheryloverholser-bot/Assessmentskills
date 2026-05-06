---
name: crisp-raci-sync
description: >
  Updates the RACI assignments across the Crisp Assessment HTML site — both the per-phase
  RACI chips and the full RACI Quick Reference table. Use when role assignments change,
  when the user says "update the RACI", "change who's responsible for phase 2", "sync the
  RACI table", or "add a role to the matrix."
---

# Crisp RACI Sync

## Step 0 — Find the HTML file

Search for the file in this order:
1. Current working directory: `Crisp-Assessment-AI-Process-Plan.html`
2. Recursively in cwd: any file matching `*Assessment*Process*.html`
3. Known default: `C:\Users\COverholser\Documents\Cantactix\Templates\Crisp-Assessment-AI-Process-Plan.html`

If not found, ask the user.

---

## TODO: Implement this skill

**What it should do:**
1. Accept updated RACI assignments (phase, activity/deliverable, R/A/C/I roles)
2. Update the RACI chips in each phase page (`id="page-phase{N}"`)
3. Update the full RACI reference table (`id="page-raci"`)
4. Keep both in sync — single source of truth

**Target file:** `Crisp-Assessment-AI-Process-Plan.html (search cwd first, fall back to known path)`

**RACI chip structure (per-phase):**
```html
<div class="raci-wrap">
  <span class="chip chip-r">R: Role Name</span>
  <span class="chip chip-a">A: Role Name</span>
  <span class="chip chip-c">C: Role Name</span>
  <span class="chip chip-i">I: Role Name</span>
</div>
```

**RACI table structure (reference page):**
```html
<table class="raci-table">
  <thead><tr><th>Phase</th><th>Deliverable</th><th>R</th><th>A</th><th>C</th><th>I</th></tr></thead>
  <tbody>
    <tr>
      <td><span class="phase-tag">Phase 1</span></td>
      <td>Deliverable name</td>
      <td>Role</td><td>Role</td><td>Role</td><td>Role</td>
    </tr>
  </tbody>
</table>
```

**Known roles (from source docs):**
- Project Manager
- Business Consultant  
- Dir. Business Solutions
- Solutions Consultant
- Technical Architect
- VP Consulting Services
- Client Sponsor
