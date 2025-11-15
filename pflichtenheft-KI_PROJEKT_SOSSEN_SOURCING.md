# Pflichtenheft

## KI_PROJEKT_SOSSEN_SOURCING

---

## Section 1: Cover Page (Deckblatt)

| | |
|---|---|
| **Project** | KI_PROJEKT_SOSSEN_SOURCING |
| **Client** | AVO-Werke August Beisse GmbH |
| **Contractor** | Wilsch AI Services OÜ |

---

## Section 2: Goal Determination (Zielbestimmung)

### Must (POC Scope)

**Historical Recipe Cleanup:**
- Identify duplicate and similar recipes among ~8000 existing recipes
- Compare recipes based on ingredient composition and percentages
- Present similarity rankings to enable manual harmonization decisions
- Reduce production complexity by consolidating redundant recipes

**Search based on ingredient names, article numbers, and percentage compositions**
- POC validation starts with subset of ~100 recipes

### Deferred (Post-POC)

**Historical Recipe Cleanup - Advanced filtering capabilities**
- Filter recipes by special ingredient attributes (VLOG, TK, Bio, Halal, Kosher)

**Preventive Duplicate Detection:**
- Enable developers to check new product requests against existing recipe database
- Support processing of ~7000 annual product requests
- Manual trigger by developer (not automatic background processing)
- Integration into new product request system (replacement of Lotus Notes)

**Production Optimization:**
- Batch size and production quantity optimization
- Full container utilization optimization (minimizing partial containers)
- Recipe adjustment automation for production efficiency

**Future Enhancements:**
- Direct sales team access to similarity search
- Multi-language ingredient translation system integration
- Reusable AI infrastructure components for future projects
- Hybrid data approach (master data cache + selective live queries)

### Out of Scope

- Automatic recipe merging without human approval
- Automatic specification changes without quality assurance review
- Complete replacement of IBM ERP system
- Sensory/taste prediction capabilities
- Recipe formulation from scratch (only finding existing similar recipes)

---

## Section 3: Functional Requirements (Funktionale Anforderungen)

### Must (POC Scope)

**Compare recipes based on ingredient composition and percentages**
- **FR-02:** System shall match ingredients by Material_ID (article number) for exact identification.
- **FR-02a:** System shall calculate ingredient overlap ratio between recipe pairs.
- **FR-03:** System shall support hierarchical recipe structures (Vormischungen/pre-mixes) with option to compare at same level or exploded to base ingredients.
- **FR-04:** System shall compare percentage amounts between matched ingredient pairs and calculate similarity scores.
- **FR-08:** System shall identify unmatched ingredients sharing the same resource category (Rohstoffkategorie) for potential substitution matching.

**Present similarity rankings to enable manual harmonization decisions**
- **FR-05:** System shall output similarity rankings (not binary yes/no) showing percentage match scores between recipe pairs.
- **FR-06:** System shall export results to Excel format with recipe details and match scores.

**Validate POC functionality**
- **FR-11:** System shall validate POC functionality with subset of ~100 recipes before scaling to full ~8000 recipe database.

### Deferred (Post-POC)

**Historical Recipe Cleanup**

_Advanced filtering and UI capabilities_
- **FR-07:** System shall filter recipes by special ingredient attributes (VLOG, TK/Tiefkühl, Bio, Halal, Kosher).
- **FR-10:** System shall use configurable threshold parameters for similarity calculations.
- **FR-12:** System shall provide chat interface for interactive similarity search queries.

_Visual comparison enhancements_
- **FR-23:** System shall remember user-accepted ingredient substitutions for future comparison suggestions.
- **FR-24:** System shall provide visual highlighting of percentage differences with configurable color coding and slider controls.
- **FR-25:** System shall provide ingredient-level and recipe-level comparison views with percentage differences shown per column.

_Data infrastructure_
- **FR-26:** System shall query recipe database directly via JDBC for data access.
- **FR-27:** System shall automatically generate and update metadata structure file through batch processing for consistent data synchronization.

**Preventive Duplicate Detection**

_Enable developers to check new product requests against existing recipe database_
- **FR-13:** System shall parse PDF documents to extract recipe information from product requests (both searchable and scanned).
- **FR-14:** System shall parse multi-format inputs (free text, English descriptions, quantity unit conversion like "3g/kg" → 0.3%).

_Support processing of ~7000 annual product requests_
- **FR-15:** System shall enable manual trigger by developer for product request similarity searches (not automatic background processing).

_Integration into new product request system_
- **FR-16:** System shall integrate with replacement product request system (replacing Lotus Notes).

_Multi-language support_
- **FR-17:** System shall match ingredients across multiple languages (German, English, Russian, Polish).
- **FR-18:** System shall integrate with existing translation dictionary for cross-language ingredient matching.

**Production Optimization**

