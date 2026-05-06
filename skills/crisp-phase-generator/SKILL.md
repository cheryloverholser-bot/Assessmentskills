---
name: crisp-phase-generator
description: >
  Generates or updates a phase page in the Crisp Assessment HTML site. Use when the user
  wants to build out a phase page, update phase content, add activities or AI steps to a
  phase, or when they say "build phase 2", "add an activity to phase 3", "update the gate
  for phase 1", or "add an AI step to the discovery phase."
---

# Crisp Phase Generator

## Step 0 — Find the HTML file

Search for the file in this order:
1. Current working directory: `Crisp-Assessment-AI-Process-Plan.html`
2. Recursively in cwd: any file matching `*Assessment*Process*.html`
3. Known default: `C:\Users\COverholser\Documents\Cantactix\Templates\Crisp-Assessment-AI-Process-Plan.html`

If not found, ask the user.

---

## TODO: Implement this skill

**What it should do:**
1. Accept phase metadata (number, inputs, activities, AI steps, output, RACI, gate criteria)
2. Generate the full phase page HTML using the standard 3-column + 2-column + gate layout
3. Insert or replace the `id="page-phase{N}"` section in the HTML file

**Target file:** `Crisp-Assessment-AI-Process-Plan.html (search cwd first, fall back to known path)`

**Phase page structure (must follow this exactly):**
```
page-header (phase title + gate pill)
  └── three-col
        ├── .card — Inputs (bullet list)
        ├── .card — Key Activities (progress-task checkboxes)
        └── .card.ai — ✦ AI Steps (badge-current NOW / badge-new NEW)
  └── two-col
        ├── .card — Output (title, description, template links)
        └── .card — RACI (chips: chip-r, chip-a, chip-c, chip-i)
  └── .gate-card (gate icon, title, bullet criteria)
```

**CSS classes already in file:**
- `.three-col`, `.two-col`, `.card`, `.card.ai`, `.ai-tag`, `.ai-step`, `.ai-step-badge`
- `.badge-current` (NOW), `.badge-new` (NEW)
- `.progress-task`, `.progress-check` (for checkbox tasks)
- `.gate-card`, `.gate-title`, `.gate-items`
- `.chip`, `.chip-r`, `.chip-a`, `.chip-c`, `.chip-i`
- `.tpl-link` (template pill links)

**Phase IDs:** `page-phase1` through `page-phase4`

**Notes:**
- Each activity needs `data-phase="{N}"` and `data-task="{index}"` for progress tracking
- AI Steps section links to the prompt library: `onclick="nav('prompts')"`
- Gate card icon: 🚦 for phases 1–3, 🏁 for phase 4
