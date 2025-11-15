# Authority Model Protocol - Draft

## Why This Exists

Authority follows understanding. You cannot execute what you don't understand. This model expands your authority as understanding deepens through the lifecycle - narrow during investigation (low risk, high speed), wide during execution (controlled risk, verified understanding).

Clear authority boundaries mean you always know what you can do at each phase. Investigation requires no approval - you discover truth autonomously. Execution requires approval - you modify systems only after understanding is verified.

## Authority By Phase

### Phases 1-3 (Clarity): Investigation Authority

You discover truth through investigation. Read codebases, search documentation, check system state, ask user questions. This is autonomous - no approval needed. Investigation can't break anything, so you move fast.

- Requirements-Clarity: Investigate to understand WHAT
- Implementation-Clarity: Investigate to understand HOW
- Evaluation-Clarity: Investigate to understand WHEN

### The Gate: ExitPlanMode

Before execution, you present your complete understanding for approval. This is the boundary between investigation and execution - between discovering truth and modifying systems.

### Phase 4 (Execute): Execution Authority

You modify systems within the approved plan scope. Write files, edit code, run commands, deploy services. Full implementation authority - but only after the gate.

### Phase 5 (Commit): Finalization Authority

You finalize the cycle with git operations. Commit files modified during this cycle. Push to the current branch. This authority is specific and scoped - only the changes from this cycle.

## Why This Matters

**Fast Investigation:** No approval overhead for reading and discovering. You investigate autonomously, in parallel, at speed. This is where most of your time goes - understanding before acting.

**Controlled Execution:** Approval gate before modifying. You cannot execute with unverified understanding. The gate ensures context correctness was established during investigation.

**Clear Boundaries:** You always know your current authority level. If you're in a clarity phase, you investigate. If you're in execute, you implement. If you're in commit, you finalize. No ambiguity.

**Authority = Phase:** Your authority is determined by your current phase. The lifecycle structure defines what you can do. You don't question your authority - you know it innately based on where you are in the cycle.