_Batch size and production quantity optimization_
- **FR-19:** System shall calculate optimal batch sizes to minimize partial containers for priority ingredients (TK, Tomatenmark, etc.).
- **FR-20:** System shall adjust recipe quantities within tolerance ranges for full container utilization.

_Full container utilization optimization_
- **FR-21:** System shall optimize for full container usage of specified priority raw materials.
- **FR-22:** System shall integrate production equipment capacity constraints (batch sizes per mixer type).

---

## Section 4: Non-Functional Requirements (Liste der nicht-funktionalen Anforderungen)

**Note:** Final quantified metrics to be defined in collaboration with Thomas Erhard (infrastructure specialist)

### Performance

- **NFR-01 [TBD]:** System shall support comparison operations on database of ~8000 recipes.
  - _To be quantified: Response time thresholds, throughput requirements_

- **NFR-02 [TBD]:** POC shall complete similarity analysis on subset of ~100 recipes.
  - _To be quantified: Maximum processing time acceptable_

### Compatibility

- **NFR-03:** System shall integrate with IBM AS/400 database system.

- **NFR-04:** System shall export results in Excel-compatible format.

### Security

- **NFR-05 [TBD]:** System shall require VPN tunnel access for POC deployment phase.
  - _To be defined with Thomas Erhard: Encryption standards, authentication requirements_

### Usability

- **NFR-06:** System shall support manual triggering by developers (not fully automated processing).

---

**Action Items:**
- Review and quantify NFR-01, NFR-02, NFR-05 with Thomas Erhard
- Define specific performance thresholds (response time < X seconds, etc.)
- Specify security requirements (encryption standards, access controls)

---

## Section 5: Acceptance Criteria (Abnahmekriterien)

**Note:** Acceptance criteria for deferred requirements will be defined during their respective implementation phases.

### FR-02: Material_ID Matching
- **Given** two recipes with shared Material_IDs
- **When** comparison is executed
- **Then** system identifies all exact Material_ID matches between recipes

### FR-02a: Overlap Ratio Calculation
- **Given** Recipe A (20 ingredients) and Recipe B (10 ingredients) with 8 shared ingredients
- **When** overlap ratio is calculated
- **Then** system returns overlap ratio of 0.40 (8/20 using MAX normalization)

### FR-04: Percentage Similarity
- **Given** matched ingredient with 5.2% in Recipe A and 5.8% in Recipe B
- **When** percentage similarity is calculated
- **Then** system calculates similarity score based on percentage difference

### FR-08: Resource Category Matching
- **Given** unmatched ingredients from two recipes
- **When** resource category comparison is executed
- **Then** system identifies and flags ingredient pairs sharing same Rohstoffkategorie

### FR-05: Similarity Rankings Output
- **Given** comparison of Recipe A against all recipes in database
- **When** similarity search completes
- **Then** system outputs ranked list of similar recipes with percentage match scores (not binary yes/no)

### FR-06: Excel Export
- **Given** completed similarity analysis results
- **When** export is requested
- **Then** system generates Excel file containing recipe pairs, match scores, and ingredient details

### FR-11: POC Validation
- **Given** POC subset of 100 recipes
- **When** validation tests are executed
- **Then** system successfully completes all comparison operations without errors before scaling to full database

---

## Section 6: Technical Constraints (Technische Rahmen- oder Randbedingungen)

### Deployment Environment

**POC Phase:**
- Hosting: WPH datacenter on IBM Power 10
- Data format: IBM Save-File (*SAVF) containing metadata table
- Test dataset: 100 recipes with 5 known duplicate pairs (provided by AVO)
- Hosting costs included in proposal

**Production Phase:**
- On-premise deployment on AVO's IBM Power 10 server
- Hardware: 8 CPU cores, 512GB RAM
- Operating system: IBM i
- AI-LPAR setup effort: 4-5 person-days
- No additional hardware required (current assessment)

### Required Integrations

**Database Integration:**
- IBM AS/400 / IBM i system with DB2 database
- Data access: Metadata file in IBM Save-File format (*SAVF)
- Metadata structure: Denormalized table with flattened recipe hierarchy
- ~8000 recipes in production database
- Batch processing for metadata file updates (cycle TBD with AVO)

**Output Integration:**
- Excel export format (based on AVO template from workshop)
- Top 5 similar recipes per query
- Three criteria displayed separately per match

**Existing Systems Context:**
- DIA-LIMS system (laboratory information, linked to metadata)
- SoftM/Comarch ERP system
- Lotus Notes/Domino (product request system - replacement planned)

### Technology Stack Decisions

**Backend [TBD with Thomas Erhard]:**
- Preferred: FastAPI (Python)
- Constraint: IBM Power processor compatibility to be verified
- Alternative: Node.js (confirmed compatible with IBM i)

