# Authoritative Sources Protocol - Draft

## Why This Exists

Truth comes from verifiable sources. You retrieve knowledge just-in-time from sources that are testable - sources where you can determine if something is true or false, not sources that require interpretation. Authoritative sources are self-updating: they stay current without manual maintenance. This enables ephemeral sessions - you don't depend on work logs or summaries. You discover truth on-demand from sources that are always current.

## The Sources

### Codebase + Docstrings: Technical Truth

The codebase is always current - it's the system's self-updating truth. Code shows what exists, how it works, what's configured. Docstrings capture what's not inherently clear from code itself - context, rationale, non-obvious behavior. When you modify a file, you update its docstring. This keeps the abstract information current alongside the concrete implementation.

### User: Decision Authority

The user knows preferences, priorities, and choices. This is decision authority - only the user can provide it. You retrieve this through AskUserQuestion across all clarity phases. User knowledge doesn't live in documentation - it lives with the user, available when you ask.

### Internet Documentation: External Tool Truth

Official documentation for tools, libraries, and services you use. These sources are self-updating - maintained by the tool creators, always reflecting current versions. You retrieve via Context7 MCP when available, or research agents when not. Links to documentation are more authoritative than copied explanations because they update when the tools update.

## What Is NOT Authoritative

**Work Logs:** Interpretive summaries of what happened. These are your subjective synthesis, not verifiable truth. The next session cannot build reliable understanding from interpretation.

**AI Summaries:** Cannot be tested as true or false. Subjective by nature. Useful for human reading, not for AI continuation.

## Why This Matters

**JIT Knowledge Works:** When truth lives in verifiable sources, you can retrieve it on-demand. You don't need pre-loaded context or session handoff documents. You investigate authoritative sources during clarity phases and build fresh understanding each time.

**Self-Updating Truth:** Codebase changes when the system changes. Documentation updates when tools update. User knowledge is always current because you ask directly. You never work from stale information.

**Testable vs Interpretive:** Authoritative sources provide facts you can verify. Code either has a function or doesn't. Documentation either describes an API or doesn't. User either prefers option A or B. No interpretation needed - just truth discovery.

**Ephemeral Sessions:** You don't carry interpretive summaries between sessions. You start fresh, retrieve truth from authoritative sources, build understanding through investigation. This works because truth persists in reliable sources, not in session memory.
