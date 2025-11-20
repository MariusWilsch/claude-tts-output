# ADR: Adopt Obsidian Wikilinks for Flat File Structure with Semantic Relationships

## Status
**Accepted** | Date: 2025-11-20

**Related ADRs:**
- [[sff-semantic-file-finder]] (superseded - replaced by Explore agent)
- [[explore-agent-hippocampus-document-discovery]] (current document discovery method)

## Context

**Organizational Structure:**
- Hippocampus uses flat file structure: resources/, clients/, company/
- Files organized semantically by name, not folder hierarchy
- Explore agent performs semantic search across all files

**The Problem:**
- Client files have natural relationships (workshops → deliverables → contracts)
- Flat structure loses implicit grouping that folders provide
- Need explicit way to connect related documents
- AI agents must discover relationships for effective search

**Requirements:**
- Maintain flat structure (no nested folders)
- Preserve semantic relationships between files
- AI agent (Explore) must understand relationships
- Human-readable and writable
- Grep/search must work efficiently

## Decision

We will use **Obsidian wikilinks** (`[[filename]]` syntax) to create explicit semantic relationships between files in the flat hippocampus structure.

**Implementation Specifics:**
- Use basic wikilink syntax: `[[filename]]` (no paths needed in flat structure)
- Create "hub" documents for major entities (e.g., `avo-client.md` linking to all avo workshops/deliverables)
- AI agents parse wikilinks via regex: `\[\[([^\]|]+)(?:\|[^\]]+)?\]\]`
- Backlinks computed on-demand via grep: `rg '\[\[target-filename'`
- Files maintain unique names across vault for unambiguous resolution

**Why Wikilinks:**
- Plain text format (no proprietary encoding)
- Simple regex parsing for AI agents
- Human-readable and writable
- Grep/ripgrep fully compatible
- Semantic relationships explicit in content

## Consequences

### ✅ Positive

**Flat Structure Preserved:**
- No folder hierarchy needed
- Simple `[[filename]]` syntax (no paths)
- Unique filenames eliminate ambiguity

**AI Agent Compatible:**
- Explore agent reads wikilinks as plain text
- Regex parsing: `\[\[([^\]]+)\]\]` extracts targets
- Forward links discovered by reading file content
- Backlinks computed via grep across all files

**Semantic Relationships Explicit:**
- Links visible in file content (not implied by folders)
- Relationship types can be documented (e.g., "Supersedes:", "Related:")
- Network of connections emerges naturally

**Fast Discovery:**
- Grep searches flat directory efficiently
- File resolution simple: `filename` → `filename.md`
- No path traversal needed

**Scalability:**
- Works well up to thousands of files
- Grep/ripgrep handles large file sets efficiently
- O(n) search in flat structure

### ❌ Negative

**Not Standard Markdown:**
- Wikilinks won't render in GitHub, VSCode preview, or other standard Markdown viewers
- Alternative `[text](file.md)` syntax has broader compatibility but loses Obsidian features

**No Visual Graph (without Obsidian):**
- Backlinks must be computed manually via grep
- No automatic graph visualization
- Requires Obsidian app for visual network exploration

**Filename Uniqueness Required:**
- All filenames must be unique across vault
- Cannot have `notes.md` in multiple contexts
- Requires thoughtful naming conventions

**Obsidian Ecosystem Dependency:**
- Tied somewhat to Obsidian conventions
- Block references `[[file#^blockid]]` don't work elsewhere
- Embed syntax `![[file]]` won't render outside Obsidian

### ⚪ Neutral

**Naming Convention Needed:**
- Must establish clear, descriptive filename patterns
- Example: `avo-workshop-1.md`, `archibus-contract-2025.md`
- Prevents generic names like `meeting.md`, `notes.md`

**Hub Document Pattern:**
- Create index documents for major entities
- Example: `avo-client.md` with curated links to all avo files
- Manual curation vs. automatic aggregation trade-off

**Obsidian App Optional:**
- Wikilinks work without Obsidian (plain text parsing)
- Obsidian provides enhanced features (graph view, backlinks panel)
- Can use vault with or without Obsidian app

## Alternatives Considered

| Alternative | Rejection Reason |
|-------------|------------------|
| **Folder Hierarchy** | Contradicts flat structure philosophy established in [[explore-agent-hippocampus-document-discovery]]. Files would need paths in links (`[[folder/file]]`), increasing complexity. Folder organization is manual overhead that semantic search eliminates. |
| **Standard Markdown Links** | Syntax `[text](file.md)` has broader compatibility but loses Obsidian's automatic backlink computation and graph visualization. More verbose to write. Agent still needs to parse links, just different regex pattern. Trade-off: portability vs. ecosystem features. |
| **YAML Frontmatter Only** | Frontmatter provides metadata but not bidirectional relationships. Requires structured field definitions. Less human-readable for navigating relationships. Wikilinks complement frontmatter (both can be used together). |
| **Tags Instead of Links** | Tags categorize but don't create explicit relationships between specific files. No directional connections (A relates to B). Tags useful for grouping, wikilinks for relationships. Both can coexist. |
| **Implicit Relationships via Naming** | File prefixes (e.g., `avo-*`) provide weak grouping but no explicit connections. Agent must infer relationships from patterns. Error-prone and ambiguous. Wikilinks make relationships explicit and discoverable. |

---

**Key Resources:**
- [Obsidian Wikilinks Documentation](https://help.obsidian.md/Linking+notes+and+files/Internal+links)
- [Ripgrep for Link Discovery](https://github.com/BurntSushi/ripgrep)
- Research: AI agent compatibility with wikilinks (session 2025-11-20)
- Related: [[explore-agent-hippocampus-document-discovery]] for semantic search implementation
