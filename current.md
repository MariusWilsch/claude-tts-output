## Section 2: Goal Determination (Zielbestimmung)

**Understanding:**
- POC focuses on two main use cases: historical recipe cleanup and preventive duplicate checking
- AI provides suggestions, humans make final decisions
- Production optimization is future work post-POC
- System integrates with existing IBM ERP database

### Must (POC Scope)

**Historical Recipe Cleanup:**
- Identify duplicate and similar recipes among ~8000 existing recipes
- Compare recipes based on ingredient composition and percentages
- Present similarity rankings to enable manual harmonization decisions
- Reduce production complexity by consolidating redundant recipes

**Preventive Duplicate Detection:**
- Enable developers to check new product requests against existing recipe database
- Support processing of ~7000 annual product requests
- Manual trigger by developer (not automatic background processing)
- Search based on ingredient names, article numbers, and percentage compositions

### Deferred (Post-POC)

- Batch size and production quantity optimization
- Full container utilization optimization (minimizing partial containers)
- Recipe adjustment automation for production efficiency
- Direct sales team access to similarity search
- Integration into new product request system (replacement of Lotus Notes)
- Multi-language ingredient translation system integration

### Out of Scope

- Automatic recipe merging without human approval
- Automatic specification changes without quality assurance review
- Complete replacement of IBM ERP system
- Sensory/taste prediction capabilities
- Recipe formulation from scratch (only finding existing similar recipes)
