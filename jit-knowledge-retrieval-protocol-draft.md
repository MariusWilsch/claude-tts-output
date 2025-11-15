# JIT Knowledge Retrieval Protocol - Draft

## Why This Exists

Knowledge lives in authoritative sources, not session memory. You retrieve truth on-demand when you need it, not in advance. This enables ephemeral sessions - you can finish a cycle, end the session at 60-70% tokens, and start completely fresh next time. No context carried between sessions, no handoff documents, no session memory dependency. Truth persists in sources. You discover it when needed.

## How JIT Works

### Need-Driven Investigation

You investigate when you need to understand, not speculatively. Requirements unclear? Investigate the codebase, documentation, or ask the user. Approach unclear? Investigate prerequisites and dependencies. Verification unclear? Investigate success patterns. Investigation happens during clarity phases - when understanding is needed to reach confidence ✓.

### Fresh Retrieval Each Session

Every session starts fresh. No pre-loaded context. You discover what you need from authoritative sources: read the codebase, check documentation, ask the user. The sources are always current - code reflects the system, docs reflect the tools, user reflects decisions. You build understanding through investigation, not through reading what a previous session thought.

### Understanding Is Disposable

After commit, the understanding you built during clarity phases is disposable. You don't carry it forward. The next requirement starts fresh investigation. This works because truth persists in sources, not in your memory. The codebase still has the code. The user still knows their preferences. Documentation still describes the tools.

## Why This Matters

**Ephemeral Sessions Work:** You can stop confidently at any commit. Finish the current requirement completely, end the session, start fresh next time. The gap doesn't matter - 1 hour or 10 days. You retrieve what you need when you need it.

**Always Current:** You never work from stale information. Every investigation retrieves from self-updating sources. Code changes are immediately visible. Documentation updates reflect new versions. User knowledge is current because you ask directly.

**No Maintenance Burden:** You don't maintain handoff documents, session summaries, or context records. Investigation replaces handoff. Authoritative sources replace interpretive summaries. This scales - the cost doesn't grow with session count.

**Scales With Gaps:** Time between sessions doesn't degrade understanding quality. Fresh retrieval means fresh understanding. 1 hour gap = same investigation quality as 10 day gap. JIT retrieval has no decay - sources stay current, investigation stays effective.
