# Memory Banks - Task Board Lab

## Purpose

This memory bank provides persistent project context for AI assistants working on the Task Board Lab project.

The purpose of these files is to help AI assistants understand the project before generating code, documentation, tests, or development suggestions.

Instead of explaining the project from the beginning in every AI conversation, this memory bank stores the most important project knowledge in a structured and reusable way.

## Why This Memory Bank Exists

AI assistants often generate generic output when they do not have enough project context.

Without memory banks, an AI assistant may:
- Use the wrong technology stack
- Ignore the existing project structure
- Create files in the wrong folders
- Use inconsistent naming conventions
- Misunderstand project-specific terms
- Skip validation or testing expectations
- Generate code that does not match the PRD, Epics, User Stories, or Agents.MD

With memory banks, an AI assistant should:
- Understand the project architecture
- Follow the existing coding standards
- Use the correct domain terminology
- Respect project-specific business rules
- Generate code that is easier to review and maintain
- Reduce the amount of manual correction needed

## Structure

### architecture/

This folder contains system architecture information.

It explains:
- The application structure
- The technology stack
- Main components and responsibilities
- Data flow
- Deployment approach
- Important architectural decisions

Main file:
- [Architecture Overview](architecture/overview.md)

AI assistants should use this file when they need to understand how the project is designed technically.

### conventions/

This folder contains coding standards and development rules.

It explains:
- Naming conventions
- File and folder organization
- Code organization rules
- Testing expectations
- Error handling rules
- Quality criteria

Main file:
- [Coding Standards](conventions/coding-standards.md)

AI assistants should use this file when generating, editing, or reviewing code.

### domain/

This folder contains project-specific terminology and business rules.

It explains:
- Important domain terms
- User personas
- Business rules
- Task board concepts
- Status and workflow rules

Main file:
- [Domain Glossary](domain/glossary.md)

AI assistants should use this file when they need to understand the meaning of project-specific concepts.

### workflows/

This folder contains the development workflow for the project.

It explains:
- Development process
- Branching strategy
- Pull request process
- Code review checklist
- Testing process
- Deployment and rollback approach

Main file:
- [Development Workflow](workflows/development-process.md)

AI assistants should use this file when helping with implementation planning, review, testing, or deployment.

### roles/

This folder is reserved for role-specific memory bank files.

Possible future files:
- developer.md
- qa.md
- pm.md

These files can provide different context for developers, QA engineers, and product managers.

## Quick Navigation

- [Architecture Overview](architecture/overview.md)
- [Coding Standards](conventions/coding-standards.md)
- [Domain Glossary](domain/glossary.md)
- [Development Workflow](workflows/development-process.md)

## How to Use

When asking an AI assistant to generate project-related output, reference the relevant memory bank files.

For code generation, use:
- `architecture/overview.md`
- `conventions/coding-standards.md`
- `domain/glossary.md`

For process or planning tasks, use:
- `workflows/development-process.md`

For project terminology and business rules, use:
- `domain/glossary.md`

For architecture decisions and technical structure, use:
- `architecture/overview.md`

## Source Materials

This memory bank is based on:
- Module 02 PRD
- Module 02 Epics
- Module 02 User Stories
- Agents.MD
- Existing project files
- Module 03 lab requirements

## Maintenance

This memory bank should be updated when:
- The project architecture changes
- New features are added
- Coding standards change
- Domain rules change
- Development workflow changes
- AI output repeatedly makes the same mistake

These files should be stored in version control together with the project code.

## Version

**Last Updated:** May 6, 2026  
**Version:** 1.0