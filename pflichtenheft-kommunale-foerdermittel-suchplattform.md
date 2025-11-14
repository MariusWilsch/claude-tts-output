# Pflichtenheft: Kommunale Fördermittel-Suchplattform

*Hybrid Post-Workshop Documentation for AI-Driven POC Projects*

---

## 1. Cover Page

**Project:** Kommunale Fördermittel-Suchplattform

**Client:** Abtmayr & Reichert GmbH

**Contractor:** Wilsch AI Services OÜ

---

## 2. Goal Determination

### Must (POC Scope)
- Website with landing page for Klimafolgenschutzverein targeting municipalities
- Interactive questionnaire to capture project details (type, scope, budget, municipality info)
- AI-powered semantic search of funding databases (Förderdatenbank, KfW, BAFA, EU sources)
- Display of relevant funding programs with estimated amounts and percentages
- Package-based categorization for standardized projects (digitalization, climate protection, infrastructure)
- Lead generation flow directing to association membership application
- Data capture for follow-up consultation

### Deferred (Post-POC)
- Document upload capability (cost estimates, planning documents from architects)
- Direct funding application submission through platform interface
- Browser automation for filling external funding forms
- Detailed personalized consultation and advisory services
- Integration with EE-Mann (energy efficiency expert) workflow

### Out of Scope
- Custom/niche project types beyond defined standard packages
- On-site consultation visits (replaced by remote/online approach)
- Manual processing of individual edge cases
- Physical distribution materials or regional office setup

### Outstanding Requirements Definition

**Items Requiring Workshop 2 Clarification:**

**Website Scope (MEDIUM Priority):**
- Number of pages and site structure
- Branding assets (logo, colors, style guide)
- Content/copywriting responsibility and approval process
- Design complexity level and reference examples
- Municipality targeting messaging and positioning

**Questionnaire Structure (HIGH Priority):**
- Exact questions and field types (dropdown, text, number)
- Conditional logic and branching rules
- Number of steps/screens in user flow
- Validation requirements and error handling
- Client explicitly stated: "we need to define together"

**Package Categorization (HIGH Priority):**
- Definition criteria (budget ranges, municipality size, employee count)
- Total number of packages to support
- Differentiation fields per package type
- Example packages with concrete specifications
- Currently only conceptual - no detailed specifications provided

**Funding Database Integration (MEDIUM Priority):**
- Integration sequence (all sources at once vs phased approach)
- API availability vs web scraping requirements
- Data freshness and update frequency needs
- Which funding sources are MVP-critical vs nice-to-have

**Lead Data Capture (LOW Priority):**
- Specific form fields required (municipality name, contact, project details)
- Essential vs optional data points
- Storage mechanism and follow-up workflow integration

---

## 3. Functional Requirements

### Must (POC Scope)

**Website with landing page for Klimafolgenschutzverein targeting municipalities**
- **FR-07:** System shall provide informational content about Klimafolgenschutzverein mission and services.

**Interactive questionnaire to capture project details**
- **FR-01:** System shall provide interactive questionnaire to collect project details including type (digitalization, climate protection, infrastructure), scope, budget, and municipality information.

**AI-powered semantic search of funding databases**
- **FR-02:** System shall search one funding database (specific source TBD in Workshop 2) using semantic matching based on questionnaire inputs.

**Display of relevant funding programs with estimated amounts and percentages**
- **FR-03:** System shall display 2-3 relevant funding programs with estimated amounts, percentage ranges, and program descriptions.

**Package-based categorization for standardized projects**
- **FR-04:** System shall categorize projects into predefined packages (e.g., digitalization small/medium/large, infrastructure, climate measures).

**Lead generation flow directing to association membership application**
- **FR-05:** System shall direct users to association membership application form after displaying funding opportunities.

**Data capture for follow-up consultation**
- **FR-06:** System shall capture and store municipality contact information and identified funding interests for follow-up consultation.

### Deferred (Post-POC)

**Document upload capability**
- **FR-08:** System shall accept document uploads (cost estimates, planning documents) for enhanced funding search precision.

**Direct funding application submission through platform interface**
- **FR-09:** System shall enable direct submission of funding applications to BAFA/KfW portals on behalf of municipalities.

**Integration with EE-Mann (energy efficiency expert) workflow**
- **FR-10:** System shall integrate with EE-Mann workflow for projects requiring expert validation.

### Functional Requirement Dependencies

**FR-02 depends on FR-01**
- Questionnaire (FR-01) collects structured project parameters that the AI semantic search (FR-02) uses to query funding databases effectively.

**FR-03 depends on FR-02**
- Search must complete (FR-02) and return results before the system can display funding programs (FR-03) to the user.

**FR-04 depends on FR-01**
- Package categorization (FR-04) uses project details from questionnaire (FR-01) to classify the project into predefined standardized offerings.

**FR-05 depends on FR-03**
- User must first see funding opportunities (FR-03) before being directed to membership application (FR-05) as part of lead generation flow.

**FR-06 depends on FR-01, FR-03**
- Data capture (FR-06) stores both questionnaire inputs (FR-01) and which funding results (FR-03) the user viewed for follow-up consultation purposes.

**FR-09 depends on FR-08** (Deferred)
- Document uploads (FR-08) provide the detailed cost data needed to pre-fill direct application submissions (FR-09) to funding portals.

---

## 4. Non-Functional Requirements

### Performance
- *To be defined in Workshop 2*

### Security
- *To be defined in Workshop 2*

### Compatibility
- *To be defined in Workshop 2*

### Usability
- *To be defined in Workshop 2*

