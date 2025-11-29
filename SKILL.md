---
name: deliverable-tracking
description: Create GitHub Issues for client deliverables. Use when clarity phases have identified a deliverable need - the skill handles the HOW (issue creation in DaveX2001/deliverable-tracking) while clarity phases handle the WHAT (scope, criteria, context). Triggers on "create deliverable", "track this work", "log task for client".
---

# Deliverable Tracking Skill

## Overview

Creates GitHub Issues for client deliverables. This skill is invoked during the Execute phase after clarity phases have disambiguated the deliverable requirements.

**Context expectation:** The conversation already contains disambiguated information about:
- What the deliverable is
- Why it's important (business context)
- Success criteria / due date
- Any blockers

## Workflow

### Step 1: Extract from Clarity Context

Use sequential_thinking to extract deliverable information from the prior conversation:
- **Title:** Generate concise title from disambiguated requirements
- **What?** - Deliverable description (from requirements-clarity)
- **Why important?** - Business impact (from requirements-clarity)
- **Done = ?** - Success criteria and due date (from evaluation-clarity)
- **Blocked by?** - Dependencies (from requirements-clarity, default "-")

### Step 2: Fill Gaps (if any)

If any field cannot be extracted from conversation context, use AskUserQuestion to ask ONLY for missing fields. Most information should already be available from clarity phases.

### Step 3: Confirm Before Creating

Present summary:
```
Ready to create issue:

Title: [generated title]

## What?
[description]

## Why important?
[business context]

## Done = ?
- Criteria: [criteria]
- Due: [date]

## Blocked by
[blockers]

Proceed?
```

### Step 4: Create Issue

Run:
```bash
gh issue create \
  --repo DaveX2001/deliverable-tracking \
  --title "[title]" \
  --body "[formatted body]"
```

### Step 5: Confirm Success

Return the issue URL to user and confirm creation.

---

## Error Handling

- **Repo not found:** Inform user that `DaveX2001/deliverable-tracking` repo needs to exist
- **Auth failed:** Suggest running `gh auth login`
- **Missing context:** If clarity phases didn't provide enough info, ask for missing fields

---

## Limitations

- This skill CREATES new issues only
- Expects context from prior clarity phases
- Does NOT query existing issues (use `gh issue list` directly)
- Requires `gh` CLI authenticated with repo access
