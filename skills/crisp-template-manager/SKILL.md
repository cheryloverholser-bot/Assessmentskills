---
name: crisp-template-manager
description: >
  Manages template links in the Crisp Assessment HTML site — adds, updates, or validates
  links to assessment template files. Use when the user wants to add a template link to a
  phase, update a template file name, check for broken links, or when they say "add a
  template to phase 3", "update the template link", or "what templates are linked."
---

# Crisp Template Manager

## TODO: Implement this skill

**What it should do:**
1. List all existing template links currently in the HTML
2. Add new template links to the correct phase's output section
3. Validate that referenced template files exist in the templates directory
4. Update file names if templates have been renamed

**Target file:** `C:\Users\COverholser\Documents\Cantactix\Templates\Crisp-Assessment-AI-Process-Plan.html`
**Templates directory:** `C:\Users\COverholser\Documents\Cantactix\Templates\Assessments Templates\`

**Template link structure:**
```html
<a class="tpl-link" href="[relative-path]">[icon] [filename]</a>
```

**Icon convention:**
- 📄 = Word documents (.docx)
- 📊 = Excel files (.xlsx)
- 📋 = PowerPoint files (.pptx)
- 🤖 = AI prompt links (navigate to prompt library)

**Known templates (as of v2.0):**
- Phase 1: CMS.QUESTIONNAIRE.docx, CX.ASSESSMENT.KICKOFF.2025.pptx
- Phase 2: Assessment Workshop Guide.pptx, CX.ASSESSMENT.WORKSHOPS.2025.pptx, CX.ASSESSMENT.ONSITE.QUESTIONS.xlsx
- Phase 3: OPPORTUNITY_LOG_Template.xlsx
- Phase 4: Assessment Solution Roadmap Template.pptx, Assessment_Executive_Summary.pptx

**Notes:**
- Template links live inside `.templates-wrap` divs in each phase's Output card
- Links to the prompt library use `onclick="nav('prompts')"` instead of `href`
