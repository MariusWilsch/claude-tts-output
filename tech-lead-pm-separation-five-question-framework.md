# ADR: Adopt Tech Lead + PM Role Separation with 5-Question Deliverable Framework

## Status
**Proposed** | Date: 2025-11-20

## Context

**Solo Operation Scaling Challenge:**
- Operating as solo Tech Lead executing/delegating work across multiple client projects
- Need to maintain technical execution focus while ensuring deliverable visibility
- No formal tracking system for deliverable status across projects
- Onboarding ops person to handle coordination and tracking

**Current State:**
- Deliverable tracking exists informally or in Tech Lead's head
- No standardized way to communicate deliverable status
- Unclear separation of concerns between executor and operator roles

**Business Drivers:**
- Scale solo operation without losing visibility into project status
- Enable Tech Lead to focus on technical decisions and execution
- Provide ops person with clear framework for deliverable tracking
- Maintain big picture across multiple concurrent client projects

## Decision

We will adopt a **Tech Lead + PM role separation** where the Tech Lead focuses on technical execution while the PM (ops person) handles deliverable tracking and coordination using a standardized 5-question framework.

**Implementation Specifics:**

**Role Boundaries:**

| Role | Ownership | Responsibilities |
|------|-----------|------------------|
| **Tech Lead (User)** | What work exists + How it gets done | • Define deliverables from projects<br>• Make technical decisions<br>• Execute work OR delegate to others<br>• Create markdown files with 5-question answers for new deliverables<br>• Provide estimates and communicate blockers |
| **PM (Ops Person)** | Where work stands + What needs attention | • Track deliverable status (open/in-progress/done)<br>• Maintain big picture across all projects<br>• Extract updates via daily sync<br>• Surface blockers to Tech Lead<br>• Add new deliverables to tracking from markdown handoffs |

**5-Question Deliverable Framework:**

Each deliverable must answer (Tech Lead documents in markdown format for async handoff):
1. **What is it?** (Deliverable scope - what needs to be built/delivered)
2. **Why does it matter?** (Value/importance - business justification)
3. **What does "done" mean?** (Definition of done - completion criteria)
4. **Estimated time to complete?** (Time estimate for execution)
5. **Dependencies?** (What or who is needed - resources, people, information)

**Interaction Model:**
- **Daily sync:** Discuss existing deliverable status (progress, blockers, next steps)
- **New deliverables (async):** Tech Lead creates markdown file with 5-question answers, hands off to PM asynchronously
- **PM tracking:** Adds new deliverables from markdown handoffs, maintains centralized view across all projects

**Empirical Validation:**

Framework tested with 2 real deliverables:

**Deliverable #1: 006-Client-Archibus - Dynamic Authentication**
- **What:** Research task transitioning to coding - create dynamic authentication based on user token and bearer token (currently hardcoded in .env) to support multiple users
- **Why:** Preparing for market launch - current hardcoded test user authentication blocks production deployment and customer onboarding
- **Done:** Validated proof of concept demonstrating dynamic authentication working correctly
- **Time:** 2-3 days of focused work
- **Dependencies:** Execution work itself + Rein (API contact on client side for documentation/endpoints/clarifications)

**Deliverable #2: 002-Client-IITR - Client Material Follow-up**
- **What:** Ensuring client provides required materials (meeting recording, final specifications for Navigation format, additional knowledge document, test questions) so project can proceed to implementation
- **Why:** Enables project to actually begin - without these materials implementation cannot start
- **Done:** All materials received from client AND full requirement clarity achieved (judged by Tech Lead)
- **Time:** **OPEN QUESTION** - Client-dependent deliverable doesn't fit "time to complete" model (options: next follow-up date, mark N/A, different tracking approach)
- **Dependencies:** Client (Herr Stellmacher/IITR team) must provide requested materials

## Consequences

### ✅ Positive

**Focused Execution:**
- Tech Lead maintains focus on technical decisions and execution without context-switching to tracking
- Clear boundary: Tech Lead owns "how work gets done," PM owns "where work stands"

**Standardized Communication:**
- 5-question framework provides consistent structure for deliverable documentation
- Every deliverable answers same questions, enabling pattern recognition across projects
- Paragraph-length context (not just keywords) provides sufficient detail for ops tracking

**Empirical Validation:**
- Framework tested with 2 real client deliverables before full ops onboarding
- Concrete examples demonstrate framework applicability to technical work (dynamic auth) and coordination work (client follow-up)

**Scalable Visibility:**
- PM maintains big picture across multiple concurrent projects
- Daily sync extracts updates without Tech Lead maintaining separate tracking system
- Centralized deliverable status prevents "lost in my head" knowledge

### ❌ Negative

**Framework Limitation:**
- Question 4 ("Estimated time to complete?") doesn't fit client-dependency blockers
- Client-waiting deliverables need different tracking (next follow-up date) vs work deliverables (execution time)
- Framework assumes deliverables are execution-controlled, not externally-controlled

**Tracking Adaptation Required:**
- Ops person must distinguish between work deliverables and client-dependency blockers
- No standardized approach yet for "time" tracking on client-waiting tasks
- Framework needs refinement for edge cases discovered during validation

**Daily Sync Overhead:**
- Requires consistent daily check-ins for status extraction
- Tech Lead must context-switch daily to provide updates
- Framework assumes availability for daily sync (may not fit all work patterns)

### ⚪ Neutral

**Ops Person Learning Curve:**
- New hire must learn to distinguish deliverable types (work vs client-waiting)
- PM role requires understanding when to escalate vs track independently
- Framework provides structure but requires judgment in application

**Process Formalization:**
- Shifts from informal tracking (Tech Lead's head) to formalized documentation
- Requires discipline to answer 5 questions for every deliverable
- Trade-off: overhead of documentation vs benefit of visibility

## Alternatives Considered

| Alternative | Rejection Reason |
|-------------|------------------|
| **No Framework (Informal Sync)** | Tested empirically - current informal tracking doesn't scale. Knowledge stays in Tech Lead's head, preventing ops person from maintaining independent big picture. No consistent structure for deliverable communication. |
| **Asana/Jira Project Management Tools** | Overhead of tool maintenance and categorization. Friction of keeping external system updated. Framework provides just enough structure without tool complexity. Prefer human-centric daily sync over tool-centric tracking. |
| **Different Question Count (3 or 7 questions)** | 5 questions emerged from ops person's explicit request. Not arbitrary - comes from real ops tracking needs. Framework already validated with 2 deliverables at this question count. |
| **Tech Lead Tracks Own Deliverables** | Defeats purpose of ops scaling. Tech Lead loses execution focus if maintaining tracking system. Role separation enables specialization - executor vs operator. |

---

**Key Resources:**
- Timing API data used to identify active billable projects for framework validation
- Trial deliverables: 006-Client-Archibus (37.40 hours Oct 1 - Nov 20), 002-Client-IITR (36.19 hours Oct 1 - Nov 20)
- Framework status: Proposed (validating before full ops person onboarding)
