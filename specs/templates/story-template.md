# User Story: [STORY TITLE]

**Story ID:** STORY-[EPIC-ID].[NUMBER]  
**Epic:** [EPIC NAME / EPIC ID]  
**Status:** [BACKLOG / READY / IN PROGRESS / IN REVIEW / DONE]  
**Created Date:** [DATE]  
**Last Updated:** [DATE]  
**Assignee:** [TEAM MEMBER NAME]  

---

## 1. Story ID and Title

<!-- Guidance: Use a hierarchical ID format that links the story to its parent Epic. This makes tracking and organization easier. Choose a descriptive title that summarizes what the user wants to accomplish. -->

**Story ID:** STORY-[EPIC-ID].[NUMBER]

**Title:** [STORY TITLE]

Example format: `STORY-AUTH.001: User can log in with email and password`

---

## 2. User Story

<!-- Guidance: Write the story from the user's perspective using the "As a, I want, so that" format. Focus on the user's need or goal, not the implementation. Keep it concise and clear. -->

**As a** [PERSONA],

**I want to** [ACTION],

**so that** [BENEFIT].

### Context

[OPTIONAL: Provide additional context or background information that helps understand the story better. What led to this story? What problem does it solve?]

---

## 3. Acceptance Criteria

<!-- Guidance: Define 3-5 specific, testable conditions that must be met for this story to be considered "done". Each criterion should be independently verifiable. Use Given/When/Then (Gherkin) format for complex scenarios. Avoid vague language like "works well," "easy," or "user-friendly." Be specific and measurable. -->

### Criterion 1

**Given** [INITIAL CONTEXT/PRECONDITION]  
**When** [USER ACTION]  
**Then** [EXPECTED OUTCOME]

### Criterion 2

**Given** [INITIAL CONTEXT/PRECONDITION]  
**When** [USER ACTION]  
**Then** [EXPECTED OUTCOME]

### Criterion 3

**Given** [INITIAL CONTEXT/PRECONDITION]  
**When** [USER ACTION]  
**Then** [EXPECTED OUTCOME]

### Criterion 4

**Given** [INITIAL CONTEXT/PRECONDITION]  
**When** [USER ACTION]  
**Then** [EXPECTED OUTCOME]

### Criterion 5 (if applicable)

**Given** [INITIAL CONTEXT/PRECONDITION]  
**When** [USER ACTION]  
**Then** [EXPECTED OUTCOME]

---

## 4. Technical Notes

<!-- Guidance: Add optional implementation details that help the development team. Include constraints, dependencies on other features/systems, edge cases to handle, performance considerations, or architectural notes. This is NOT requirements — it's helpful context. The team should still have freedom to decide HOW to implement. -->

### Constraints

- [CONSTRAINT, E.G., "Must work on mobile devices with iOS 12+"]
- [CONSTRAINT, E.G., "Must support browsers: Chrome, Firefox, Safari"]
- [CONSTRAINT, E.G., "Response time must be under 2 seconds"]

### Dependencies

- [ ] [DEPENDENCY, E.G., "Requires authentication system from STORY-AUTH.001"]
- [ ] [DEPENDENCY, E.G., "Depends on database schema update"]
- [ ] [DEPENDENCY, E.G., "Requires API endpoint from backend team"]

### Edge Cases & Error Handling

- [EDGE CASE, E.G., "What happens if the user's session expires?"]
- [EDGE CASE, E.G., "How do we handle network timeouts?"]
- [EDGE CASE, E.G., "What if the user enters invalid input?"]

### Implementation Notes (Optional)

[OPTIONAL: Add any technical suggestions, architectural patterns, or references to relevant documentation. Keep this brief — the team has the final say on implementation.]

---

## 5. Estimation

<!-- Guidance: Estimate the relative effort using story points or days. This story should be small enough to complete in 1-3 days of work. If it's larger, break it down into smaller stories. Include the rationale for your estimate. -->

### Effort Estimate

**Story Points:** [NUMBER] points  
**OR Estimated Days:** [NUMBER] days (1-3 days recommended)

### Estimation Rationale

[EXPLAIN YOUR ESTIMATION. CONSIDER:
- Complexity of the task
- Whether this story builds on existing features or is new functionality
- Dependencies that might affect work
- Unfamiliar technologies or domains
- Whether the team has done similar work before
]

### Complexity Level

[ ] Simple (Low risk, well-understood, straightforward) | [ ] Moderate (Some unknowns, moderate effort) | [ ] Complex (High risk, significant unknowns, requires spike/investigation)

---

## 6. INVEST Validation Checklist

<!-- Guidance: Use INVEST principles to validate that this is a well-formed story. Check each criterion before moving the story to "Ready for Development". If any criterion is not met, refine or split the story. -->

### ✓ Independent
- [ ] This story can be completed independently without blocking or being blocked by other stories
- [ ] The story doesn't depend on another story being done first (except documented dependencies in Technical Notes)
- [ ] This story could theoretically be done by a single team or person

**If not met:** Does this story need to be split? Should dependencies be clarified?

### ✓ Negotiable
- [ ] The story focuses on WHAT the user wants, not HOW to build it
- [ ] Implementation details are flexible and open to team discussion
- [ ] The acceptance criteria define the outcome, not the implementation approach
- [ ] There's room for the team to propose alternative solutions

**If not met:** Is the story too prescriptive? Can we remove implementation details and focus on user needs?

