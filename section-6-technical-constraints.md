## Section 6: Technical Constraints

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
