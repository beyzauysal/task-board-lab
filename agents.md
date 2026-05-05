# Task Board Lab - Project Conventions

This document defines the conventions and guidelines for the Task Board Lab project. All contributors, including AI assistants, should follow these conventions to maintain consistency and organization.

---

## 1. Project Overview

**Project Name:** Task Board Lab

**Purpose:** A personal task management application for solo developers to organize and track tasks across multiple projects.

**Target Users:** Solo developers and individual contributors managing 2-3 concurrent projects

**Scope:** Frontend-only, single-user application. No backend, no database, no authentication required.

---

## 2. Tech Stack

The Task Board Lab uses the following technology stack:

- **Framework:** React 18
- **Build Tool:** Vite
- **Language:** TypeScript
- **Styling:** [CSS/TailwindCSS/styled-components — specify as project grows]
- **State Management:** React Context + Hooks (or Redux if needed later)
- **Persistence:** localStorage (browser storage only)
- **Backend:** None (frontend-only application)
- **Database:** None (no persistence layer beyond localStorage)
- **Authentication:** None (single-user, no login required)
- **Hosting:** Static file hosting (Vercel, Netlify, or GitHub Pages)

---

## 3. Specification Structure

All specifications are organized in the `specs/` directory following this structure:

### Templates Directory (`specs/templates/`)

Contains reusable templates for creating new specifications:
- `prd-template.md` — Product Requirements Document template
- `epic-template.md` — Epic template for breaking down PRDs into large features
- `story-template.md` — User Story template following INVEST principles

### Generated Specifications

Generated specifications (actual PRDs, Epics, and Stories) are stored in their respective subdirectories:

- **PRDs:** `specs/prds/` — Generated Product Requirements Documents
- **Epics:** `specs/epics/` — Generated Epic specifications
- **Stories:** `specs/stories/` — Generated User Stories

### Prompt Files

GitHub Copilot prompt files are stored in the project root:
- `.github/prompts/` — AI assistant prompts and custom instructions

---

## 4. Naming Conventions

Follow these naming conventions for all files:

### General Rules

- **Required Prefixes:** Use the required uppercase prefixes exactly as defined for generated specification files: `PRD-`, `EPIC-`, and `STORY-`
- **Descriptive Segment Format:** Use kebab-case for the descriptive part after the required prefix
- **Prompt Files:** Use lowercase kebab-case and end with `.prompt.md`
- **Template Files:** Use lowercase kebab-case and end with `.md`
- **Avoid:** spaces, underscores, CamelCase in the descriptive segment, or special characters

### File Naming by Type

#### PRD Files
```
PRD-{feature-name}.md

Examples:
- PRD-task-management-core.md
- PRD-project-views.md
- PRD-task-filtering.md
```

#### Epic Files
```
EPIC-{number}-{name}.md

Examples:
- EPIC-001-user-authentication.md
- EPIC-002-task-management.md
- EPIC-003-project-organization.md
```

#### Story Files
```
STORY-{epic-number}.{story-number}-{name}.md

Examples:
- STORY-001.001-create-task-input-form.md
- STORY-001.002-save-task-to-storage.md
- STORY-002.001-display-task-list.md
```

#### Prompt Files
```
{description}.prompt.md

Examples:
- refine-user-stories.prompt.md
- create-epic-from-prd.prompt.md
```

---

## 5. AI Assistant Guidelines

All AI assistants working on this project should follow these guidelines:

### General Principles

1. **Use Templates:** Always use the appropriate template from `specs/templates/` when creating PRDs, Epics, or Stories.
2. **Avoid Generic Content:** Write specific, detailed specifications tailored to the Task Board Lab project. Avoid boilerplate text.
3. **Be Measurable:** Use specific metrics, numbers, and objective criteria instead of vague language like "easy," "fast," or "user-friendly."
4. **Use SMART Metrics:** In PRD and Epic success criteria, use SMART metrics (Specific, Measurable, Achievable, Relevant, Time-bound).
5. **Follow INVEST Principles:** When creating User Stories, ensure each story is Independent, Negotiable, Valuable, Estimable, Small, and Testable.
6. **Clear Scope:** Explicitly define "In Scope" and "Out of Scope" for every specification to prevent feature creep.

