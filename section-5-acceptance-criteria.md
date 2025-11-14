## Section 5: Acceptance Criteria (Abnahmekriterien)

**Understanding:**
- Acceptance criteria link to POC scope functional requirements only
- Deferred requirements will have acceptance criteria defined when implemented
- Format: Given-When-Then or binary pass/fail criteria

| Requirement ID | Acceptance Test | Expected Outcome |
|----------------|-----------------|------------------|
| FR-02 | Given two recipes with shared Material_IDs, when comparison is executed | System identifies all exact Material_ID matches between recipes |
| FR-02a | Given Recipe A (20 ingredients) and Recipe B (10 ingredients) with 8 shared ingredients, when overlap ratio is calculated | System returns overlap ratio of 0.40 (8/20 using MAX normalization) |
| FR-04 | Given matched ingredient with 5.2% in Recipe A and 5.8% in Recipe B, when percentage similarity is calculated | System calculates similarity score based on percentage difference |
| FR-08 | Given unmatched ingredients from two recipes, when resource category comparison is executed | System identifies and flags ingredient pairs sharing same Rohstoffkategorie |
| FR-05 | Given comparison of Recipe A against all recipes in database, when similarity search completes | System outputs ranked list of similar recipes with percentage match scores (not binary yes/no) |
| FR-06 | Given completed similarity analysis results, when export is requested | System generates Excel file containing recipe pairs, match scores, and ingredient details |
| FR-11 | Given POC subset of 100 recipes, when validation tests are executed | System successfully completes all comparison operations without errors before scaling to full database |

---

**Note:** Acceptance criteria for deferred requirements (FR-07, FR-10, FR-12, FR-13, FR-14, FR-15, FR-16, FR-17, FR-18, FR-19, FR-20, FR-21, FR-22, FR-23, FR-24, FR-25, FR-26, FR-27) will be defined during their respective implementation phases.
