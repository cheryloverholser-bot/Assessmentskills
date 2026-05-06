---
name: crisp-prompt-builder
description: >
  Adds a new AI prompt entry to the Crisp Assessment Process HTML site's AI Prompt Library.
  Use this skill whenever the user wants to add, create, or insert a new Claude prompt into
  the Crisp assessment site — even if they just describe the prompt idea and don't have the
  full text yet. Handles ID sequencing, HTML generation, and file insertion automatically.
  Also use when the user says things like "add a prompt for X to the assessment site",
  "create a new prompt in the library", "put this prompt in phase 2", or "add this to the prompt library."
---

# Crisp Prompt Library Builder

You are adding a new AI prompt entry to the **Crisp Assessment AI Process Plan** HTML site.

## Step 0 — Find the HTML file

Search for the file in this order:
1. Current working directory: `Crisp-Assessment-AI-Process-Plan.html`
2. Recursively in cwd: any file matching `*Assessment*Process*.html`
3. Known default: `C:\Users\COverholser\Documents\Cantactix\Templates\Crisp-Assessment-AI-Process-Plan.html`

If none found, ask the user where the file is before proceeding.

---

## Step 1 — Collect prompt details

Ask for any that are missing. Infer what you can from context (e.g. if user pastes a prompt
and says "add this to phase 3", draft the title and input description from the prompt text):

| Field | Description | Required |
|---|---|---|
| **title** | Short display name (e.g. "Workshop Gap Flagging") | Yes |
| **phase** | 1 (Intake), 2 (Discovery), 3 (Analysis), or 4 (Roadmap & Readout) | Yes |
| **type** | `NOW` (existing workflow) or `NEW` (newly designed) | Yes |
| **input_description** | What the user pastes into Claude before running this prompt | Yes |
| **prompt_text** | The actual Claude prompt text, verbatim | Yes |
| **note** | Optional tip or quality check | No |

---

## Step 2 — Read the file and determine IDs

Find all existing `id="pc{N}"` and `id="pt{N}"` values. The new prompt gets the next
sequential integer (highest existing + 1).

Find the insertion point: last `.prompt-card` in the target phase group, inside `id="page-prompts"`.

If `id="page-prompts"` doesn't exist yet, tell the user the library section hasn't been built
and offer to scaffold it first.

---

## Step 3 — Generate the HTML block

```html
<div class="prompt-card" id="pc{N}">
  <div class="prompt-header" onclick="togglePrompt('pc{N}')">
    <div>
      <div class="prompt-title">{title}</div>
      <div class="prompt-meta">Phase {phase} · <span class="ai-step-badge badge-{badge_class}">{type}</span></div>
    </div>
    <div class="prompt-chevron">▾</div>
  </div>
  <div class="prompt-body">
    <div class="prompt-section">
      <div class="prompt-section-label">What to paste in</div>
      <div style="font-size:13px;color:var(--muted)">{input_description}</div>
    </div>
    <div class="prompt-section">
      <div class="prompt-section-label">Prompt — click to copy</div>
      <div class="prompt-text" id="pt{N}">{prompt_text}</div>
      <button class="copy-btn" onclick="event.stopPropagation(); copyPrompt('pt{N}', this)">Copy Prompt</button>
    </div>{note_block}
  </div>
</div>
```

- `{badge_class}` = `badge-current` for NOW, `badge-new` for NEW
- `{note_block}` = `<div class="prompt-note">{note}</div>` if note provided, else empty
- Escape `&` → `&amp;`, `<` → `&lt;`, `>` → `&gt;` in prompt_text and input_description
- Preserve all line breaks in prompt_text exactly (the element uses `white-space: pre-wrap`)

---

## Step 4 — Insert and verify

Insert immediately after the closing `</div>` of the last `.prompt-card` in the target phase,
before the next `.prompt-phase-title` or the section's closing tag.

Verify insertion: confirm `id="pc{N}"` appears in the file after editing.

---

## Step 5 — Confirm

Report: title, ID assigned (e.g. pc11/pt11), phase inserted into, copy button target.

---

## Reference: CSS and JS already in file (do not duplicate)

```
.prompt-card  .prompt-header  .prompt-title  .prompt-meta  .prompt-chevron
.prompt-body  .prompt-section  .prompt-section-label  .prompt-text
.copy-btn  .copy-btn.copied  .prompt-note
.ai-step-badge  .badge-current  .badge-new
```
Functions: `togglePrompt(id)`, `copyPrompt(id, btn)`

Phase section titles: Phase 1 = Intake · Phase 2 = Discovery ·
Phase 3 = Analysis & Opportunity Log · Phase 4 = Roadmap & Readout
