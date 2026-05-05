# Module 02 Peer Review Notes

## 1. What I Built

For this lab, I used AI to build a full documentation workflow for the Task Board project.

I created:
- AI-generated templates for PRDs, Epics, and User Stories
- An AI-generated prompt library for producing project documents
- A generated PRD for the Personal Task Board
- Generated Epics derived from the PRD
- Generated User Stories derived from the most critical Epic
- A final validation pass to confirm consistency, scope, and completeness

## 2. My AI-Generated Templates

I created three reusable templates:
- **PRD template** for defining product goals, personas, use cases, requirements, metrics, and scope
- **Epic template** for breaking a PRD into larger feature areas with measurable outcomes
- **User Story template** for breaking Epics into small, testable development units

These templates help keep AI output structured, consistent, and easier to review. Instead of generating documents from scratch each time, the AI follows a repeatable format.

## 3. My AI-Generated Prompts

I created three reusable Copilot prompt files:
- **`generate-prd`** to turn a project brief into a complete PRD
- **`decompose-epics`** to turn a PRD into 3-4 well-scoped Epics
- **`decompose-stories`** to turn an Epic into 5-7 User Stories

These prompts are reusable in Copilot Chat and make the workflow repeatable for future projects, not just this one lab.

## 4. Full Flow

The full workflow was:
1. AI created the PRD, Epic, and User Story templates
2. AI created the reusable prompt files
3. I used the prompts to generate the PRD from the Task Board brief
4. I used the prompts again to generate Epics from the PRD
5. I used the prompts again to generate User Stories from the most important Epic
6. I validated the final output for completeness, structure, and scope alignment

## 5. One Refinement Example

During final validation, I found a naming convention inconsistency in `agents.md`.

The file originally said to use lowercase kebab-case for all file names, but it also required uppercase prefixes like `PRD-`, `EPIC-`, and `STORY-`.

I fixed this by clarifying the rule:
- Use uppercase prefixes exactly as required: `PRD-`, `EPIC-`, and `STORY-`
- Use kebab-case only for the descriptive part after the prefix

This made the naming convention consistent and easier for both humans and AI to follow.

## 6. What I Learned

From this lab, I learned:
- The hierarchy between **PRD → Epic → User Story**
- How **SMART success metrics** make PRDs more measurable and useful
- How **INVEST principles** improve User Story quality
- AI can create reusable tools and workflows, not just one-time answers
- Validation is important because AI-generated output can still need refinement

## 7. Questions for Peer Feedback

I would like feedback on these points:
- Is my PRD specific enough?
- Are my Epics clear and independently understandable?
- Are my User Stories small and testable?
- Are the prompts reusable for future projects?

## Short Closing Summary

My Module 02 lab output is not just a set of documents. It is a reusable AI-assisted workflow for generating structured product documentation, refining it, and validating it for future projects.