### Writing Requirements

- **Be Specific:** Instead of "Users should be able to create tasks," write "Users can create a task by entering a title and optional description, then clicking 'Save' or pressing Enter."
- **Include Edge Cases:** Document how the system handles errors, empty states, and unusual scenarios.
- **Link to Goals:** Every Epic should link to a PRD goal, and every Story should link to an Epic.
- **Avoid Implementation Details:** Focus on WHAT the system must do, not HOW to build it (except in Technical Notes).

### Frontend-Only Guidelines

- **No Backend Features:** Do not propose or create specifications for backend APIs, databases, authentication systems, or server-side features.
- **localStorage Only:** All data persistence should use browser localStorage or similar client-side storage.
- **UI/UX Focus:** Specifications should focus on user interface, user experience, and frontend functionality.
- **Single-User Assumption:** Do not include multi-user collaboration, sharing, or permission features.

---

## 6. File Organization Rules

### Do's

✓ Place all generated PRDs in `specs/prds/`  
✓ Place all generated Epics in `specs/epics/`  
✓ Place all generated Stories in `specs/stories/`  
✓ Place all prompt files in `.github/prompts/`  
✓ Use kebab-case for all file names  
✓ Include guidance comments in specifications  
✓ Keep specifications well-organized and easy to review  
✓ Link related documents (PRD → Epic → Story)  

### Don'ts

✗ Do not place generated specifications outside the `specs/` folder  
✗ Do not create backend-related files (APIs, database schemas, server configurations)  
✗ Do not add implementation code (React components, utility functions) unless explicitly requested by the user  
✗ Do not mix templates with generated specifications  
✗ Do not create duplicate files with similar names  
✗ Do not use spaces or special characters in file names  

---

## 7. Quality Checklist for Specifications

Before finalizing any specification, verify:

### PRD Quality

- [ ] All 7 sections are complete (Overview, Personas, Use Cases, Functional Requirements, Non-Functional Requirements, Success Metrics, Scope)
- [ ] Goals are specific and measurable
- [ ] Success metrics include SMART examples
- [ ] Scope clearly defines In Scope / Out of Scope
- [ ] No backend features are included
- [ ] All content is specific to Task Board Lab, not generic

### Epic Quality

- [ ] Epic delivers end-to-end user value
- [ ] Epic has clear boundaries
- [ ] Epic is linked to a PRD goal or success metric
- [ ] Epic can be broken into 4-8 user stories
- [ ] Sizing rationale is documented
- [ ] Dependencies are identified

### Story Quality

- [ ] Story follows "As a [persona], I want [action] so that [benefit]" format
- [ ] Story is estimable and can be completed in 1-3 days
- [ ] All acceptance criteria use Given/When/Then format
- [ ] Acceptance criteria are specific and testable (not subjective)
- [ ] INVEST principles are validated (all 6 criteria met)
- [ ] Story is independent and can be worked on separately

---

## 8. Project Metadata

**Repository:** Task Board Lab  
**Start Date:** May 5, 2026  
**Project Type:** Frontend React Application  
**Audience:** Solo developers and contributors  
**Status:** Active Development  

---

## 9. Questions for AI Assistants

When working on this project, AI assistants should consider:

1. **Does this follow the templates?** Is the output using the approved templates from `specs/templates/`?
2. **Is it specific to the project?** Does the specification make sense for a personal task board frontend app?
3. **Is the scope clear?** Can a developer understand exactly what to build and what not to build?
4. **Is it testable?** Can the specification be verified and tested objectively?
5. **Is it actionable?** Can a developer start working immediately without needing clarification?
6. **Is it organized?** Are files named correctly and stored in the right location?

---

## 10. Getting Help

If you're unsure about conventions or how to apply them:

- **Check the templates:** Review `specs/templates/` for examples
- **Review related documents:** Look at similar PRDs, Epics, or Stories already created
- **Follow the guidance comments:** Each template includes inline guidance comments
- **Reference this document:** This file documents all conventions and guidelines

---

**Last Updated:** May 5, 2026  
**Version:** 1.0  
**Maintained By:** Project Team
