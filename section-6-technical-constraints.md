## Section 6: Technical Constraints (Technische Rahmen- oder Randbedingungen)

**Understanding:**
- Based on Workshop 2 results document (2025-10-28/29)
- POC hosted at WPH (Wilsch Power Hosting) datacenter
- Production deployment on AVO's IBM Power 10 infrastructure
- Technology decisions for POC implementation phase

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
