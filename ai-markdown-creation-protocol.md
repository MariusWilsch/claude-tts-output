# Adopt AI Markdown Create-or-Edit Protocol with Search-First Duplicate Prevention

[[document-discovery]]

## Status
**Accepted** | Date: 2025-11-21

## Context

**The Challenge:**
- AI agents lack systematic approach for markdown file operations in centralized knowledge base
- Risk of duplicate creation when existing files could be evolved
- Ambiguity about creation vs editing decision authority
- Need for consistent relationship tracking without manual overhead
- Balance between AI autonomy (discovery) and user authority (classification)

**Core Insight:**
Documents evolve continuously rather than existing in "done" states. Git version control enables edit-first workflow where AI discovers existing content and evolves it, preventing fragmentation while preserving complete revision history.

## Decision

We will adopt **search-first create-or-edit protocol** where AI autonomously discovers existing content before any markdown operation, collaborates with user on classification decisions, and enforces mandatory relationship tracking.

**Core Principles:**

**Search-First Discovery:**
- AI searches centralized knowledge base before creating any markdown file
- Discovery surfaces existing files that could be edited rather than duplicated
- Autonomous search eliminates "did I already document this?" uncertainty

**Edit-Over-Duplicate:**
- Found content → Edit existing file (Git tracks evolution)
- Not found → Create new file with proper classification
- Version control preserves complete document history
- No "v2" files or manual versioning - Git handles evolution

**Collaborative Classification:**
- AI discovers and presents options
- User decides tier placement (cross-project vs project-specific)
- User selects relationship tracking (phantom nodes)
- Clear authority boundary: AI finds, user classifies

**Mandatory Relationship Tracking:**
- Every file requires explicit semantic relationships via wikilinks
- Search-and-reuse pattern for relationship vocabulary
- Prevents isolated documents without discoverable context
- Enables both AI discovery (search) and human visualization (graph)

**Interactive Refinement:**
- User confirmation at key decision points
- Tool for ALL user interaction (not just preferences, also context and confirmation)
- Prevents assumption-based decisions without validation

## Consequences

### ✅ Positive

**Duplicate Prevention Through Evolution:**
- Search discovers existing files to edit rather than duplicate
- Git version control tracks continuous document improvement
- Single source of truth with complete revision history
- No "notes-v2.md" proliferation or version drift

**Clear Authority Boundaries:**
- AI autonomy: Discovery and search operations
- User authority: Classification decisions and edit vs create choice
- No ambiguity about "can AI decide this?" or "must I approve?"
- Interactive pattern at explicit decision checkpoints

**Systematic Relationship Tracking:**
- Mandatory wikilinks ensure every file has discoverable context
- Search-and-reuse prevents phantom node proliferation
- Relationship vocabulary emerges organically through reuse
- Both AI discovery layer and human visualization layer supported

**Ephemeral Session Compatible:**
- No session state required (truth lives in files)
- Fresh discovery each session via search
- Git preserves evolution between sessions
- JIT knowledge retrieval replaces handoff documents

### ❌ Negative

**Workflow Latency:**
- Search before action adds overhead vs immediate creation
- Interactive decisions require user input
- Trade-off: thoroughness vs speed
- Multiple steps vs "just create file"

**Search Tool Dependency:**
- Workflow effectiveness tied to discovery mechanism quality
- Failed search could miss existing files
- No automatic enforcement beyond workflow discipline
- Discovery quality determines duplicate prevention success

**Learning Curve:**
- New interaction pattern for AI agents to adopt
- Users must participate in classification decisions
- Requires understanding tier semantics and phantom node purpose
- More interactive than autonomous file creation

### ⚪ Neutral

**Version 1 Workflow:**
- Based on initial reasoning (test-and-learn approach)
- Will evolve based on real friction encountered
- Specific steps may change while principles remain stable
- Iteration expected as usage patterns emerge

**Relationship Vocabulary Emergence:**
- No predefined taxonomy or phantom node list
- Vocabulary emerges through search-and-reuse patterns
- Natural convergence toward stable semantic groupings
- Balance between consistency and flexibility

## Alternatives Considered

| Alternative | Rejection Reason |
|-------------|------------------|
| **No mandatory search** | Violates edit-over-duplicate principle. High duplicate risk when AI doesn't check existing files. Discovery before action is non-negotiable for preventing fragmentation. |
| **AI auto-determines all decisions** | Removes user authority over classification and relationships. Content categorization requires domain knowledge AI lacks. Collaborative approach ensures intentional decisions. |
| **Optional relationship tracking** | Creates isolated documents without discoverable context. Mandatory wikilinks ensure every file has semantic connections. Files without relationships become invisible to discovery. |
| **Create with versioned names** | Reintroduces manual versioning problem Git solves. "notes-v2.md" pattern fragments knowledge. Version control designed specifically for tracking evolution without filename pollution. |
| **Autonomous editing without confirmation** | Breaks trust boundary - AI must confirm before modifying user content. Discovery is autonomous, editing requires validation. Clear authority model prevents unwanted changes. |