### Outstanding Non-Functional Requirements (Require Workshop 2 Definition)

The following NFRs need quantification and validation:
1. **Availability/Uptime:** Required system availability percentage (e.g., 99.5% uptime?)
2. **Scalability Target:** Peak concurrent users to support (50? 100? 500?)
3. **Data Retention:** How long to store captured municipality data
4. **Response Time SLAs:** Acceptable latency for each user interaction
5. **Browser/Device Support:** Specific versions and device types to support

---

## 5. Acceptance Criteria

**FR-01:** Given user accesses website, when questionnaire loads, then all required input fields are displayed and functional

**FR-02:** Given questionnaire submitted, when search executes, then funding programs from specified database are returned

**FR-03:** Given search completes, when results display, then 2-3 relevant funding programs shown with percentage ranges and amounts

**FR-04:** *To be defined in Workshop 2 - Package categorization logic requires definition*

**FR-05:** Given results displayed, when user views page, then membership application CTA is visible and functional

**FR-06:** Given user interactions complete, when data capture executes, then municipality contact info and funding interests are stored

**FR-07:** Given user accesses landing page, when page loads, then Klimafolgenschutzverein informational content is displayed

### Deferred Acceptance Criteria (Post-POC)

**FR-08:** Given user uploads document, when file processing completes, then document content is extracted and used to enhance search

**FR-09:** Given funding program selected, when submission initiates, then application data is transmitted to appropriate portal (BAFA/KfW)

**FR-10:** Given project requires EE-Mann, when workflow triggers, then expert validation process is initiated

### Outstanding Acceptance Criteria (Require Workshop 2 Definition)

The following criteria require detailed specification:
1. **FR-01 Questionnaire:** Specific fields, validation rules, error handling scenarios
2. **FR-04 Package Categorization:** Classification logic and package definitions
3. **FR-02 Search Relevance:** What constitutes a "relevant" funding match?
4. **FR-03 Result Sorting:** How should 2-3 programs be prioritized/sorted?
5. **FR-06 Data Storage:** What specific fields are captured and stored?

---

## 6. Technical Constraints

### Deployment Environment
- **Backend:** Hetzner server (Frankfurt datacenter)
- **Frontend:** Vercel platform
- Cloud-based architecture with separation of concerns

### Required Integrations
- Initial integration with one funding database (specific source TBD in Workshop 2: Förderdatenbank, KfW, or BAFA)
- Integration method to be determined in Workshop 2 (API access vs web scraping)
- Additional databases deferred to post-POC

### Technology Stack Decisions
- **Backend Framework:** FastAPI (Python)
- **Frontend Framework:** React
- **Database:** Supabase (for municipality contact data and search results storage)
- **Deployment:** Backend on Hetzner, Frontend on Vercel
- **API Communication:** REST API between React frontend and FastAPI backend
- **Authentication:** No user authentication required for POC (public access for municipalities)

### Outstanding Technical Constraints (Require Workshop 2 Definition)

The following technical decisions need clarification:
1. **Primary Funding Database:** Which database to integrate first (Förderdatenbank, KfW, or BAFA)?
2. **Integration Method:** API access vs web scraping vs hybrid approach for funding databases

---

## 7. Data Model - SKIPPED

*This section is skipped as database schema is an implementation detail to be decided during development.*

---

## 8. Domain Glossary

### Key Terms

**Fördermittel**
- Government subsidies or grants provided to municipalities for public projects.

**Förderdatenbank**
- Central German database containing information about available funding programs from various sources.

**Gemeinde**
- Municipality or local government entity in Germany.

**KfW (Kreditanstalt für Wiederaufbau)**
- German state-owned development bank providing subsidized loans and grants for infrastructure and climate projects.

**BAFA (Bundesamt für Wirtschaft und Ausfuhrkontrolle)**
- Federal Office for Economic Affairs and Export Control, manages various funding programs.

**EE-Mann (Energieeffizienz-Experte)**
- Energy efficiency expert required to validate and approve certain climate/building projects for funding eligibility.

**Klimafolgenschutzverein**
- Climate Impact Protection Association (client organization), supports municipalities in accessing climate-related funding.

**Bürgermeister**
- Mayor of a municipality, key decision-maker for project approvals.

**Kämmerer**
- Municipal treasurer, responsible for financial planning and budget management.

**Digitalisierung**
- Digitalization of municipal administrative processes and services.

### Outstanding Terminology (Require Workshop 2 Definition)

The following terms are referenced but not yet formally defined:
1. **Paket / Package:** What constitutes a standardized project package (e.g., "Digitalisierungspaket klein/mittel/groß")?
2. **Package Categories:** Specific categorization criteria for different package types (digitalization, infrastructure, climate measures).

---

## 9. Evaluation Infrastructure

### Test Datasets
- *To be defined in Workshop 2*

### Success Metrics
- *To be defined in Workshop 2*

### Input/Output Specifications
- **Input:** Questionnaire responses (structure TBD in Workshop 2)
- **Output:** 2-3 funding programs with percentages and amounts (format TBD in Workshop 2)

### Validation Process
- **Validator:** Abtmayr & Reichert (client) validates AI recommendations during POC
- **Method:** Client reviews search results based on their funding program knowledge

### Outstanding Evaluation Requirements (Require Workshop 2 Definition)

The following evaluation infrastructure needs definition:
1. **Test Dataset Creation:** Sample municipality projects with known correct funding matches
2. **Success Metrics:** Definition of "successful" funding program match (precision, relevance criteria)
3. **Acceptance Threshold:** Required accuracy level for POC approval
4. **Feedback Loop:** Process for collecting and incorporating validation feedback
