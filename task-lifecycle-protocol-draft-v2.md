# Task Lifecycle Protocol - Draft v2

## Why This Exists

Context correctness determines implementation success. When you understand WHAT, HOW, and WHEN (success criteria) before executing, good implementation follows naturally. When understanding diverges, hours are spent debugging misalignment that seconds of clarity would have prevented.

This lifecycle defines clear boundaries for every task - unambiguous start and end points. Clear boundaries enable ephemeral sessions: you can confidently stop at any cycle completion and start fresh, because you always know where one task ends and the next begins.

## Task Boundaries: The Foundation

Every requirement follows the same path:

Requirements-Clarity → Implementation-Clarity → Evaluation-Clarity → Execute → Commit
        ↓                      ↓                        ↓                         ↓
   Confidence ✓          Confidence ✓            Confidence ✓              Next Requirement

**Start:** Requirements-Clarity begins when a requirement is stated.

**End:** Commit completes when changes are finalized.

After commit, you return to the beginning: ready for the next requirement. This is a continuous loop - each cycle completes cleanly, preparing you for the next.

## What Each Phase Represents

### Requirements-Clarity: Shared Understanding of WHAT

Disambiguation resolves ambiguities about what needs to be built. Investigation authority lets you discover truth (codebase, documentation, system state). User authority provides decisions (preferences, choices). Confidence ✓ means the requirement is clear to both of you.

### Implementation-Clarity: Shared Understanding of HOW

Planning identifies the approach, prerequisites, and execution sequence. You verify what exists, what's missing, what needs preparation. Confidence ✓ means the implementation path is clear - no mid-execution surprises.

### Evaluation-Clarity: Shared Understanding of WHEN

Success criteria define what "done" looks like before you build anything. Testable assertions separate what you can verify (logs, outputs, file states) from what requires human judgment (UI correctness, business logic). Confidence ✓ means you both know how to recognize success.

### Execute: Building with Verified Understanding

All ambiguities from the three clarity phases are resolved. You implement within the approved plan scope. No mid-cycle clarification needed - context correctness was established upfront.

### Commit: Cycle Completion

Git operations finalize the changes. This marks the clean boundary - the requirement is complete. You're ready for the next requirement. The cycle can confidently end here.

## Confidence Gating: The Mechanism

Each clarity phase uses binary confidence indicators:

- **✗** = Ambiguities remain (more disambiguation needed)
- **✓** = Shared understanding achieved (ready to proceed)

You cannot proceed past ✗. This isn't optional - it's how the cycle works. Skipping clarity creates the misalignment you'll debug later. Resolving ambiguities upfront is always faster than fixing misunderstood implementation.

## Protocol vs Commands

**This protocol defines:**
- That these five phases exist
- That they occur in this sequence
- That confidence gates control progression
- That commit marks cycle completion
- That cycles loop continuously (commit → next requirement)

**Commands provide:**
- How to conduct requirements disambiguation
- How to plan implementation systematically
- How to define evaluation criteria
- What tools to use at each phase

You don't need commands to know the lifecycle exists. The lifecycle is your operating structure - innate awareness of how work progresses. Commands give you phase-specific expertise within the structure you already understand.

## Why Clear Boundaries Matter

**Ephemeral Sessions:** When every cycle completes at commit, you can stop at 60-70% token usage. Finish the current requirement completely, then end the session. Next session starts fresh with the next requirement. No mid-requirement breaks - you always complete what you start.

**Task Clarity:** You always know: "Where am I in this requirement?" The answer is always one of five phases. You always know: "Is this requirement done?" The answer is: "Has it been committed?"

**Continuous Flow:** After commit, you return to requirements. The cycle loops. One requirement ends, the next begins. Clear boundaries between them.
