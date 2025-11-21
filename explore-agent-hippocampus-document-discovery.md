# ADR-001: Adopt Explore Agent for Hippocampus Document Discovery

## Status
**Accepted** | Date: 2025-11-18

**Supersedes:** [ADR-000: Adopt sff (SemanticFileFinder) for Document Discovery](ADR-000-adopt-sff-semantic-file-finder.md)

## Context

**The Problem:**
- Empirical testing of sff semantic search revealed 50% success rate (2/4 test queries)
- Failed to find React frontend README (ranked #2 and #5 with low scores 0.26/0.25, below deployment docs)
- Failed to find database ADRs (returned ADR distribution system docs instead of database architecture docs)
- Semantic embeddings prioritized keyword density over conceptual intent
- Filename-based discovery (e.g., "README-REACT-FRONTEND.md") performed poorly despite descriptive naming

**Test Results Summary:**

| Query | sff Result | Explore Agent Result |
|-------|------------|---------------------|
| Caddy subdomain setup | ✅ Found (0.67 score, rank #1) | ✅ Found immediately |
| FastAPI backend patterns | ✅ Found (0.65 score, rank #1) | ✅ Found immediately |
| React frontend guidelines | ❌ Missed (0.26 score, rank #2/5) | ✅ Found immediately |
| Database-related ADRs | ❌ Wrong results (ADR system docs) | ✅ Found 2 files with details |

**Requirements:**
- Git-tracked centralized knowledge base (~/.claude/hippocampus/)
- Cross-system portability (travels with Claude config across installations)
- Reliable document discovery by conceptual intent, not just keyword matching
- Zero-maintenance philosophy (no metadata, no categorization overhead)

## Decision

We will use **Explore agent** for document discovery in ~/.claude/hippocampus/, replacing the planned sff semantic search workflow while maintaining the centralized hippocampus directory architecture.

**Implementation Specifics:**
- Explore agent invoked via Task tool for document searches
- Hippocampus directory remains at ~/.claude/hippocampus/ (Git-tracked)
- Flat file structure with path-prefixed filenames (e.g., `docs-work-log-file.md`)
- 34 markdown files from velox-global-adrs as initial knowledge base
- Agent searches by conceptual queries without requiring exact terminology

## Consequences

### ✅ Positive

**Higher Search Reliability:**
- 100% success rate (4/4) vs sff's 50% (2/4) in empirical testing
- Successfully handles both filename-based discovery (READMEs) and content-based discovery (Caddy patterns)
- Better conceptual query understanding ("backend patterns" finds FastAPI README without "FastAPI" keyword)

**Intent-Based Discovery:**
- Finds files by user intent rather than semantic embedding similarity
- Handles multi-concept queries correctly ("database-related ADRs" = database + ADRs, not ADR system)
- Works with generic queries ("subdomain setup") without requiring specific technology names

**Consistent Performance:**
- No query-dependent variance in success (unlike sff's 0.26-0.67 score range)
- Provides detailed content descriptions, not just paths with scores
- Filename pattern matching complements content understanding

### ❌ Negative

**Cost vs Local Execution:**
- Explore agent uses model inference (API cost) vs sff's local embeddings (zero cost)
- Each search consumes tokens, scaling with knowledge base size and query complexity
- No caching mechanism - repeated queries incur repeated costs

**Performance Trade-off:**
- Slower than sff's ~250ms searches (agent involves model reasoning)
- Latency depends on model availability and load
- No sub-second search guarantee like sff's stateless architecture

**Complexity:**
- Requires Task tool invocation vs simple bash command (`sff "query"`)
- Agent-based approach less transparent than direct CLI tool
- Harder to integrate into external scripts or automation

### ⚪ Neutral

**Architecture Shift:**
- Replaces planned sff workflow before production adoption
- Hippocampus directory concept unchanged (still Git-tracked, cross-system)
- Flat file structure still optimal for both approaches

**Model Dependency:**
- Explore agent quality tied to underlying model capabilities
- Future model improvements automatically benefit search quality
- Can switch back to sff if cost/performance becomes prohibitive

## Alternatives Considered

| Alternative | Rejection Reason |
|-------------|------------------|
| **sff (SemanticFileFinder)** | Empirical testing revealed 50% success rate. Failed on React README (semantic embeddings ranked deployment docs higher than actual README) and database ADRs (confused "database ADRs" with "ADR system architecture"). Query-dependent reliability (0.26-0.67 score variance) makes it unsuitable for general-purpose document discovery. |
| **Hybrid (sff + Explore fallback)** | Adds complexity without clear benefit. sff's failures weren't edge cases - React README and database ADRs are common query patterns. Maintaining two search systems increases cognitive load and decision friction ("which tool for which query?"). Explore agent's 100% success rate eliminates need for fallback. |
| **Custom MCP server for sff** | Doesn't solve core semantic search limitations. Test failures weren't about interface convenience - sff's embedding model prioritized keyword density over conceptual intent. Building infrastructure around a fundamentally unreliable search method wastes effort. |

---

**Key Resources:**
- [ADR-000: Adopt sff for Document Discovery](ADR-000-adopt-sff-semantic-file-finder.md) - Superseded decision and original rationale
- [sff GitHub Repository](https://github.com/do-me/sff) - Tool remains available for future re-evaluation
- [velox-global-adrs Repository](https://github.com/veloxforce/velox-global-adrs) - Source of hippocampus knowledge base
