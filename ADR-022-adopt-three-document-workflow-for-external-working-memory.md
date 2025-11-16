# ADR-022: Adopt Three-Document Workflow as External Working Memory for Multi-Project Engagement

## Status
**Proposed** | Date: 2025-11-16

## Context

**Business Model: Solo Freelancer Managing Concurrent Projects**
- Multiple client engagements running simultaneously
- Constant context switching between projects
- Cannot hold all project details in working memory
- Need systematic way to preserve and retrieve project context

**Workshop Transcript Problem:**
- Workshops produce valuable client discussions captured in transcripts
- Decisions buried in noise: "we decided" looks the same as "we discussed"
- When context needed days/weeks later (proposals, POC development, teammate briefing)
- Forced to re-read hour-long transcripts: 30-60 minutes per context switch
- This is expensive and doesn't scale with multiple concurrent projects

**Transformation Model:**
```
Workshop Transcript = Ore (signal + noise mixed together)
        ↓
Pflichtenheft = Refined Metal (pure decisions, organized, reusable)
        ↓
Outputs = Products (proposals, POC development, documentation)
```

**Missing Systematic Process:**
- Need standardized way to extract workshop decisions
- Need technical scoping that serves both pricing and development
- Need cross-session AI context (when starting new session, need foundational context)
- Ad-hoc approach leads to re-reading transcripts or missing critical decisions

**Strategic Driver:**
- Create "20% foundational context that frames the other 80%"
- Enable 5-minute context retrieval instead of 30-60 minute transcript re-reading
- Single source of truth for multiple downstream uses

---

## Decision

We will mandate a **three-document transformation workflow** where workshop transcripts are systematically refined into reusable artifacts that serve as external working memory.

**Implementation Specifics:**

**Document 1: Pflichtenheft (Decision Extraction Machine)**
- Converts workshop chaos into organized decisions
- Separates "we decided" from "we discussed"
- Uses direct quotes from workshop transcripts as evidence
- Organized by topic (not chronological like transcripts)
- Must be accepted before work begins (German standard compliance)
- Created AFTER Workshop 2 (converts Lastenheft client requirements → implementation approach)

**Document 2: Internal Scoping Document**
- Technical breakdown of functional requirements into sub-tasks
- Effort estimates in days (8-hour workdays) assuming solo senior developer
- Dual purpose: basis for pricing calculation + blueprint for development
- Documents technical stack, assumptions, and implementation decisions
- Not client-facing (internal technical detail)
- Created from Pflichtenheft requirements

**Document 3: Client Offer**
- Business proposal converting scoping document into client-facing format
- Two types based on information completeness:
  - **Richtpreisangebot** (Indicative Pricing) - Non-binding estimate after Workshop 1
  - **Festpreisangebot** (Fixed-Price Offer) - Binding proposal after Workshop 2 + detailed scoping
- Includes business value, deliverables, milestones, success criteria, pricing (EUR)

**Two Entry Points:**

| Entry Point | Pflichtenheft | Scoping Detail | Offer Type |
|-------------|---------------|----------------|------------|
| **Workshop 1** | Limited/rough | Rough estimates | Richtpreisangebot (indicative) |
| **Workshop 2** | Comprehensive | Detailed breakdown | Festpreisangebot (binding) |

**Cross-Session AI Context:**
- All three documents serve as standardized context for AI agents in new sessions
- Pflichtenheft: WHAT was decided
- Scoping Document: HOW MUCH EFFORT to implement
- Offer: BUSINESS TERMS agreed with client

---

## Consequences

### ✅ Positive

**External Working Memory:**
- Creates "20% foundational context that frames the other 80%"
- Reduces context retrieval from 30-60 min (re-reading transcripts) to 5 min (reading documents)
- Enables effective management of multiple concurrent projects

**Single Source, Multiple Uses:**
- One Pflichtenheft enables: proposals, POC development, teammate briefing, AI handoff
- Prevents duplicated effort across different downstream activities
- "When I look at this in two months, I still know what we got out of the workshop"

**Evidence-Backed Decisions:**
- Direct quotes from workshop transcripts prove decisions
- Prevents "he-said-she-said" misunderstandings
- Organized by topic (not chronological) for fast reference

**Systematic Proposal Generation:**
- Standardized process for creating both indicative and binding offers
- Repeatable workflow across all client engagements
- Quality consistency across proposals

**Cross-Session AI Context:**
- New AI sessions can immediately understand project fundamentals
- Reduces onboarding overhead for AI assistance
- Enables effective handoff between sessions

### ❌ Negative

**Documentation Overhead:**
- Requires upfront effort to create all three documents
- Additional time investment vs direct-to-offer approach
- Must be maintained and updated if requirements change

**Discipline Required:**
- Need systematic execution to maintain all three documents
- Risk of documents becoming stale if not updated
- Requires commitment to documentation process

### ⚪ Neutral

**Process Change:**
- Requires standardizing workflow across all engagements
- Learning curve for new team members or partners
- Need to educate clients on document purposes

**German Standard Compliance:**
- Pflichtenheft acceptance before work begins
- Aligns with industry standard practice
- May seem bureaucratic to some clients

---

## Alternatives Considered

| Alternative | Rejection Reason |
|-------------|------------------|
| **Direct-to-Offer (skip Pflichtenheft and Scoping)** | Loses workshop decisions, forces transcript re-reading for each context switch, no development blueprint |
| **Pflichtenheft Only (skip Scoping Document)** | Missing technical breakdown needed for pricing and development guidance, can't systematically create offers |
| **Ad-Hoc Documentation (create documents as needed)** | Inconsistent quality, context retrieval still expensive, not reusable across sessions or team members |
| **Transcript Summaries (AI-generated summaries)** | Still mixes decisions with discussions, not organized by topic, lacks evidence (direct quotes), not structured for downstream use |

---

**Key Resources:**
- Example POC Offer: `docs/pricing-framework/examples/POC-Offer-Document-AVO.pdf`
- Example Richtpreisangebot: `docs/pricing-framework/examples/Richtpreisangebot-Produktionssystem-Erweiterungen.pdf`
- Example Pflichtenheft: `docs/pflichtenheft-kommunale-foerdermittel-suchplattform.md`
- Example Scoping Document: `docs/kostenvorschlag-kommunale-foerdermittel-suchplattform.md`