### ✓ Valuable
- [ ] This story delivers clear value to the user or business
- [ ] Completing this story moves us toward the Epic goal
- [ ] The user benefit is explicitly stated in the user story
- [ ] The story links back to a PRD goal or success metric

**If not met:** Why are we building this? What value does it create?

### ✓ Estimable
- [ ] The team has enough information to estimate the effort
- [ ] There are no major unknowns that would prevent estimation
- [ ] The story is clear enough that different team members would estimate similarly
- [ ] The story is small enough to estimate with confidence

**If not met:** Do we need to do a spike/investigation story first? Is the story too vague or too large?

### ✓ Small
- [ ] This story can be completed in 1-3 days of work by one developer
- [ ] The story is small enough to fit in a single sprint
- [ ] Completing this story won't delay other work significantly
- [ ] The story is not doing multiple things at once

**If not met:** Can we split this story into smaller stories?

### ✓ Testable
- [ ] Acceptance criteria are clear and objective — not subjective
- [ ] A QA team member could verify this story without clarification
- [ ] We can measure whether the acceptance criteria are met
- [ ] No criterion uses vague language like "works well," "is easy," or "looks good"

**If not met:** Do acceptance criteria need to be more specific and measurable?

### Summary

**Is this story INVEST-compliant?** [ ] YES | [ ] NO

If NO, what needs to be refined?
- [ ] Story needs to be split into smaller stories
- [ ] Story needs clearer acceptance criteria
- [ ] Dependencies need to be documented
- [ ] Story needs to focus more on user value
- [ ] Other: [DESCRIBE]

---

## Acceptance Criteria Verification

<!-- This section is used during testing/QA to verify the story meets all criteria -->

| Criterion | Pass | Notes |
|-----------|------|-------|
| Criterion 1 | [ ] | [QA notes] |
| Criterion 2 | [ ] | [QA notes] |
| Criterion 3 | [ ] | [QA notes] |
| Criterion 4 | [ ] | [QA notes] |
| Criterion 5 | [ ] | [QA notes] |

**Overall Status:** [ ] All criteria met (DONE) | [ ] Some criteria not met (NEEDS WORK)

---

## Common Mistakes to Avoid

### 1. **Vague Acceptance Criteria**
- ❌ Mistake: "The system should be easy to use"
- ✓ Fix: "A new user should complete the login flow in under 30 seconds without external help"

### 2. **Acceptance Criteria That Are Too Implementation-Focused**
- ❌ Mistake: "Build a REST API endpoint that returns JSON"
- ✓ Fix: "Users can view their account details without refreshing the page"

### 3. **Story That's Too Large**
- ❌ Mistake: Trying to fit an entire feature into one story
- ✓ Fix: Break it into smaller stories (e.g., "Add login", "Add password reset", "Add remember me")

### 4. **Missing Business Context**
- ❌ Mistake: "Fix the bug on the dashboard"
- ✓ Fix: "As a manager, I want to see accurate revenue totals on the dashboard so that I can monitor daily performance"

### 5. **Unclear Dependencies**
- ❌ Mistake: Stories that secretly depend on other stories but it's not documented
- ✓ Fix: Document all dependencies clearly in Technical Notes

### 6. **Not Estimable**
- ❌ Mistake: "Build user authentication system" (too vague and large)
- ✓ Fix: "Add email validation to the signup form" (specific and estimable)

### 7. **Subjective Success Criteria**
- ❌ Mistake: "The page should look beautiful" or "The error message should be helpful"
- ✓ Fix: "The error message should be under 100 characters and include how to fix the problem"

### 8. **Story Without Clear Value**
- ❌ Mistake: "Update the database schema for future use"
- ✓ Fix: "Optimize database queries to reduce page load time from 5s to 2s for user profile page"

### 9. **Forgetting Edge Cases**
- ❌ Mistake: Acceptance criteria only cover the "happy path"
- ✓ Fix: Include criteria for edge cases (invalid input, network errors, null values, etc.)

### 10. **Poor Story Title**
- ❌ Mistake: "Bug fix" or "Backend work"
- ✓ Fix: "Users can reset password via email link" or "Optimize product search query performance"

---

## Definition of Done Checklist

<!-- Use this to verify the story is truly complete before moving to Done -->

Before marking this story as DONE, verify:

- [ ] All acceptance criteria have been met and verified by QA
- [ ] Code has been peer reviewed and approved
- [ ] Tests have been written and are passing (unit, integration, or both)
- [ ] Documentation has been updated (if applicable)
- [ ] No new bugs or issues have been introduced
- [ ] Code follows team standards and conventions
- [ ] Story can be merged and deployed to production
- [ ] Deployment completed successfully (if applicable)
- [ ] Stakeholder sign-off obtained (if applicable)

---

## Related Documents & Links

- **Epic:** [LINK TO PARENT EPIC]
- **Related Stories:** [LINKS TO RELATED STORIES]
- **Design Doc/Mockup:** [LINKS TO DESIGN ASSETS]
- **Technical Doc:** [LINKS TO TECHNICAL DOCUMENTATION]
- **PR/Code Review:** [LINKS TO PULL REQUESTS]

---

## Discussion & Notes

<!-- Use this section for comments, decisions, and team discussions related to this story -->

**Key Decisions:**
- [DECISION AND DATE]
- [DECISION AND DATE]

**Questions/Clarifications:**
- [QUESTION AND ANSWER]
- [QUESTION AND ANSWER]

**Comment Thread:**
[ADD COMMENTS HERE AS THE STORY PROGRESSES]

