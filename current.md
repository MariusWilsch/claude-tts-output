## Section 3: Functional Requirements (Funktionale Anforderungen)

**Understanding:**
- Requirements organized by Section 2 goals
- Shows traceability from high-level goals to specific features
- POC focuses on Historical Recipe Cleanup only

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

**Historical Recipe Cleanup - Advanced filtering capabilities**
- **FR-07:** System shall filter recipes by special ingredient attributes (VLOG, TK/Tiefkühl, Bio, Halal, Kosher).

**Preventive Duplicate Detection**

_Enable developers to check new product requests against existing recipe database_
- **FR-12:** System shall provide chat interface for interactive similarity search queries during product request processing.
- **FR-13:** System shall parse PDF documents to extract recipe information from product requests (both searchable and scanned).
- **FR-14:** System shall parse multi-format inputs (free text, English descriptions, quantity unit conversion like "3g/kg" → 0.3%).

_Support processing of ~7000 annual product requests_
- **FR-15:** System shall enable manual trigger by developer for product request similarity searches (not automatic background processing).

_Integration into new product request system_
- **FR-16:** System shall integrate with replacement product request system (replacing Lotus Notes).

**Production Optimization**

_Batch size and production quantity optimization_
- **FR-19:** System shall calculate optimal batch sizes to minimize partial containers for priority ingredients (TK, Tomatenmark, etc.).
- **FR-20:** System shall adjust recipe quantities within tolerance ranges for full container utilization.

_Full container utilization optimization_
- **FR-21:** System shall optimize for full container usage of specified priority raw materials.
- **FR-22:** System shall integrate production equipment capacity constraints (batch sizes per mixer type).

**Future Enhancements**

_Historical Recipe Cleanup - Algorithm tuning capabilities_
- **FR-10:** System shall use configurable threshold parameters for similarity calculations.

_Preventive Duplicate Detection - Multi-language support_
- **FR-17:** System shall match ingredients across multiple languages (German, English, Russian, Polish).
- **FR-18:** System shall integrate with existing translation dictionary for cross-language ingredient matching.
