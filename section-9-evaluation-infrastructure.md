## Section 9: Evaluation Infrastructure (Evaluierungsmethodik)

**Understanding:**
- Validation methodology defined in Workshop 2
- Test dataset with known duplicates as baseline
- Iterative refinement based on AVO review

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
