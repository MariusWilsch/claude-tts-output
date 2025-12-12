# Shutdown Ritual (Evening Selection Ceremony)

## Purpose

**Pure selection** for tomorrow's maker work and psychological closure on the workday.

This ritual separates **planning** (manager mode) from **execution** (maker mode). By selecting tasks the evening before, you wake up ready to execute without decision overhead.

Grooming already handled: assignee, blocked/ready, maker/manager classification. You just select.

## When

After dinner, before ending the workday.

## Prerequisites

- Grooming has classified items (maker/manager labels applied)
- Physical book/notebook ready

## The Ceremony (5-10 minutes)

### Step 1: Query Maker Items

Pull your actionable maker items from To-Do:

```bash
# Fetch To-Do + Maker items (excluding blocked and sub-issues)
gh api graphql -f query='{
  repository(owner: "DaveX2001", name: "deliverable-tracking") {
    issues(first: 50, states: OPEN, filterBy: {assignee: "MariusWilsch"}) {
      nodes {
        number
        title
        labels(first: 10) { nodes { name } }
        parent { number }
      }
    }
  }
}' --jq '.data.repository.issues.nodes[]
  | select(.parent == null)
  | select(.labels.nodes | map(.name) | any(. == "to-do"))
  | select(.labels.nodes | map(.name) | any(. == "maker"))
  | select(.labels.nodes | map(.name) | all(. != "blocked"))
  | "#\(.number): \(.title)"'
```

**Note:** This query returns only items that are:
- Assigned to you
- Labeled `to-do` (groomed and ready)
- Labeled `maker` (half-day deep work)
- NOT labeled `blocked`
- NOT sub-issues (parent issues only)

### Step 2: Select 3

From the list, choose maximum 3 items for tomorrow.

**Selection criteria:**
- What has the highest stakes/urgency?
- What am I most prepared for?
- What moves the needle most?

Realistically, 1-2 items get done per day. 3 is the max.

### Step 3: Write in Book

Write the selected issue numbers in your physical notebook.

This is your **maker queue** for tomorrow.

### Step 4: Done

Board is now closed until tomorrow's manager time.

Tomorrow's maker queue is set. Shutdown complete.

## The Next Morning

1. Open physical book
2. Pick first issue number
3. If context needed: `gh issue view #number` (terminal, not browser)
4. Work. Board stays **CLOSED**.
5. When done → pick next from book OR stop

## Rules

1. **Book = only maker tasks** (half-day items)
2. **Board = closed during maker time** (no exceptions)
3. **Single issue = okay** (via CLI or direct URL, never through board)
4. **Max 3 items in book** (realistic daily capacity)

## What This Ritual Does NOT Do

| ❌ Not in Ritual | ✅ Where It Happens |
|-----------------|---------------------|
| Blocked scan | Grooming (daily with David) |
| Maker/Manager classification | Grooming (daily with David) |
| Assignee verification | Grooming (daily with David) |
| Context clarification | Grooming (daily with David) |

The ritual is **pure selection** - grooming handles everything else.

## Related

- [GROOMING.md](./GROOMING.md) - Daily sync that classifies items (Definition of Ready)
- [Personal Kanban 101](https://www.personalkanban.com/personal-kanban-101/) - Background concepts