**AI/ML Framework [TBD]:**
- Framework selection during implementation phase
- Must support similarity algorithm requirements

**Data Processing:**
- Metadata file: Hierarchical recipe structures flattened to single-level
- Relative quantities calculated to 100% per manufacturing instruction
- Integration with DIA-LIMS data fields

**AVO Infrastructure Context:**
- Existing technologies: RPG, Java, Profound UI
- Database: DB2 on IBM i
- Python deployment: Compatibility verification needed

---

**Action Items:**
- Verify FastAPI/Python deployment on IBM Power 10 with Thomas Erhard
- Receive metadata file (*SAVF) test dataset from AVO (100 recipes)
- Receive Excel template from AVO for output formatting
- Define batch processing cycle for metadata updates

---

## Section 7: Data Model (Datenmodell)

### Metadata Table Structure

The POC uses a denormalized metadata file containing flattened recipe data. Key transformations:

- Hierarchical Baukasten structure → single-level table
- Relative quantities normalized to 100% per manufacturing instruction
- DIA-LIMS data integrated per ingredient

**Complete column structure:** See "AVO_WS2_Tabellenstruktur Meta-Datei_20251108.xlsx" (Workshop 2 deliverable)

**Source:** IBM AS/400 / IBM i (DB2)
**Format:** IBM Save-File (*SAVF)
**Update:** Batch processing (cycle TBD with AVO)

---

## Section 8: Domain Glossary (Fachbegriffe)

### Recipe Structure Terms

**Vormischungen (Pre-mixes)**
Intermediate products marked with "V" prefix that have their own recipes and are used as ingredients in final products.

**Baukasten (Modular Structure)**
Hierarchical recipe system where recipes can contain other recipes as components.

**Herstellvorschrift (Manufacturing Instruction)**
Recipe specification defining ingredients and their proportions.

**Ansatzgröße (Batch Size)**
Production quantity for a single manufacturing run.

### Ingredient Classification

**Material_ID (Article Number)**
Unique identifier for ingredients and components in the database.

**Rohstoffkategorie (Resource Category)**
Functional grouping of ingredients for substitution matching (e.g., "Gewürze/Paprika" for all paprika variants).

**Materialgruppe (Material Group)**
Purchasing-oriented ingredient categories (M-prefix).

### Quality & Dietary Attributes

**VLOG (Genetic Modification-Free)**
Ingredients certified as free from genetic engineering.

**TK (Tiefkühl - Frozen)**
Frozen ingredients requiring special handling and storage.

**Bio (Organic)**
Ingredients meeting organic certification standards.

**Halal**
Ingredients compliant with Islamic dietary laws.

**Kosher**
Ingredients compliant with Jewish dietary laws.

### Technical Terms

**DIA-LIMS**
Laboratory Information Management System containing specification data.

**IBM Save-File (*SAVF)**
IBM i file format used for data transfer between systems.

**Metadatei (Metadata File)**
Denormalized table structure containing flattened recipe data for AI processing.

**Muster (Sample)**
Sample status articles (M-prefix) still under development.

---

## Section 9: Evaluation Infrastructure (Evaluierungsmethodik)

### Test Dataset Structure

**Size:** 100 recipes from production database

**Composition:**
- Minimum 5 known duplicate pairs manually identified by AVO product development
- Represents realistic production data distribution
- Known duplicates serve as validation baseline

**Format:** IBM Save-File (*SAVF) in metadata table structure

**Provider:** AVO (Mitwirkungspflicht - client responsibility)

### Input/Output Specification

**Input:**
- Article number (Artikelnummer) as query parameter
- Single recipe comparison per query

**Output:**
- Top 5 most similar recipes ranked by similarity
- Excel format based on AVO workshop template
- Three criteria displayed separately per match:
  1. Komponenten-Übereinstimmung (Overlap ratio)
  2. Mengenähnlichkeit (Percentage similarity)
  3. Kategorie-Matching (Resource category matches)

### Success Criteria

**Primary Validation:**
- Algorithm must identify the 5 known duplicate pairs
- Known duplicates should rank in Top 5 results for their counterparts

**Iterative Refinement:**
- AVO product development reviews Excel outputs
- Algorithm parameters adjusted based on feedback
- Threshold values tuned iteratively (starting point: 10 percentage points)

**Acceptance:**
- Known duplicates correctly identified
- Results deemed useful by product development for harmonization decisions
- False positive rate acceptable to AVO

### Evaluation Process

1. Load test dataset (100 recipes) into POC environment
2. Run similarity search for each recipe in test set
3. Export results to Excel using AVO template
4. AVO reviews outputs and validates against known duplicates
5. Adjust algorithm parameters if needed
6. Repeat until acceptance criteria met

**Responsibility:** Wilsch AI Services implements evaluation, AVO validates results
