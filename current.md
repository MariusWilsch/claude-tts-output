## Section 3: Functional Requirements (Funktionale Anforderungen)

**Understanding:**
- Requirements organized by Section 2 goals
- Shows traceability from high-level goals to specific features
- POC focuses on Historical Recipe Cleanup only

### Must (POC Scope)

**Identify duplicate and similar recipes among ~8000 existing recipes**
- **FR-01:** System shall search and compare recipes from database based on ingredient composition and percentage amounts.

**Compare recipes based on ingredient composition and percentages**
- **FR-02:** System shall match ingredients by article number (exact match) and ingredient name (semantic similarity).
- **FR-03:** System shall support hierarchical recipe structures (Vormischungen/pre-mixes) with option to compare at same level or exploded to base ingredients.
- **FR-04:** System shall calculate similarity scores based on percentage differences per ingredient.

**Present similarity rankings to enable manual harmonization decisions**
- **FR-05:** System shall output similarity rankings (not binary yes/no) showing percentage match scores between recipe pairs.
- **FR-06:** System shall export results to Excel format with recipe details and match scores.

**Reduce production complexity by consolidating redundant recipes**
- **FR-07:** System shall filter recipes by special ingredient attributes (VLOG, TK/Tiefkühl, Bio, Halal, Kosher).
- **FR-08:** System shall support ingredient substitutability matching (e.g., grouping Paprika variants, Pfeffer variants).
- **FR-09:** System shall support material group categories (M-prefix purchasing-oriented groups).

**Search based on ingredient names, article numbers, and percentage compositions**
- **FR-10:** System shall allow adjustable similarity tolerance thresholds for percentage-based matching (e.g., 2%, 5%, 10%).
- **FR-11:** System shall validate POC functionality with subset of ~100 recipes before scaling to full ~8000 recipe database.

### Deferred (Post-POC)

**Preventive Duplicate Detection - Enable developers to check new product requests against existing recipe database**
- **FR-12:** System shall provide chat interface for interactive similarity search queries during product request processing.
- **FR-13:** System shall parse PDF documents to extract recipe information from product requests (both searchable and scanned).
- **FR-14:** System shall parse multi-format inputs (free text, English descriptions, quantity unit conversion like "3g/kg" → 0.3%).

**Preventive Duplicate Detection - Support processing of ~7000 annual product requests**
- **FR-15:** System shall enable manual trigger by developer for product request similarity searches (not automatic background processing).

**Preventive Duplicate Detection - Integration into new product request system**
- **FR-16:** System shall integrate with replacement product request system (replacing Lotus Notes).

**Future Enhancements - Multi-language ingredient translation system integration**
- **FR-17:** System shall match ingredients across multiple languages (German, English, Russian, Polish).
- **FR-18:** System shall integrate with existing translation dictionary for cross-language ingredient matching.

**Production Optimization - Batch size and production quantity optimization**
- **FR-19:** System shall calculate optimal batch sizes to minimize partial containers for priority ingredients (TK, Tomatenmark, etc.).
- **FR-20:** System shall adjust recipe quantities within tolerance ranges (±3-10% per ingredient) for full container utilization.

**Production Optimization - Full container utilization optimization**
- **FR-21:** System shall optimize for full container usage of specified priority raw materials.
- **FR-22:** System shall integrate production equipment capacity constraints (batch sizes per mixer type).
