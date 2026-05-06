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

You are adding a new AI prompt entry to the **Crisp Assessment AI Process Plan** — a single
self-contained HTML file at:

```
C:\Users\COverholser\Documents\Cantactix\Templates\Crisp-Assessment-AI-Process-Plan.html
```

## Your job

1. Gather the prompt details from the user (or infer what you can)
2. Read the HTML file to find the current highest prompt ID and the correct insertion point
3. Generate the new prompt's HTML block
4. Insert it into the file in the right phase section
5. Confirm what was added

---

## Step 1 — Collect prompt details

You need these five things. Ask for any that are missing, but make reasonable inferences
where you can (e.g. if the user pastes a prompt and says "add this to phase 3", you can
draft the title and input description from the prompt text itself):

| Field | Description | Required |
|---|---|---|
| **title** | Short display name (e.g. "Workshop Gap Flagging") | Yes |
| **phase** | Which phase: 1 (Intake), 2 (Discovery), 3 (Analysis), or 4 (Roadmap & Readout) | Yes |
| **type** | `NOW` (existing workflow) or `NEW` (newly designed) | Yes |
| **input_description** | Plain-English description of what the user pastes into Claude before running this prompt | Yes |
| **prompt_text** | The actual Claude prompt text, verbatim | Yes |
| **note** | Optional tip, edge case, or quality check for the user | No |

---

## Step 2 — Read the HTML file and determine IDs

Read the HTML file. Find all existing prompt card IDs (they look like `id="pc1"`, `id="pc2"`, etc.)
and prompt text IDs (`id="pt1"`, `id="pt2"`, etc.). The next prompt gets the next sequential
integer — if the highest existing ID is `pc10`, the new one is `pc11` / `pt11`.

Also locate the correct insertion point. The file has one `.prompt-phase-title` block per phase
in the `id="page-prompts"` section. Find the last `.prompt-card` block within the target phase's
group — insert the new card immediately after it.

**Important:** If the `id="page-prompts"` section doesn't exist yet (the library hasn't been
built), tell the user and offer to scaffold the full prompt library section first.

---

## Step 3 — Generate the HTML block

Use this exact template. Replace all {placeholders}:

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

Where:
- `{N}` = the next sequential integer
- `{badge_class}` = `badge-current` when type is NOW, or `badge-new` when type is NEW
- `{note_block}` = empty string if no note, or:
  ```html
  
    <div class="prompt-note">{note}</div>
  ```

Escape any HTML special characters in prompt_text and input_description:
- `&` → `&amp;`
- `<` → `&lt;`
- `>` → `&gt;`

The prompt_text block uses `white-space: pre-wrap` styling — preserve line breaks exactly as
the user provides them. Do not collapse or reformat the prompt text.

---

## Step 4 — Insert into the file

Use the Edit tool to insert the new HTML block. The insertion point is immediately after the
closing `</div>` of the last `.prompt-card` in the target phase group, and before either the
next `.prompt-phase-title` or the closing `</div>` of the page section.

After editing, do a quick sanity check: search the file for the new `id="pc{N}"` to confirm
it was inserted correctly.

---

## Step 5 — Confirm

Tell the user:
- The prompt title and ID assigned (e.g. "Added 'Workshop Gap Flagging' as pc11/pt11")
- Which phase section it was added to
- That the copy button is wired to `copyPrompt('pt{N}', this)` and will work immediately

---

## CSS reference (already in the file — do not duplicate)

```
.prompt-card, .prompt-header, .prompt-header:hover
.prompt-title, .prompt-meta, .prompt-chevron
.prompt-card.open .prompt-chevron  (rotate 180°)
.prompt-body, .prompt-card.open .prompt-body  (display: block)
.prompt-section, .prompt-section-label
.prompt-text  (green-tinted code block, pre-wrap)
.copy-btn, .copy-btn:hover, .copy-btn.copied
.prompt-note  (amber left-border tip box)
.ai-step-badge, .badge-current, .badge-new
```

JavaScript functions `togglePrompt(id)` and `copyPrompt(id, btn)` are already defined.

---

## Edge cases

- **Prompt library section missing:** If `id="page-prompts"` doesn't exist in the HTML, stop
  and tell the user. Offer to scaffold it before adding the prompt.

- **Phase section missing within the library:** If the target phase's `.prompt-phase-title`
  doesn't exist yet inside `page-prompts`, add it before the new card:
  ```html
  <div class="prompt-phase-title">Phase {phase} — {phase_name}</div>
  ```
  Phase names: 1 = Intake, 2 = Discovery, 3 = Analysis & Opportunity Log, 4 = Roadmap & Readout

- **User provides a prompt idea, not final text:** Draft the prompt using the established
  style (structured numbered steps, ends with a [PASTE X HERE] placeholder). Show the draft
  and ask for approval before inserting.

- **Duplicate title:** If a prompt with the same title already exists, flag it and confirm before adding.
