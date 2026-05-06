---
name: crisp-search-indexer
description: >
  Builds or rebuilds the client-side search index for the Crisp Assessment HTML site.
  Use when the user enables the Search feature toggle, adds new content to the site,
  or says "update the search index", "rebuild search", or "search isn't finding my new content."
---

# Crisp Search Indexer

## TODO: Implement this skill

**What it should do:**
1. Read all page sections from the HTML (`id="page-overview"`, `id="page-phase1"` through
   `id="page-phase4"`, `id="page-prompts"`, `id="page-raci"`, `id="page-gates"`)
2. Extract searchable text from each section (page titles, activity text, AI step text,
   prompt titles and text, gate criteria)
3. Build a JavaScript search index object
4. Inject it into the HTML as a `const SEARCH_INDEX = [...]` in the `<script>` block
5. Wire up or update the `searchContent()` function to use it

**Target file:** `C:\Users\COverholser\Documents\Cantactix\Templates\Crisp-Assessment-AI-Process-Plan.html`

**Search index entry structure:**
```javascript
{
  id: "page-phase1",        // section to navigate to
  title: "Phase 1 — Intake",
  text: "full searchable text content...",
  tags: ["phase", "intake", "questionnaire"]
}
```

**Search UI elements (already in HTML):**
- `id="searchWrap"` — search bar container (hidden when feature off)
- `id="searchResults"` — results dropdown container
- Feature toggle: `features.search` in projectData

**Notes:**
- Search should be case-insensitive
- Results should show page title + a snippet of matching text
- Clicking a result should call `nav(id)` to navigate to that section
- Prompt text from `.prompt-text` elements is high-value search content
