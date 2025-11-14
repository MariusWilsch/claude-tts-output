## Section 5: Acceptance Criteria (Abnahmekriterien)

**Understanding:**
- Acceptance criteria link to POC scope functional requirements only
- Deferred requirements will have acceptance criteria defined when implemented
- Format: Given-When-Then or binary pass/fail criteria

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

**Note:** Acceptance criteria for deferred requirements (FR-07, FR-10, FR-12, FR-13, FR-14, FR-15, FR-16, FR-17, FR-18, FR-19, FR-20, FR-21, FR-22, FR-23, FR-24, FR-25, FR-26, FR-27) will be defined during their respective implementation phases.
