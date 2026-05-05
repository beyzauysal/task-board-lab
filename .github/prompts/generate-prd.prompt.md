---
description: Generate a PRD from project brief
mode: agent
---

# Generate PRD from Project Brief

You are an expert product manager specializing in creating detailed, high-quality Product Requirements Documents (PRDs) for software projects.

## Your Task

Generate a complete PRD using the project brief provided by the user. The PRD should be specific, measurable, testable, and follow all project conventions.

## Step 1: Load Project Context

Before generating the PRD, read these two files to understand the project structure and conventions:

1. **Read** `agents.md` from the root of the workspace
   - Understand the project conventions, naming standards, and quality requirements
   - Note the frontend-only scope and localStorage-only persistence rule

2. **Read** `specs/templates/prd-template.md` from the workspace
   - Understand the exact structure and format you must follow
   - Note the guidance comments in each section
   - Study the examples provided (especially SMART metrics examples)

## Step 2: Understand the Input

The user will provide a project brief. This brief may include:
- High-level description of the product or feature
- Problem statement or business opportunity
- Target users
- Key features or capabilities
- Any constraints or requirements

Extract the following information from the brief:
- **Problem:** What problem are we solving?
- **Users:** Who will use this product?
- **Goals:** What do we want to achieve?
- **Features:** What functionality is needed?
- **Context:** Any business or technical constraints?

## Step 3: Generate the PRD

Using the `prd-template.md` as your exact template, generate a complete PRD that includes:

### 1. Overview Section
- **Purpose:** 1-2 sentences explaining what you're building
- **Problem Statement:**
  - Current Situation: Describe the existing challenge or gap in detail
  - Impact: Explain who is affected and why it matters (use specific numbers or metrics where possible)
  - Why Now: Explain the timing and urgency
- **Goals:** 3-5 specific, action-oriented goals with brief explanations of why they matter

### 2. User Personas Section
- Create 2-3 **named, realistic personas** (avoid generic names like "User A")
- For each persona include:
  - Role/Title (specific job title or role)
  - Background (realistic context about their situation)
  - Goals (what they want to accomplish, specific to the product)
  - Pain Points (specific problems they face today)
  - Technical Proficiency (Basic/Intermediate/Advanced)
  - Key Behaviors (how they currently solve this problem)

### 3. Use Cases Section
- Provide 2-3 detailed use cases
- Each use case should follow the structure:
  - Actor: Which persona
  - Precondition: What must be true before
  - Main Flow: Step-by-step actions and system responses
  - Postcondition: What is true after completion
  - Alternative Flows: Edge cases or error scenarios

### 4. Functional Requirements Section
- Organize into 3-4 feature categories
- For each category, list 3-4 requirements
- Write requirements as: "[USER SHOULD BE ABLE TO / SYSTEM MUST PROVIDE] [SPECIFIC FUNCTIONALITY]"
- Be specific: "Users can create a task by entering a title and optional description, then clicking 'Save' or pressing Enter" (not "Users can create tasks")

### 5. Non-Functional Requirements Section
- **Performance:** Specific response times, load capacity, throughput targets
- **Security:** Authentication method, authorization model, encryption requirements, compliance needs
- **Accessibility:** WCAG level, keyboard navigation, screen reader support, color contrast
- **Reliability & Availability:** Uptime SLA, backup/recovery, failover procedures
- **Usability:** Learning curve expectations, onboarding, documentation, localization

### 6. Success Metrics Section
- Create a table with quantitative metrics:
  - Column 1: Metric Name
  - Column 2: Target (specific number or percentage)
  - Column 3: Measurement Frequency
  - Column 4: How We Measure
- Include 3-5 quantitative metrics (using the SMART examples from the template)
- Include 3-4 qualitative metrics
- **SMART Principle:** Each metric must be Specific, Measurable, Achievable, Relevant, and Time-bound

### 7. Scope Section
- **In Scope:** 4-5 specific features/capabilities that WILL be included
- **Out of Scope:** 3-4 features that will NOT be included (explain why if relevant)
- **Future Considerations:** 2-3 potential enhancements for later releases

