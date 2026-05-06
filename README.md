# Assessment Skills — Crisp Claude Plugin

A Claude Code plugin containing skills for the Crisp AI-enhanced Category Management Assessment process.

## Install

```bash
claude plugin install https://github.com/cheryloverholser-bot/Assessmentskills.git
```

## Skills

| Skill | Status | What it does |
|---|---|---|
| `crisp-prompt-builder` | ✅ Ready | Add a new AI prompt to the Prompt Library in the assessment site |
| `crisp-engagement-setup` | 🔲 Scaffold | Configure the site for a new client engagement |
| `crisp-phase-generator` | 🔲 Scaffold | Generate or update a phase page (inputs, activities, AI steps, RACI, gate) |
| `crisp-raci-sync` | 🔲 Scaffold | Update RACI assignments across phase pages and reference table |
| `crisp-template-manager` | 🔲 Scaffold | Add, update, or validate template file links in the site |
| `crisp-search-indexer` | 🔲 Scaffold | Build the client-side search index when new content is added |
| `crisp-progress-reporter` | 🔲 Scaffold | Report build status against the implementation plan |
| `crisp-engagement-generator` | 🔲 Scaffold | Spin up a complete folder + HTML copy for a new client engagement |

---

## Skill details

### `crisp-prompt-builder` ✅
Adds a new AI prompt accordion card to the HTML site's Prompt Library.
- Triggers: "add a prompt for X", "put this prompt in phase 2", "add this to the library"
- Handles ID sequencing, badge styling (NOW/NEW), copy button wiring
- Drafts prompt text in the established style if you don't have it yet

### `crisp-engagement-setup` 🔲
Pre-configures the HTML site for a specific client and engagement lead.
- Triggers: "set up a new engagement", "configure the site for [client]"

### `crisp-phase-generator` 🔲
Generates or updates a full phase page using the standard 3-column layout.
- Triggers: "build phase 2", "add an activity to phase 3", "update the gate for phase 1"

### `crisp-raci-sync` 🔲
Keeps RACI assignments consistent across all 7 places they appear in the site.
- Triggers: "update the RACI", "change who's responsible for phase 2"

### `crisp-template-manager` 🔲
Manages template links — adds, updates, and validates links to assessment files.
- Triggers: "add a template to phase 3", "update the template link", "what templates are linked"

### `crisp-search-indexer` 🔲
Builds the JavaScript search index from all page content.
- Triggers: "rebuild search", "search isn't finding my new content"

### `crisp-progress-reporter` 🔲
Checks the HTML against the implementation plan and reports what's done vs. remaining.
- Triggers: "what's left to build", "how far along is the site"

### `crisp-engagement-generator` 🔲
Creates a complete new client engagement folder with a pre-configured HTML copy and all templates.
- Triggers: "create an engagement for [client]", "spin up a new assessment for [client name]"

---

## Plugin structure

```
.claude-plugin/
  plugin.json
skills/
  crisp-prompt-builder/       ✅ SKILL.md
  crisp-engagement-setup/     🔲 SKILL.md (scaffold)
  crisp-phase-generator/      🔲 SKILL.md (scaffold)
  crisp-raci-sync/            🔲 SKILL.md (scaffold)
  crisp-template-manager/     🔲 SKILL.md (scaffold)
  crisp-search-indexer/       🔲 SKILL.md (scaffold)
  crisp-progress-reporter/    🔲 SKILL.md (scaffold)
  crisp-engagement-generator/ 🔲 SKILL.md (scaffold)
README.md
```
