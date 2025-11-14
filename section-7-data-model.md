## Section 7: Data Model (Datenmodell)

**Understanding:**
- Metadata file structure defined in Workshop 2
- Complete column definitions documented in Excel deliverable
- No duplication needed - reference external documentation

### Metadata Table Structure

The POC uses a denormalized metadata file containing flattened recipe data. Key transformations:

- Hierarchical Baukasten structure → single-level table
- Relative quantities normalized to 100% per manufacturing instruction
- DIA-LIMS data integrated per ingredient

**Complete column structure:** See "AVO_WS2_Tabellenstruktur Meta-Datei_20251108.xlsx" (Workshop 2 deliverable)

**Source:** IBM AS/400 / IBM i (DB2)  
**Format:** IBM Save-File (*SAVF)  
**Update:** Batch processing (cycle TBD with AVO)
