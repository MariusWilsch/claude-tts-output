# ADR-002: Adopt Hippocampus-First Document Workflow

## Status
**Accepted** | Date: 2025-11-18

## Context

**The Problem:**
- Risk of creating duplicate documents across project repositories and hippocampus
- Uncertainty about where new markdown documentation should be created
- No clear workflow for document lifecycle (creation → editing → version control)
- Manual copying between locations creates maintenance burden and version drift
- Need to establish single source of truth while maintaining Git version control

**The Insight:**
If hippocampus is the centralized knowledge base for AI-accessible documentation, creating documents elsewhere then copying creates the exact fragmentation problem hippocampus was designed to solve. Working directly in hippocampus with Git version control provides both single-source-of-truth and full revision history.

**Requirements:**
- Prevent duplicate documents across repositories
- Establish clear "where do I create this?" workflow
- Maintain Git version control for all document evolution
- Enable Explore agent discovery for all documentation
- Support cross-system portability (hippocampus travels with Claude config)
- No "done vs temporary" distinction (documents evolve continuously)

## Decision

We will create **all new markdown documents directly in ~/.claude/hippocampus/** with Git version control, using Explore agent search before creation to prevent duplicates.

**Workflow Pattern:**
1. **Before creating:** Search hippocampus via Explore agent ("Does doc about [topic] exist?")
2. **Not found:** Create new document in `~/.claude/hippocampus/[descriptive-filename].md`
3. **Found:** Edit existing document (Git tracks evolution)
4. **Commit:** Git commit changes with descriptive message

**Implementation Specifics:**
- All new `.md` files created in `~/.claude/hippocampus/` (no subdirectories, flat structure)
- Path-prefixed filenames for origin context (e.g., `soloforce-client-X-proposal.md`)
- Explore agent pre-creation search prevents duplicates
- Git tracks continuous document evolution (no "finalized" state)
- Cross-system sync via Git (hippocampus repository)

**Transition Approach:**
- Existing project documentation remains in place for now
- New documents go to hippocampus immediately
- Migration of existing docs happens organically over time
- Test-and-learn: iterate workflow based on real friction

## Consequences

### ✅ Positive

**Single Source of Truth:**
- No manual copying between project repos and hippocampus
- No version drift (editing happens in one location)
- Git history provides complete revision tracking
- Eliminates "which version is current?" confusion

**Duplicate Prevention:**
- Explore agent search before creation surfaces existing docs
- Flat structure + descriptive filenames make duplicates obvious
- Git prevents silent overwrites (you'll see file exists)
- Natural discovery mechanism (search finds related content)

**Simplified Workflow:**
- Clear decision rule: "New doc? → Hippocampus"
- No "where should this live?" decision paralysis
- No post-creation copying workflow
- AI agents know where to create documentation

**Cross-System Portability:**
- Git-tracked hippocampus travels with Claude config
- Fresh installations get full knowledge base via clone
- No per-project documentation setup needed
- Consistent discovery mechanism across all systems

**Continuous Evolution:**
- No "done vs temporary" mental overhead
- Git tracks all changes (nothing is ever "final")
- Documents improve incrementally over time
- Version control enables rollback if needed

### ❌ Negative

**Transition Friction:**
- Existing project docs remain in original locations
- Temporary duplication during transition period
- Need to remember "new = hippocampus, old = in place"
- Migration effort spread over time vs. one-time bulk move

**Search Dependency:**
- Duplicate prevention relies on Explore agent search working
- If search fails, might create duplicates unknowingly
- Requires discipline: "search before create"
- No automatic enforcement mechanism

**Project-Specific Context Loss:**
- Project repos no longer contain their own documentation
- External contributors might not know about hippocampus
- Requires hippocampus access for full context
- May need README linking to hippocampus docs

### ⚪ Neutral

**Test-and-Learn Approach:**
- Workflow will iterate based on real friction encountered
- Not all edge cases anticipated upfront
- May discover need for subdirectories or categorization
- Flexibility to adjust as usage patterns emerge

**Path Prefix Convention:**
- `soloforce-client-X.md`, `velox-pattern-Y.md` for origin tracking
- Helpful but not enforced
- Flat structure may need evolution at scale
- Alternative: subdirectories if flat becomes unwieldy

## Alternatives Considered

| Alternative | Rejection Reason |
|-------------|------------------|
| **Create in projects, copy to hippocampus** | Manual copying creates version drift, maintenance burden, and "which is current?" confusion. Violates single-source-of-truth principle. Exact problem hippocampus was designed to eliminate. |
| **Symlinks from projects to hippocampus** | Cross-platform symlink support varies (Windows complications). Git doesn't track symlink targets well. Adds complexity without solving core workflow question: "where do I create new docs?" |
| **Dual-purpose (project-specific in repos, cross-project in hippocampus)** | Requires decision rule for categorization: "Is this project-specific or cross-project?" Creates cognitive overhead and edge cases. Most documentation has value across projects (patterns, decisions, examples). |
| **Wait for perfect architecture before committing** | Prevents learning from real usage. Over-engineering risk (solving problems that don't exist). Test-and-learn approach yields better-fit solutions. Can iterate after encountering actual friction. |

---

**Key Resources:**
- [ADR-001: Adopt Explore Agent for Hippocampus Document Discovery](ADR-001-adopt-explore-agent-for-hippocampus-document-discovery.md) - Search mechanism for duplicate prevention
- [ADR-000: Adopt sff for Document Discovery](ADR-000-adopt-sff-semantic-file-finder.md) - Original centralized knowledge base concept (superseded)
