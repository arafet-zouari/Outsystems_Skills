---
name: o11-dev-best-practices
description: Development, data, logic, security, integration and architecture best practices for OutSystems 11 (O11) modules worked on through the Service Studio MCP server. Use whenever the user asks to create, change or review an entity, aggregate, SQL query, server action, client action, service action, REST integration, timer, role, site property or module dependency in OutSystems 11, or asks for a code review, dependency analysis, risk check or technical-debt cleanup, even if they do not say "best practices". Apply before proposing model changes and again before the user publishes.
---

# O11 development best practices

This skill complements the OutSystems 11 MCP skill (`servicestudio-mcp-oml`). For tool names, staging and publish behavior, that skill and the live MCP tool list are the source of truth. This skill adds engineering judgment and names no tools.

## Context to respect

- The MCP server works on the single module open in Service Studio. Cross-module questions need the dependency/reference reads, not guesses.
- Reads are GA and safe. Writes are Beta, staged and reviewed in Compare-and-Merge. Propose, explain, let the user accept. Publishing is the user's decision.
- Changes flow through the normal O11 lifecycle (1-Click Publish, LifeTime). Never suggest bypassing it.

## Workflow

1. **Understand:** read the module's data model, actions, roles and references. Reuse what exists.
2. **Assess impact:** before changing a public or exposed element, check who depends on it. Breaking consumers is the main O11 risk.
3. **Plan:** state the change, the rules below that apply, and the risk.
4. **Change small:** the smallest staged change that works.
5. **Validate:** read validation messages (TrueChange), run `references/dev-review-checklist.md`, and only then suggest publishing.

## Architecture

- Follow the four-layer Architecture Canvas: End-user modules on top, Core services and business logic below, Foundation (integrations, shared libraries, UI/theme) at the bottom. References go downward only; no circular dependencies and no end-user-to-end-user references.
- Put entities in core modules that own the data. Expose through public actions/service actions, not by letting every consumer touch entities freely.
- Wrap each external system in one integration module. Consumers use the wrapper, not the raw REST/SOAP API.
- Keep public surface small. Every public element is a contract; changing it needs an impact check on consumers.
- Prefer weak references (service actions, REST) across independently deployed apps when tight coupling would block deployment.

## Data and queries

- Aggregates: set limits, fetch needed attributes, filter in the query not in logic.
- Never run an Aggregate or SQL query inside a loop. Fetch once, then look up in memory.
- Avoid chains of dependent Aggregates when one join does the job.
- SQL only when Aggregates cannot express it. Always use parameters; never concatenate user input.
- Index attributes used in filters and sorts of large entities. Plan purge/archive for growing data.
- Keep transactions short; commit deliberately and handle rollback paths.

## Logic

- Reactive: avoid several server calls in one client action when one server action can do the work. No database operations in client-side screen logic.
- Small, single-purpose actions with descriptions on public elements and parameters.
- Handle exceptions deliberately: catch what you can handle, log with context, show user-safe messages.
- No hard-coded values: use Site Properties, Static Entities or configuration. Remove unused actions, aggregates, queries and variables, and leave no reminder comments or large blocks of disabled logic.
- Timers: short, idempotent, resumable, processing in batches that wake themselves; respect the timeout.

## Security

- Every screen has explicit roles. Avoid screens accessible to Anonymous/Everyone unless intentionally public.
- Authorize on the server for every action that reads or changes protected data. Hiding or disabling a button is not security.
- Never trust a user ID sent from the client. Resolve identity server-side.
- Exposed REST APIs require authentication. Store secrets in secret Site Properties; never log tokens, passwords or personal data.
- Do not expose system or sensitive entities via screen aggregates that anyone can reach.

## Mobile and offline (if the module is Mobile)

- Choose a sync pattern that fits the data (read-only, last-write-wins, conflict detection). Keep local data small and sync incremental.
- Do not do heavy work on app start or screen init.

## Reference files

- `references/dev-review-checklist.md` – read before suggesting publish.
- `references/risk-map.md` – maps common risk categories to fixes. Read when fixing findings or summarizing risk.
