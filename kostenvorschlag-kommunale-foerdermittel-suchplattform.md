# Kostenvorschlag (Richtpreisangebot)

## Kommunale Fördermittel-Suchplattform

| | |
|---|---|
| **Project** | Kommunale Fördermittel-Suchplattform |
| **Client** | Abtmayr & Reichert GmbH |
| **Contractor** | Wilsch AI Services OÜ |
| **Document Type** | Richtpreisangebot (Indicative Pricing Proposal) |
| **Date** | 2025-11-15 |

---

## Introduction

This document provides effort estimates for the POC scope of the Kommunale Fördermittel-Suchplattform project, as defined in the accompanying Pflichtenheft. Estimates are provided in days (8-hour workdays) assuming a solo senior full-stack developer. Items with dependencies on Workshop 2 clarification are shown as ranges to account for specification uncertainty.

---

## Effort Estimates

### Functional Requirements

**FR-01 + FR-06: Interactive Questionnaire & Data Capture**

*Requirements:*
- *FR-01: System shall provide interactive questionnaire to collect project details including type (digitalization, climate protection, infrastructure), scope, budget, and municipality information.*
- *FR-06: System shall capture and store municipality contact information and identified funding interests for follow-up consultation.*

**Effort Estimate: 1.5 days**

**Sub-task Breakdown:**
- Form builder tool configuration and setup: 0.5 day
  - Configure form fields, conditional logic, validation
  - Set up branding and user flow
  - Configure webhook integration

- Backend webhook integration and data storage: 1 day
  - Receive form submissions via webhook
  - Data validation and sanitization
  - Store questionnaire data in Supabase
  - Session tracking (cookie/localStorage) to link submissions with search results
  - Associate funding programs viewed with user session for follow-up
  - Form redirect to results page after submission

*Decision: Using form builder tool (Fillout/Typeform/similar) embedded via iframe instead of custom React component to reduce POC development time and enable flexible iteration. Simple session-based tracking without user authentication.*

---

**FR-02: AI-Powered Semantic Search**

*Requirement: System shall search one funding database (specific source TBD in Workshop 2) using semantic matching based on questionnaire inputs.*

**Effort Estimate: 6-7 days**

**Sub-task Breakdown:**
- Funding database scraper and data ingestion: 3-4 days
  - Build web scraper for funding database (specific source TBD)
  - Extract program details (title, description, amounts, eligibility)
  - Data cleaning and normalization
  - Initial load of ~50-100 programs
  - *Range accounts for database structure complexity and dynamic content handling*

- Typesense integration and semantic search: 2 days
  - Set up embedding model (self-hosted or cloud-hosted)
  - Configure Typesense vector search
  - Generate and index embeddings for funding programs
  - Implement semantic query processing and relevance scoring

- Backend API endpoints: 1 day
  - POST endpoint to receive search queries from questionnaire
  - Process questionnaire data into search parameters
  - Query Typesense and return ranked results
  - Error handling and logging

*Note: Estimate assumes small sample dataset (~50-100 programs). Database selection in Workshop 2 will determine scraping complexity.*

---

**FR-03: Display Funding Programs**

*Requirement: System shall display 2-3 relevant funding programs with estimated amounts, percentage ranges, and program descriptions.*

**Effort Estimate: 1.5-2 days**

**Sub-task Breakdown:**
- Frontend results display component (React): 1-1.5 days
  - Results card/list layout design
  - Display program title, description, amounts, percentage ranges
  - Responsive design for desktop and mobile
  - Loading states and error handling

- Backend result formatting: 0.5 day
  - Format search results for frontend consumption
  - Calculate/estimate funding amounts and percentages
  - Limit results to top 2-3 matches
  - Add metadata (source, eligibility summary)

*Note: Assumes standard UI components. Does not include advanced filtering or sorting beyond top 2-3 results.*

---

**FR-05 + FR-07: Landing Page & Lead Generation Flow**

*Requirements:*
- *FR-07: System shall provide informational content about Klimafolgenschutzverein mission and services.*
- *FR-05: System shall direct users to association membership application form after displaying funding opportunities.*

**Effort Estimate: 3.5-4.5 days**

**Sub-task Breakdown:**
- Landing page implementation (React): 3-4 days
  - Hero section with value proposition and CTA
  - "How it works" process flow (3-4 steps)
  - About Klimafolgenschutzverein section
  - Trust indicators/benefits for municipalities
  - Responsive layout (desktop/tablet/mobile)
  - Clean modern design using component library (MUI/Chakra/similar)
  - Placeholder images throughout

- Lead generation CTA integration: 0.5 day
  - CTA buttons throughout page flow
  - Link to client-provided membership application
  - Consistent design and messaging

*Note: Assumes Workshop 2 delivers content/copy and branding guidelines. Uses placeholder images and simple/static design (no animations or SEO optimization for POC). Component library for faster development.*

---

### Infrastructure & Deployment

**Infrastructure & Deployment Setup**

**Effort Estimate: 2-3 days**

**Sub-task Breakdown:**
- Backend infrastructure (FastAPI on Hetzner): 1-1.5 days
  - FastAPI project scaffolding and configuration
  - Typesense Docker container deployment on Hetzner
  - Environment variables and secrets management
  - CORS and security configuration
  - Manual deployment process documentation

- Frontend infrastructure (React on Vercel): 0.5-1 day
  - React project setup with build configuration
  - shadcn/ui component library integration
  - Vercel deployment configuration
  - Environment variables for API endpoints
  - Manual deployment process

- Database setup (Supabase): 0.5 day
  - Supabase project creation and configuration
  - Initial schema setup for lead data and search results
  - Connection configuration for backend
  - Basic row-level security policies

