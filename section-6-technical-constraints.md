## Section 6: Technical Constraints (Technische Rahmen- oder Randbedingungen)

**Understanding:**
- Deployment constraints from client infrastructure
- Integration points to existing systems
- Technology decisions for POC phase

### Deployment Environment

**POC Phase:**
- External hosting with VPN tunnel access
- Web service deployment model
- Data provided via XML export from client database

**Production Phase:**
- On-premise deployment on IBM Power 10 server
- Hardware: 8 CPU cores, 512GB RAM
- Operating system: IBM i (AIX)
- Network: Internal client network access

### Required Integrations

**Database Integration:**
- IBM AS/400 / IBM i system with DB2 database
- Data access: XML export (POC), JDBC connectivity (production - FR-26)
- ~8000 recipes in existing database structure

**Output Integration:**
- Excel-compatible export format for results
- Integration with existing ERP system workflows

**Legacy Systems:**
- LIMS system (specification management)
- Lotus Notes/Domino (current product request system - to be replaced in FR-16)

### Technology Stack Decisions

**Backend [TBD with Thomas Erhard]:**
- Preferred: FastAPI (Python)
- Constraint: IBM Power processor compatibility to be verified
- Alternative: Node.js (confirmed compatible with IBM i infrastructure)

**AI/ML Framework [TBD]:**
- Framework selection during implementation phase
- Must support similarity algorithm requirements (FR-02, FR-02a, FR-04, FR-08)

**Data Processing:**
- Batch processing for metadata file generation (FR-27)
- Support for hierarchical recipe structure processing (FR-03)

**Client Infrastructure Context:**
- Existing: RPG, Java, Profound UI
- Database: DB2 on IBM i
- Python support on IBM i: To be verified with infrastructure team

---

**Action Items:**
- Verify FastAPI/Python deployment compatibility on IBM Power 10 with Thomas Erhard
- Confirm JDBC connectivity requirements for production phase
- Define batch processing schedule for metadata updates
