# Pflichtenheft

## Kommunale Fördermittel-Suchplattform

---

## Section 1: Cover Page (Deckblatt)

|  |  |
| :---- | :---- |
| **Project** | Kommunale Fördermittel-Suchplattform |
| **Client** | Casa Curata UG GmbH |
| **Contractor** | Wilsch AI Services OÜ |

---

## Section 2: Goal Determination (Zielbestimmung)

### Must (POC Scope)

- Website with landing page for Klimafolgenschutzverein targeting municipalities  
- Interactive questionnaire to capture project details (type, scope, budget, municipality info)  
- AI-powered semantic search of funding databases (starting with one database)  
- Display of relevant funding programs with estimated amounts and percentages (2-3 results)  
- Package-based categorization for standardized projects (digitalization, climate protection, infrastructure)  
- Lead generation flow directing to association membership application  
- Data capture for follow-up consultation

### Deferred (Post-POC)

- Document upload capability (cost estimates, planning documents from architects)  
- Direct funding application submission through platform interface  
- Browser automation for filling external funding forms  
- Detailed personalized consultation and advisory services  
- Integration with EE-Mann (energy efficiency expert) workflow

---

## Section 3: Functional Requirements (Funktionale Anforderungen)

### Must (POC Scope)

**Website with landing page for Klimafolgenschutzverein targeting municipalities**

- **FR-07:** System shall provide informational content about Klimafolgenschutzverein mission and services.

**Interactive questionnaire to capture project details**

- **FR-01:** System shall provide interactive questionnaire to collect project details including type (digitalization, climate protection, infrastructure), scope, budget, and municipality information.

**AI-powered semantic search of funding databases**

- **FR-02:** System shall search one funding database (specific source TBD in Workshop 2\) using semantic matching based on questionnaire inputs.

**Display of relevant funding programs with estimated amounts and percentages**

- **FR-03:** System shall display 2-3 relevant funding programs with estimated amounts, percentage ranges, and program descriptions.

**Package-based categorization for standardized projects**

- **FR-04:** System shall categorize projects into predefined packages (e.g., digitalization small/medium/large, infrastructure, climate measures).

**Lead generation flow directing to association membership application**

- **FR-05:** System shall direct users to association membership application form after displaying funding opportunities.

**Data capture for follow-up consultation**

- **FR-06:** System shall capture and store municipality contact information and identified funding interests for follow-up consultation.

### 

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

## Section 4: Liste der nicht-funktionalen Anforderungen (Non-Functional Requirements)

Non-functional requirements (performance, security, compatibility, and usability specifications) will be defined during Workshop 2.

---

## Section 5: Abnahmekriterien (Acceptance Criteria)

| Requirement ID | Acceptance Test | Expected Outcome |
| :---- | :---- | :---- |
| FR-01 | Given user accesses website, when questionnaire loads | Then all required input fields are displayed and functional |
| FR-02 | Given questionnaire submitted, when search executes | Then funding programs from specified database are returned |
| FR-03 | Given search completes, when results display | Then 2-3 relevant funding programs shown with percentage ranges and amounts |
| FR-04 | Given project details submitted, when categorization executes | Then project is assigned to appropriate package category |
| FR-05 | Given results displayed, when user views page | Then membership application CTA is visible and functional |
| FR-06 | Given user interactions complete, when data capture executes | Then municipality contact info and funding interests are stored |
| FR-07 | Given user accesses landing page, when page loads | Then Klimafolgenschutzverein informational content is displayed |

### Deferred Acceptance Criteria (Post-POC)

| Requirement ID | Acceptance Test | Expected Outcome |
| :---- | :---- | :---- |
| FR-08 | Given user uploads document, when file processing completes | Then document content is extracted and used to enhance search |
| FR-09 | Given funding program selected, when submission initiates | Then application data is transmitted to appropriate portal (BAFA/KfW) |
| FR-10 | Given project requires EE-Mann, when workflow triggers | Then expert validation process is initiated |

---

## Section 6: Technische Rahmen- oder Randbedingungen (Technical Constraints)

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

---

## Section 7: Data Model (Datenmodell) \- SKIPPED

---

## Section 8: Domain Glossary (Glossar / Fachglossar)

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

---

## Section 9: Evaluation Infrastructure (AI-Specific Testing)

### Test Datasets

- 
### Success Metrics

- 
### Input/Output Specifications

- **Input:** Questionnaire responses (structure TBD in Workshop 2\)  
- **Output:** 2-3 funding programs with percentages and amounts (format TBD in Workshop 2\)

### Validation Process

- **Validator:** Casa Curata UG (client) validates AI recommendations during POC  
- **Method:** Client reviews search results based on their funding program knowledge


