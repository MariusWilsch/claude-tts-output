## Section 3: Functional Requirements (Funktionale Anforderungen)

**Understanding:**
- Requirements organized by Section 2 goals
- Shows traceability from high-level goals to specific features
- POC focuses on Historical Recipe Cleanup only

### Must (POC Scope)

| ID | Description |
|----|-------------|
| FR-02 | System shall match ingredients by Material_ID (article number) for exact identification. |
| FR-02a | System shall calculate ingredient overlap ratio between recipe pairs. |
| FR-03 | System shall support hierarchical recipe structures (Vormischungen/pre-mixes) with option to compare at same level or exploded to base ingredients. |
| FR-04 | System shall compare percentage amounts between matched ingredient pairs and calculate similarity scores. |
| FR-08 | System shall identify unmatched ingredients sharing the same resource category (Rohstoffkategorie) for potential substitution matching. |
| FR-05 | System shall output similarity rankings (not binary yes/no) showing percentage match scores between recipe pairs. |
| FR-06 | System shall export results to Excel format with recipe details and match scores. |
| FR-11 | System shall validate POC functionality with subset of ~100 recipes before scaling to full ~8000 recipe database. |

### Deferred (Post-POC)

| ID | Description |
|----|-------------|
| FR-07 | System shall filter recipes by special ingredient attributes (VLOG, TK/Tiefkühl, Bio, Halal, Kosher). |
| FR-10 | System shall use configurable threshold parameters for similarity calculations. |
| FR-12 | System shall provide chat interface for interactive similarity search queries. |
| FR-23 | System shall remember user-accepted ingredient substitutions for future comparison suggestions. |
| FR-24 | System shall provide visual highlighting of percentage differences with configurable color coding and slider controls. |
| FR-25 | System shall provide ingredient-level and recipe-level comparison views with percentage differences shown per column. |
| FR-26 | System shall query recipe database directly via JDBC for data access. |
| FR-27 | System shall automatically generate and update metadata structure file through batch processing for consistent data synchronization. |
| FR-13 | System shall parse PDF documents to extract recipe information from product requests (both searchable and scanned). |
| FR-14 | System shall parse multi-format inputs (free text, English descriptions, quantity unit conversion like "3g/kg" → 0.3%). |
| FR-15 | System shall enable manual trigger by developer for product request similarity searches (not automatic background processing). |
| FR-16 | System shall integrate with replacement product request system (replacing Lotus Notes). |
| FR-17 | System shall match ingredients across multiple languages (German, English, Russian, Polish). |
| FR-18 | System shall integrate with existing translation dictionary for cross-language ingredient matching. |
| FR-19 | System shall calculate optimal batch sizes to minimize partial containers for priority ingredients (TK, Tomatenmark, etc.). |
| FR-20 | System shall adjust recipe quantities within tolerance ranges for full container utilization. |
| FR-21 | System shall optimize for full container usage of specified priority raw materials. |
| FR-22 | System shall integrate production equipment capacity constraints (batch sizes per mixer type). |

### Traceability to Section 2 Goals

**Historical Recipe Cleanup (Must - POC Scope):**
- FR-02, FR-02a, FR-03, FR-04, FR-08, FR-05, FR-06, FR-11

**Historical Recipe Cleanup (Deferred):**
- FR-07, FR-10, FR-12, FR-23, FR-24, FR-25, FR-26, FR-27

**Preventive Duplicate Detection (Deferred):**
- FR-13, FR-14, FR-15, FR-16, FR-17, FR-18

**Production Optimization (Deferred):**
- FR-19, FR-20, FR-21, FR-22
