# Adopt Global/Project Architecture for Hippocampus Document Organization

[[document-discovery]]

## Status
**Accepted** | Date: 2025-11-21

**Supersedes:** [[flat-structure-phantom-node-wikilinks]]

**Related ADRs:**
- [[hippocampus-first-document-workflow]] - Centralization principle
- [[explore-agent-hippocampus-document-discovery]] - Discovery mechanism
- [[obsidian-wikilinks-flat-structure]] - Relationship mechanism

## Context

**The Problem:**
- Three-folder structure (resources/, company/, clients/) requires ternary decision: "Which folder?"
- Folder names encode specific categories that may not fit all content types
- No clear rule for project-specific vs cross-project documentation
- Phantom node semantics unclear: What distinguishes topic-based vs entity-based grouping?

**Requirements:**
- Reduce decision space from three folders to binary choice
- Clear semantic distinction between phantom node types
- Auto-derivable structure when context is known (e.g., working in project directory)
- Maintain flat structure benefits within each tier
- Support both cross-project knowledge (patterns, ADRs) and project-specific documentation

## Decision

We will use **two-tier global/project architecture** where all new markdown files go to either `~/.claude/hippocampus/global/` (cross-project) or `~/.claude/hippocampus/project/{name}/` (project-specific), with context-aware phantom node linking.

**Key Principles:**

**Binary Decision Space:**
- Global: Content applicable across all projects (ADRs, patterns, business operations)
- Project: Content specific to one project or client engagement

**Context-Aware Phantom Nodes:**
- Global files: Link to topic-based phantom nodes (e.g., `[[docker-deployment]]`, `[[workshop-patterns]]`)
- Project files: Link to client-based phantom nodes (e.g., `[[client-avo]]`, `[[client-archibus]]`)

**Auto-Derivable Structure:**
- Project folder name derives from current working directory context
- Eliminates naming decision: `project/{cwd-basename}/`

**Relationship Discovery:**
- Explore agent finds files by content and filename (discovery layer)
- Wikilinks enable human graph visualization (relationship layer)
- Phantom nodes provide logical grouping without folder hierarchy overhead

## Consequences

### ✅ Positive

**Simplified Decision Space:**
- Binary choice (global vs project) vs ternary choice (resources/company/clients)
- Clear semantic boundary: "Is this reusable or project-specific?"
- Eliminates ambiguous cases where content could fit multiple categories

**Semantic Phantom Node Distinction:**
- Global `[[topic]]` = conceptual grouping (technical patterns, business operations)
- Project `[[client]]` = entity grouping (client engagements, deliverables)
- Phantom node name immediately signals content context

**Context-Aware Automation:**
- Working in project directory → Project folder auto-derived from path
- Clear when creating global content (ADR, pattern) vs project content (workshop notes)
- Reduces cognitive load: fewer manual naming decisions

**Multi-Project Per Client:**
- Handles multiple projects for same client naturally
- Example: `project/avo-backend/`, `project/avo-frontend/` both link to `[[client-avo]]`
- Phantom node preserves client relationship across projects

**Preserves Discovery Benefits:**
- Explore agent works identically (searches by content/filename)
- Flat structure within each tier (global/ and project/{name}/)
- Wikilinks provide human graph visualization via Obsidian

### ❌ Negative

**Loss of Resources/Company Distinction:**
- Previous structure separated technical (resources/) from business (company/)
- Now both in global/, distinction only via phantom nodes
- Trade-off: Simpler structure vs explicit categorization

**Project Folder Proliferation:**
- Each project gets own folder under project/
- Many folders vs single flat namespace
- Mitigated by: Flat structure within each project folder

### ⚪ Neutral

**Supersedes Earlier Flat Structure:**
- Replaces single flat clients/ folder with project/{name}/ pattern
- Core decisions preserved (phantom nodes, wikilinks, no hub files)
- Evolutionary refinement rather than architectural shift

**Phantom Node Governance Still Needed:**
- Search-and-reuse pattern for both topic and client phantom nodes
- Obsidian auto-update works for renaming (when done in Obsidian)
- Consistency mechanism separate from architectural decision

## Alternatives Considered

| Alternative | Rejection Reason |
|-------------|------------------|
| **Three-folder structure (resources/, company/, clients/)** | Ternary decision creates cognitive overhead. Categories don't cleanly separate: where do client-facing technical patterns go? Resources or company? Ambiguity defeats purpose of categorization. |
| **Single flat structure (no subfolders)** | Works for 80 files, doesn't scale to hundreds. Mixing global patterns with project-specific documents loses semantic signal. No way to distinguish "applicable everywhere" from "specific to this client." |
| **Project-based top-level (project/ only, no global/)** | Forces duplication of cross-project patterns per project. Violates DRY principle. ADRs and patterns would fragment across project folders, defeating centralized knowledge base purpose. |
| **Folder per client (client-avo/, client-archibus/)** | Doesn't handle multi-project per client. Conflates client (entity) with project (engagement). Global patterns still need separate location, reintroducing categorization problem. |
| **Deep hierarchy (global/technical/, global/business/, project/client/repo/)** | Violates flat structure benefits. Path-based navigation returns. Folder hierarchy decisions multiply. Contradicts zero-maintenance philosophy and Explore agent discovery model. |

---

**Key Resources:**
- [[hippocampus-first-document-workflow]] - All markdown → hippocampus principle
- [[explore-agent-hippocampus-document-discovery]] - Discovery mechanism (unchanged)
- [[obsidian-wikilinks-flat-structure]] - Wikilinks for relationships
- [[flat-structure-phantom-node-wikilinks]] - Superseded predecessor (single flat structure)
- Empirical Testing (2025-11-20): Phantom node governance via Obsidian auto-update