*Note: Assumes Hetzner server already provisioned. Uses Docker for Typesense deployment. Manual deployment for POC (no CI/CD automation).*

---

### Testing & Evaluation

**Testing & Evaluation Infrastructure**

**Effort Estimate: 1-1.5 days**

**Sub-task Breakdown:**
- Test dataset creation: 0.5 day
  - Create 10-20 sample municipality project scenarios
  - Document expected funding program matches for each scenario
  - Cover different project types (digitalization, climate, infrastructure)

- Functional testing: 0.5-1 day
  - Test questionnaire submission → search → results display flow
  - Verify web page functionality (forms, navigation, responsiveness)
  - Cross-browser testing (Chrome, Firefox, Safari)
  - Mobile device testing
  - Basic error handling verification

*Note: Manual testing approach for POC. Test dataset enables client to validate search relevance by filling questionnaire and reviewing results. Does not include automated testing framework or performance testing.*

---

### Documentation

**Documentation Deliverables**

**Effort Estimate: 1-1.5 days**

**Sub-task Breakdown:**
- Technical documentation: 0.5-1 day
  - API documentation (endpoints, request/response formats)
  - Deployment process documentation
  - Environment setup guide
  - Database schema documentation
  - Basic troubleshooting guide

- User guide: 0.5 day
  - How to use the platform (filling questionnaire, understanding results)
  - Simple FAQ section
  - Guide for municipalities accessing the platform

*Note: Focuses on development handoff and basic user guidance. Operational/maintenance documentation TBD in Workshop 2. Does not include comprehensive system architecture diagrams or video tutorials.*

---

### Workshop 2 Preparation

**Workshop 2 Facilitation - Requirements Definition**

**Total Estimated Effort: 2.5-3 days**

**Element Breakdown:**

**1. Questionnaire Structure Definition** — **0.25-0.375 day**
- Facilitate questionnaire design session (1-2 hours)
- Document detailed specification (1 hour with AI)
- Deliverable: Field inventory, conditional logic, validation rules

**2. Content & Copywriting** — **0.25 day**
- Facilitate content/messaging session (1 hour)
- Create content outline with AI (~30-60 min)
- Deliverable: Landing page content outline (hero, about, how it works)

**3. Branding Guidelines** — **0.125 day**
- Branding review session (30 minutes)
- Document style guide (30 minutes)
- Deliverable: Logo files, color palette, font specifications

**4. Funding Database Selection** — **1.125 days**
- Pre-workshop database research (1 day)
  - Technical evaluation of Förderdatenbank, KfW, BAFA, and others
  - API availability and documentation review
  - Web scraping difficulty assessment
  - Create comparison matrix
- Workshop presentation and documentation (1 hour)
  - Present findings and recommendation
  - Document client selection and rationale

**5. Package Categorization** — **0.5 day**
- Facilitate package definition session (2 hours)
- Document package specifications (1-2 hours)
- Deliverable: Package list with categorization rules and criteria
- Note: Implementation deferred to post-POC

**6. Non-Functional Requirements & Evaluation Criteria** — **0.25 day**
- Combined NFRs + evaluation criteria session (1 hour)
- Documentation (1 hour)
- Deliverable: Minimal NFR notes (TBD for post-POC) and evaluation criteria specification

*Note: Single on-site multi-day workshop format (client travels to your location). Estimates include facilitation and documentation only, no preparation time. Workshop 2 deliverables enable POC implementation by defining all outstanding Pflichtenheft requirements.*

---

## Summary

**Total Estimated Effort: 19.5-24 days**

### Effort Breakdown by Category

| Category | Effort Estimate | Notes |
|----------|----------------|-------|
| **Functional Requirements** | **12.5-15 days** | |
| FR-01 + FR-06: Questionnaire & Data Capture | 1.5 days | Form builder tool + webhook integration |
| FR-02: AI-Powered Semantic Search | 6-7 days | Database scraping + Typesense + embeddings |
| FR-03: Display Funding Programs | 1.5-2 days | Results display component |
| FR-05 + FR-07: Landing Page & Lead Generation | 3.5-4.5 days | Full landing page + CTA integration |
| **Infrastructure & Deployment** | **2-3 days** | Backend, frontend, database setup |
| **Testing & Evaluation** | **1-1.5 days** | Test dataset + manual testing |
| **Documentation** | **1-1.5 days** | Technical docs + user guide |
| **Workshop 2 Facilitation** | **2.5-3 days** | Requirements definition + documentation |
| **TOTAL POC EFFORT** | **19.5-24 days** | |

### Key Assumptions

**Technical Stack:**
- Form builder tool (Fillout/Typeform) for questionnaire
- Self-hosted embedding model or cloud-hosted
- Typesense for vector search (Docker on Hetzner)
- FastAPI backend on Hetzner server (already provisioned)
- React frontend with shadcn/ui on Vercel
- Supabase for database
- Manual deployment (no CI/CD)

**Scope Clarifications:**
- Small sample dataset (~50-100 funding programs)
- Generic funding database estimate (specific source TBD in Workshop 2)
- Placeholder images and simple/static design for POC
- Manual testing approach (no automated testing framework)
- Workshop 2 is separate on-site engagement (client travels to you)

**Deferred to Post-POC:**
- FR-04: Package categorization (implementation only - definition in Workshop 2)
- Advanced features (document upload, direct application submission, EE-Mann integration)
- CI/CD pipeline automation
- Performance and load testing
- Comprehensive SEO optimization

**Document Type:** Richtpreisangebot (Indicative Pricing Proposal) - Non-binding estimate based on current understanding. Final effort may vary based on Workshop 2 outcomes and implementation discoveries.
