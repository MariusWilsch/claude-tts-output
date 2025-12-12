# Daily Sync Grooming Guide

## Purpose

**Grooming = Data Quality Gate.**

Ensure every item has: correct assignee, blocked/ready status, maker/manager classification, and clear context.

Marius selects tomorrow's work in the Evening Shutdown Ritual (pure selection from pre-classified items).

---

## Step 0: Blocked Scan (5-10 minutes)

Review **ALL blocked items** (not just yours) - this is manager oversight.

```bash
# Fetch all blocked issues
gh issue list --repo DaveX2001/deliverable-tracking --label "blocked" --state open --json number,title,assignees
```

For each blocked issue:

1. **Ask:** "Is this still blocked, or can it proceed?"

**If still blocked:**
1. Ensure assignee is correct (blocked items need owners too)
2. Add a concise comment explaining why (e.g., "Blocked by #114" or "Waiting for client response")
3. Then next.

**If unblocked:** Continue with routing:
1. Remove `blocked` label
2. Ensure assignee is correct
3. Apply maker/manager label (Q4 below)
4. Move to To-Do (passed Definition of Ready)

---

## The Four Questions (For Each Backlog Item)

### Q1: "Is the Assignee correct?"

David assigns when creating. In grooming: confirm or change.

- **Marius** - Client work, decisions
- **David** - Internal, automation, design
- **Intern** - Delegatable tasks

### Q2: "Blocked or Ready?"

> "Can this be started without asking anyone or waiting for anything?"

| Answer | Action |
|--------|--------|
| **NO** | Add `blocked` label + comment "Needs: [what's missing]" |
| **YES** | Continue to Q3 and Q4 |

### Q3: "Any questions or unclear context?"

Resolve ambiguities:
- Task description accurate?
- Definition of Done clear?
- Missing information?

### Q4: "Maker or Manager?"

> "Can Marius spend half a day on this AND does he have all context to execute?"

| Criteria | Maker (YES) | Manager (NO) |
|----------|-------------|--------------|
| Duration | Half-day / multi-hour | 15-min quick task |
| Type | Coding, building, research | Email, review, admin |
| Context | Complete, ready to go | Needs more info |
| Focus | Single project | Multiple projects |

**Action:** Add `maker` or `manager` label based on answer.

---

## Definition of Ready (Move to To-Do)

An item moves from Backlog to To-Do when ALL are true:
- [ ] Assignee is correct
- [ ] Not blocked
- [ ] Has `maker` or `manager` label
- [ ] Context is clear

---

## Flow

```
Backlog (inbox)
    ↓
GROOMING (daily with David)
├── Blocked scan (route unblocked items)
├── Q1: Assignee correct?
├── Q2: Blocked or ready?
├── Q3: Context clear?
└── Q4: Maker or manager?
    ↓
To-Do (groomed, ready for selection)
    ↓
Evening Shutdown Ritual (Marius selects 3 for book)
```

---

## Daily Sync Format

**Step 0:** Blocked scan (all blocked items, 5-10 min)

**Per Backlog item (oldest first):**

```
1. Assignee correct? (Marius/David/Intern)
2. Blocked or ready?
   → NO: Add blocked label + comment
   → YES: Continue
3. Context clear? Questions?
4. Maker or manager?
   → Add label

If all YES → Move to To-Do
```

**(15-min max per item)**

**Skip:** Items already in To-Do (just quick status check if needed)

---

## Roles

| Role | Responsibility |
|------|----------------|
| **Marius** | Executes, selects in evening ritual |
| **David** | Creates issues (with assignee), grooms, async updates |

---

## Principles

1. **Grooming = Data Quality** - Every item gets classified
2. **Always Assign First** - Every item needs an owner
3. **15-Minute Time-Box** - No clarity? Add blocker comment and move on
4. **To-Do = Groomed** - Only items passing Definition of Ready enter To-Do
