# Hippocampus Skill Draft

## Frontmatter

```yaml
---
name: hippocampus
description: Use for ALL markdown documentation - finding, creating, or editing.
  No markdown files should be created outside hippocampus.
  Searches centralized knowledge base at ~/.claude/hippocampus/.
  For discovery, returns existing content. For create/edit, guides
  tier selection and phantom node linking.
---
```

## Instructions

# Hippocampus Knowledge Base

## Core Rule
**ALL markdown → hippocampus. No exceptions.**
- Never create .md files in project directories
- Never create .md files in /tmp or elsewhere
- Everything goes to ~/.claude/hippocampus/ (global or project tier)

## Determine Intent
- **Finding resource?** → Discovery path
- **Creating/editing?** → Create/Edit path

---

## Discovery Path

1. Use Task tool with `subagent_type=Explore` to search hippocampus
   - Path: `~/.claude/hippocampus/`
   - Search query based on user's request
2. Return relevant content to user

---

## Create/Edit Path

### Step 1: Search First
- Use Task tool with `subagent_type=Explore` to search hippocampus
- Path: `~/.claude/hippocampus/`
- Check if similar content already exists
- **If found:** Ask user → edit existing or create new?
- **If not found:** Continue to Step 2

### Step 2: Tier Selection
AskUserQuestion with options:
- **Global** (`~/.claude/hippocampus/global/`): Cross-project (ADRs, patterns, business ops)
- **Project** (`~/.claude/hippocampus/project/{name}/`): Client-specific content

### Step 3: Phantom Node Selection
- Use Explore agent to search for existing phantom nodes in hippocampus
- Present found options to user via AskUserQuestion
- User picks existing or creates new `[[phantom-node]]`

### Step 4: Create File
- Path: `~/.claude/hippocampus/{tier}/filename.md`
- Include selected phantom node wikilink in file
- Use descriptive filename (no prefixes needed)

### Step 5: Git Commit
- Commit changes with descriptive message
- Git tracks all document evolution

---

## Protocol (CLAUDE.md) - Ultra-minimal

```xml
<hippocampus_markdown_protocol>
Hippocampus = centralized markdown knowledge base at ~/.claude/hippocampus/
Git-tracked, cross-system portable.
ALL markdown documentation lives here. No exceptions.
</hippocampus_markdown_protocol>
```
