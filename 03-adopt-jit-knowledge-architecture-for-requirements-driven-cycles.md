# 03: Adopt JIT Knowledge Architecture for Requirements-Driven Cycle Work

## Status
**Accepted** | Date: 2025-11-13

## Context
- Knowledge management uncertainty for cycle work: "I already had an issue that I didn't really know what exactly I want to maintain" (user reflection)
- Risk of stale documentation burden when maintaining cycle-level context
- N3 Theme 4 revealed working philosophy: "everything is ephemeral... everything which needs to be gotten can be gotten on demand quickly"
- User observation: "What Cloud Code excels in is to really solve things just in time, if it understands it correctly"
- Need clear philosophy for requirements-driven cycle work specifically (other knowledge types may have different patterns)
- Task → Session → Cycle data model context: cycles are the work unit this philosophy addresses

## Decision
We will adopt Just-In-Time (JIT) Knowledge Architecture for requirements-driven cycle work, inspired by Toyota Production System principles.

**Core Principles:**

**1. Ephemeral Sessions**
- Sessions are throwaway work units
- Nothing within session context must be maintained for future work
- Session ends → context discarded (except authoritative handoff via GitHub Issues per ADR 02)

**2. Knowledge Source Hierarchy**
- **Codebase contains all technical knowledge** (implementations, configs, dependencies)
- **User contains all preferences** (choices, decisions, priorities)
- **AI investigates just-in-time** (reads, searches, explores on-demand)

**3. Need-Driven Persistence Only**
- "Nothing like pre-emptive documentation. It must always come out of a need, never because I think I need" (user principle)
- No speculative documentation for cycle work
- Only persist when need demonstrated through actual use

**4. Pull-Based Production (Toyota Principle)**
- Zero inventory: No unused artifacts created
- Pull-based: Investigation triggered by need, not anticipation
- Minimal waste: No maintenance burden for unused documentation
- Fast flow: Quick retrieval when needed vs slow creation upfront

**Scope Boundary:**
- **This ADR applies to:** Requirements-driven cycle work (within ADR 01 cycle structure)
- **This ADR does NOT apply to:** Other knowledge types (ADRs, architectural decisions, project-level patterns) which may have different persistence patterns

## Evidence

**N3 Theme 4 - User Articulated Philosophy:**

User quote: "Everything is ephemeral... everything which needs to be gotten can be gotten on demand quickly"

User quote: "Nothing like pre-emptive documentation. It must always come out of a need, never because I think I need"

User quote: "If I really have to research something more than three times, then maybe there should be some sort of memory document"

User reflection: "I was struggling with what kind of session artifacts should actually stay persistent because what I noticed is that the system works best if [we keep cycles ephemeral]"

**N3 Theme 4 - Toyota Production System Connection:**

User quote: "How's this Toyota thing called? On demand production"

Recognition of JIT manufacturing principles applied to knowledge work:
- Zero inventory (no speculative docs)
- Pull-based production (create when needed)
- Minimal waste (no unused artifacts)

**N3 Pairs - JIT Investigation Working:**

N3 Pair 7: AI autonomously investigated (searched conversation, read settings.json, checked Bun) without any persistent documentation

N3 Pair 2: AI investigated server setup (SSH connection, repo location) fresh each time

No persistent cycle-level documentation referenced in any N3 pairs - everything investigated on-demand successfully

**User Clarification - Cycle Work Specific:**

User: "For the solving of requirement cycles, this is definitely it!"

User: "This may be different for knowledge methodologies but for the solving of requirement cycles, this is definitely it!"

Clear scope: JIT for cycles, other knowledge may differ

## Consequences

### ✅ Positive
- Eliminates documentation maintenance burden for cycle work
- Prevents stale documentation problem (no docs to become outdated)
- Enables fast JIT investigation when Claude Code has capability
- Reduces friction: "system works best" when cycles are ephemeral (user observation)
- Aligns with Claude Code strengths: "excels at solving things just-in-time"
- Minimal waste: no unused artifacts created speculatively

### ❌ Negative
- No upfront cycle documentation to reference (must investigate each time)
- Requires reliable investigation capability (depends on ADR 01 disambiguation working)
- Knowledge recreation cost if investigation is slow
- No learning curve reduction from persistent cycle docs

### ⚪ Neutral
- Philosophy definitive for requirements-driven cycles
- Other knowledge types (ADRs, architectural decisions) may have different persistence patterns
- Need-driven threshold undefined (implementation detail)
- Cycle ephemeral but GitHub Issue handoff persists (ADR 02) until cycle closes

## Implementation Specifics

**Knowledge Source Mapping:**

**Codebase (Technical Knowledge):**
- Implementations: Read source files
- Configurations: Read config files
- Dependencies: Check package.json, pyproject.toml
- Architecture: Explore file structure, imports

**User (Preferences):**
- Choices: Ask via AskUserQuestion
- Priorities: Ask via AskUserQuestion
- Decisions: Captured in disambiguation (ADR 01)

**AI (JIT Investigation):**
- Tools: Read, Grep, Glob, agent-explore
- Autonomous: Discover dependencies, configs, patterns
- On-demand: Triggered by cycle requirements

**Session Lifecycle:**
```
Session Start
     ↓
(Optional: Read latest GitHub Issue for continuation - ADR 02)
     ↓
Cycle(s): JIT investigation for each requirement
     ↓
Session End → Context discarded (except closed GitHub Issues)
```

**Cycle Lifecycle (Ephemeral Knowledge):**
```
Cycle Start
     ↓
Requirements-Clarity: JIT investigation of WHAT
     ↓
Implementation-Clarity: JIT investigation of HOW
     ↓
Evaluation-Clarity: JIT investigation of verification
     ↓
Execute → Commit
     ↓
GitHub Issue Closed → Cycle knowledge ephemeral (no persistent cycle docs)
```

**Data Model Context:**
- **Task:** High-level goal (may span multiple sessions)
- **Session:** One conversation instance (ephemeral)
- **Cycle:** Requirements → Implementation → Evaluation → Execute → Commit (ephemeral)

This ADR defines knowledge management at Cycle level specifically.

## Alternatives Considered

| Alternative | Rejection Reason |
|-------------|------------------|
| **Persistent cycle documentation** | User observation: "system works best" when ephemeral - documentation becomes stale burden during development |
| **Work logs as cycle knowledge** | ADR 02 evidence: work logs are interpretive, not authoritative - JIT investigation from codebase more reliable |
| **Upfront cycle planning docs** | "Nothing like pre-emptive documentation" - creates maintenance burden and waste for fast-changing cycle work |
| **Session memory/context carryover** | Context window limits prevent this - need explicit handoff (ADR 02) not implicit memory |

---

**Relationship to v2 Architecture:**

This ADR works with:
- **ADR 01 (Progressive Disambiguation):** JIT investigation happens during all three clarity phases - investigation tools discover knowledge on-demand
- **ADR 02 (Session Continuity):** GitHub Issues capture authoritative state but are ephemeral (closed when cycle ends) - not persistent cycle documentation

Together these form **v2 Claude Code methodology**:
- **Within-session cycle structure (ADR 01):** JIT investigation during disambiguation
- **Cross-session continuity (ADR 02):** Ephemeral handoff via GitHub Issues
- **Knowledge management (this ADR):** JIT for cycles, need-driven persistence

**Key Resources:**
- Evidence: research/n3/03_friction_analysis_7363c449.md (Theme 4: JIT Knowledge Architecture)
- Toyota Production System: Zero inventory, pull-based production, minimal waste principles
- Scope: Requirements-driven cycles specifically (other knowledge types may differ)
