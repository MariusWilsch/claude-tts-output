# What is BLOOM?

BLOOM is an open-source framework that automatically generates behavioral evaluations for AI models.

**Core Function:** Takes a researcher-specified behavior and quantifies how often and how severely it appears across dynamically generated test scenarios.

## What Does BLOOM Offer?

### Automated Evaluation Pipeline
- **Understanding** - Analyzes behavior descriptions
- **Ideation** - Generates test scenarios
- **Rollout** - Simulates interactions to trigger behaviors
- **Judgment** - Scores responses for behavior presence/severity

### Key Benefits
- **Speed:** Replaces months of manual evaluation work
- **Accuracy:** 0.86 correlation with human judgment (Claude Opus 4.1)
- **Reproducibility:** Consistent results across runs
- **Flexibility:** Configurable for any behavioral trait

### Real-World Applications
Early adopters use BLOOM to evaluate:
- Jailbreak vulnerabilities
- Evaluation awareness
- Sabotage behaviors
- Model hardcoding

---

# What is Petri?

Petri is BLOOM's complementary tool for broader behavioral exploration.

**Purpose:**
- Explores overall behavioral profiles of AI models
- Surfaces new, previously unknown misaligned behaviors
- Provides general auditing vs BLOOM's targeted evaluation

## BLOOM vs Petri

| BLOOM | Petri |
|-------|-------|
| Targeted evaluation | Broad exploration |
| Measures specific behaviors | Discovers new behaviors |
| In-depth analysis | Profile overview |
| "How bad is X behavior?" | "What behaviors exist?" |

---

# Connection to Our Learning System

## Direct Synergies

### 1. Validation Pipeline
- **BLOOM:** Measures if AI behavior matches expected patterns
- **Our System:** Needs to validate if learning actually improved behavior
- **Integration:** Use BLOOM to verify learning effectiveness

### 2. Behavior Change Detection
- **BLOOM:** Quantifies behavioral traits with precision (0.86 correlation)
- **Our System:** Changes AI behavior through user corrections
- **Integration:** BLOOM measures the effectiveness of behavioral changes

### 3. Safety Guardrails
- **BLOOM:** Detects problematic behaviors (deception, sabotage)
- **Our System:** Risk of learning bad behaviors from corrections
- **Integration:** BLOOM ensures learning doesn't create misalignment

## Practical Integration

### Before/After Learning Validation:

```
User Correction → Learning Applied → BLOOM Evaluation → Behavior Change Confirmed
```

### Quality Assurance Process:
- Run BLOOM on AI before and after learning sessions
- Ensure learning improves desired traits without safety degradation
- Quantify improvement effectiveness systematically

### Enhanced Data Flywheel:
- Our learning creates behavioral changes
- BLOOM measures those changes systematically
- Better measurement improves learning algorithms

## Strategic Value

BLOOM solves our validation problem: "How do we know our learning actually works?"

Instead of relying on "silence = success", BLOOM provides:
- Quantitative improvement measurement
- Safety regression detection
- Systematic learning effectiveness scoring

---

# Bottom Line

- **BLOOM** = Targeted behavior measurement tool
- **Petri** = General behavior discovery tool
- **Our System** = Behavior adaptation tool

**Together:** We adapt AI behavior, BLOOM validates it worked correctly.

**Symbiotic relationship:** Validated adaptive AI that measurably improves over time.
