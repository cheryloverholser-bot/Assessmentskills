---
name: crisp-progress-reporter
description: >
  Reports the build status of the Crisp Assessment HTML site against the implementation
  plan. Use when the user wants to know what's done and what's left, when they say "what's
  left to build", "how far along is the site", "check the build progress", or "what tasks
  are complete."
---

# Crisp Progress Reporter

## Step 0 — Find the HTML file

Search for the file in this order:
1. Current working directory: `Crisp-Assessment-AI-Process-Plan.html`
2. Recursively in cwd: any file matching `*Assessment*Process*.html`
3. Known default: `C:\Users\COverholser\Documents\Cantactix\Templates\Crisp-Assessment-AI-Process-Plan.html`

If not found, ask the user.

---

## TODO: Implement this skill

**What it should do:**
1. Read the implementation plan at:
   `[assessment templates directory]docs\superpowers\plans\2026-05-06-assessment-process-plan.md`
2. Parse the checkbox tasks (`- [ ]` = todo, `- [x]` = done)
3. Read the HTML file and verify which sections actually exist (not just checked off)
4. Produce a clear status report: what's complete, what's in progress, what's missing

**Target files:**
- Plan: `[assessment templates directory]docs\superpowers\plans\2026-05-06-assessment-process-plan.md`
- HTML: `Crisp-Assessment-AI-Process-Plan.html (search cwd first, fall back to known path)`

**Tasks from implementation plan (9 total):**
1. HTML shell + brand CSS + topbar ✅ (exists in HTML)
2. Sidebar navigation + shell layout ✅
3. Setup modal + localStorage ✅
4. Resume project + feature toggles ✅
5. Phase pages (1–4) with content 🔲
6. AI Prompt Library ✅ (10 prompts added)
7. RACI Quick Reference 🔲
8. Decision Gates page 🔲
9. Print view + search + polish 🔲

**Output format:**
```
BUILD STATUS — Crisp Assessment AI Process Plan
================================================
✅ Complete (N tasks)
   - Task name
🔲 Remaining (N tasks)
   - Task name
📊 Overall: N/9 tasks complete (N%)
```

**Notes:**
- Verify by checking for key HTML elements, not just plan checkboxes
- Flag any section that exists in the HTML but is a placeholder ("coming soon")