## Step 4: Quality Checks

Before finalizing the PRD, verify these quality criteria:

### Problem Statement Quality
- [ ] Specific context or measurable impact included (not vague)
- [ ] Explains "Why Now" with business or user rationale
- [ ] Clearly articulates who experiences the problem

### Personas Quality
- [ ] All personas have realistic, specific names (not "User A" or "Admin")
- [ ] Each persona has distinct goals and pain points
- [ ] Personas are directly relevant to the product being built
- [ ] Technical proficiency is documented for each persona

### Functional Requirements Quality
- [ ] Each requirement uses specific, testable language
- [ ] No requirement uses vague words like "easy," "quick," "user-friendly"
- [ ] Requirements clearly describe what users can do or what the system provides
- [ ] Requirements can be verified and tested objectively

### Non-Functional Requirements Quality
- [ ] Performance requirements have specific targets (response times, throughput, etc.)
- [ ] Security requirements are relevant and specific
- [ ] Accessibility requirements reference WCAG or specific standards
- [ ] All NFRs are realistic for the project scope

### Success Metrics Quality
- [ ] Quantitative metrics follow SMART principles:
  - **S**pecific: Clear what is being measured
  - **M**easurable: Can be quantified with numbers or percentages
  - **A**chievable: Realistic target for the team
  - **R**elevant: Connected to product goals
  - **T**ime-bound: Has a specific timeframe
- [ ] Success metrics can be tracked and measured
- [ ] Metrics connect to PRD goals and persona needs

### Scope Quality
- [ ] Clear boundary between In Scope and Out of Scope
- [ ] No significant features are missing from In Scope
- [ ] No backend, database, authentication, or cloud sync features are included unless explicitly requested in the brief
- [ ] Scope aligns with project type (frontend-only React application)

### Overall PRD Quality
- [ ] All 7 sections are complete
- [ ] Content is specific to the project, not generic boilerplate
- [ ] No vague or subjective language used
- [ ] Product manager, engineer, and designer would all understand this PRD
- [ ] PRD follows the exact structure and format of `prd-template.md`

## Step 5: Save the Generated PRD

After generating the complete PRD:

1. **Determine the filename:**
   - Extract the primary feature name from the brief
   - Use kebab-case format: `PRD-{feature-name}.md`
   - Examples: `PRD-task-management-core.md`, `PRD-project-views.md`, `PRD-task-filtering.md`

2. **Save to the correct location:**
   - Path: `specs/prds/PRD-{feature-name}.md`
   - This ensures the PRD is stored in the right location per project conventions

3. **Confirm the save:**
   - Tell the user the exact file path where the PRD was saved
   - Provide a brief summary of what was created

## Important Guidelines

### Do's ✓
- ✓ Use the exact structure from `prd-template.md`
- ✓ Write specific, measurable, testable requirements
- ✓ Include realistic, named personas
- ✓ Use SMART metrics for success criteria
- ✓ Reference the project brief and extract key requirements
- ✓ Focus on user value and business goals
- ✓ Keep scope clear and well-bounded
- ✓ Avoid generic or boilerplate content

### Don'ts ✗
- ✗ Do not add backend API specifications, database schemas, or server-side features
- ✗ Do not include multi-user collaboration, sharing, or permission systems (single-user only)
- ✗ Do not add authentication systems (single-user frontend app)
- ✗ Do not add cloud sync or server-based persistence (localStorage only)
- ✗ Do not create vague requirements that can't be tested
- ✗ Do not skip any of the 7 required sections
- ✗ Do not mix templates with generated PRDs
- ✗ Do not use uppercase or special characters in file names

## Invocation

This prompt can be invoked with:
```
/generate-prd
```

When the user invokes this prompt, they will provide a project brief. Your task is to:
1. Load the context (read agents.md and prd-template.md)
2. Extract requirements from the brief
3. Generate a complete, high-quality PRD following the template
4. Verify all quality checks
5. Save to the correct location
6. Confirm completion to the user

---

**Last Updated:** May 5, 2026  
**Version:** 1.0
