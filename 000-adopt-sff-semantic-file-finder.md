# ADR-000: Adopt sff (SemanticFileFinder) for Document Discovery

## Status
**Accepted** | Date: 2025-01-18

## Context

**The Problem:**
- 28+ ADRs scattered across 5 separate locations (`/docs/adr/`, `/docs/pricing-framework/adr/`, `/docs/time-adrs/`, `/research/adr/`, `/docs/identity/`)
- Client documentation inconsistent (some clients have folders, some don't)
- Templates, research notes, workshop materials dispersed throughout repository
- Constant decision friction: "Where should I save this? Where did I put that?"
- Mental overhead maintaining folder hierarchies that exist primarily to enable retrieval

**The Insight:**
Organization systems exist to enable retrieval. If retrieval is perfect through semantic search, elaborate folder organization becomes optional overhead rather than necessity.

**Requirements:**
- Local/self-hosted (no cloud dependencies)
- Returns file paths for navigation (not content chunks for RAG)
- Auto-updates when files change (no manual reindexing)
- Minimal maintenance burden
- Works with ~2000 markdown files (ADRs, client docs, research, templates, business operations)

## Decision

We will use **sff (SemanticFileFinder)** for semantic search-based document discovery, eliminating the need for elaborate folder organization through stateless on-the-fly embedding generation.

**Core Capabilities:**
- Semantic search → file paths + line numbers (clickable in terminal/VS Code)
- Stateless architecture (no index, no server, no persistent state)
- On-the-fly embedding generation using model2vec-rs
- Recursive directory scanning with always-fresh results
- Local execution (100% privacy, no API dependencies)

**Reference:** [sff GitHub Repository](https://github.com/do-me/sff)

## Consequences

### ✅ Positive

**Zero Maintenance:**
- No index to build or rebuild
- No server process to manage
- No file watchers to configure
- No state to corrupt or sync

**Always Fresh:**
- Scans live directory on each search
- File changes immediately searchable
- No stale index problems
- No manual reindex triggers

**Location-Agnostic:**
- Save files anywhere in repository
- No "wrong place" for documents
- Eliminates decision paralysis: "Where should this go?"
- Reduces folder maintenance overhead

**Semantic Discovery:**
- Find documents by concept/meaning, not filename or path
- Natural language queries: "workshop facilitation patterns"
- Matches how brain remembers information (concepts, not locations)
- Superior to keyword-based grep/ripgrep for conceptual searches

**Privacy & Control:**
- 100% local execution
- No cloud services or API keys
- Client data never leaves machine
- Complete control over search infrastructure

### ❌ Negative

**Search Latency:**
- ~250ms for 2500 files (acceptable for CLI tool, not instant)
- Scales linearly with file count (10k+ files may become slow)
- Trade-off: freshness vs. speed (chose freshness)

**CLI-Only Interface:**
- No web UI or graphical interface
- Requires terminal comfort
- Not suitable for non-technical team members if added later

**Rust/Cargo Dependency:**
- Installation requires Rust toolchain
- Additional setup step vs. npm/pip tools
- May create friction for new environment setups

### ⚪ Neutral

**Folder Structure Flexibility:**
- Enables but doesn't mandate flat structure
- Folder organization becomes preference rather than requirement
- Separate decision needed for optimal structure (deferred to future ADR)

**Complementary to Other Tools:**
- Compatible with Obsidian integration (noted for future exploration)
- Can coexist with traditional folder browsing
- Augments rather than replaces file system organization

## Alternatives Considered

| Alternative | Rejection Reason |
|-------------|------------------|
| **LEANN (vector database)** | Designed for RAG (content retrieval) not document discovery (path retrieval). Returns content chunks to answer questions, not file paths for navigation. Fundamental use case mismatch. |
| **Typesense (search engine)** | Enterprise-grade overkill. Requires server management, schema definition, indexing pipelines, file watchers. 10+ minute reindex for 2000 docs. Massive complexity for minimal benefit (sub-50ms vs 250ms queries). |
| **semtools (LlamaIndex)** | Workspace caching provides faster repeat searches, but adds maintenance overhead (workspace management, index cleanup). Chose simplicity over performance optimization at current scale. |
| **Obsidian plugins** | Ties solution to specific note-taking tool. Reduces flexibility, requires Obsidian adoption. Prefer tool-agnostic solution that works with any markdown workflow. |
| **Custom SQLite + embeddings** | Significant development effort, maintenance burden, file watcher implementation. Reinventing wheel when purpose-built tool exists. Violates YAGNI principle. |

---

**Key Resources:**
- [sff GitHub Repository](https://github.com/do-me/sff) - Official documentation and installation
- [Research: sff vs Typesense Comparison](../research/sff-vs-typesense-comparison.md) - Detailed analysis (if created)
- Future ADR: Document organization structure (folder strategy, Git workflow, Obsidian integration)
