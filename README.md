# Assessment Skills — Crisp Claude Plugin

A Claude Code plugin containing skills for the Crisp AI-enhanced Category Management Assessment process.

## Install

```bash
claude plugin install https://github.com/cheryloverholser-bot/Assessmentskills.git
```

## Skills

### `crisp-prompt-builder`

Adds a new AI prompt to the **Crisp Assessment AI Process Plan** HTML site's Prompt Library.

**Triggers when you say things like:**
- "Add a prompt for gap scoring to the assessment site"
- "Put this prompt in phase 2 of the library"
- "Create a new NOW prompt for phase 4"
- "Add this to the prompt library"

**What it does:**
1. Reads the HTML file to find the next available prompt ID
2. Generates a properly-structured accordion card (title, phase badge, input description, prompt text, copy button)
3. Inserts it into the correct phase section
4. Handles `NOW` (existing) vs `NEW` (newly designed) badge styling automatically
5. If you don't have final prompt text, it will draft one for you in the established style

**Target file:** `C:\Users\COverholser\Documents\Cantactix\Templates\Crisp-Assessment-AI-Process-Plan.html`

---

## Plugin structure

```
.claude-plugin/
  plugin.json          # Plugin manifest
skills/
  crisp-prompt-builder/
    SKILL.md           # Skill instructions
README.md
```
