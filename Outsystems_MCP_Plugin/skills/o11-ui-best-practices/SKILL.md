---
name: o11-ui-best-practices
description: UI and UX best practices for OutSystems 11 (O11) Reactive Web and Mobile apps worked on through the Service Studio MCP server. Use whenever the user asks to create, change, restyle or review a screen, block, theme, layout, form, list, dashboard or navigation in an OutSystems 11 module open in Service Studio, or asks about OutSystems UI patterns, responsiveness or accessibility, even if they do not say "best practices". Apply before proposing or writing any model change, and again when reviewing the result.
---

# O11 UI best practices

This skill complements the OutSystems 11 MCP skill (`servicestudio-mcp-oml`). For tool names, parameters, staging and publish behavior, that skill and the live MCP tool list are the source of truth. This skill adds UI judgment only and names no tools.

## Context to respect

- The MCP server runs inside Service Studio and works on the ONE module open there. Confirm which module is open before assuming anything.
- Reads are safe. Model writes are Beta and are staged for review in Service Studio's Compare-and-Merge window. Propose changes and let the user accept them; never describe a change as done until it is accepted and published.
- Prefer Reactive Web and Mobile for new UI. Do not extend Traditional Web unless the module already is one.

## Workflow

1. **Read first:** inspect the module's screens, blocks, theme, roles and existing patterns. Reuse before creating.
2. **Plan:** list the screens/blocks you will touch and which rules below apply. Show the plan before writing.
3. **Change:** make the smallest staged change that satisfies the request.
4. **Review:** run `references/ui-review-checklist.md` and read the module's validation messages (TrueChange). Fix errors and warnings you introduced.

## Core rules

- **OutSystems UI first.** Use built-in patterns (Card, List Item Content, Tabs, Wizard, Accordion, Blank Slate, Alert, Notification, Pagination, Sidebar, Master Detail, Data Grid) before custom layouts.
- **Theme owns style.** Colors, typography, spacing and radius live in the theme/style sheet of the app's theme module, not on individual widgets. No inline styles; avoid per-screen CSS.
- **Reuse with Blocks.** Anything used on two or more screens becomes a Block with clear input parameters and events. Keep layouts shared.
- **Responsive by default.** Design smallest viewport first. Use Columns, Adaptive and Display on Device; avoid fixed pixel widths.
- **Four states per data view:** loading, empty (Blank Slate with a next step), error (Alert/Notification with recovery), populated.
- **Screen data loading.** Fetch only what the screen needs. Use limits and pagination. Keep screen aggregates independent so they can load in parallel, and fetch hidden/secondary content only on demand.
- **Forms:** visible labels, validation next to the field, one primary action, Button Loading to prevent double submit, clear disabled-state reasons.
- **Lists:** never unbounded. Default sort, pagination or infinite scroll with a limit.
- **Navigation:** shallow and predictable, with a clear back path on detail screens.
- **Accessibility:** labels on inputs and icon-only buttons, keyboard operability, visible focus, WCAG AA contrast, correct heading structure, test with the smallest viewport.
- **Text:** no hard-coded user-facing strings if the app is multilingual; use consistent verbs for the same action.
- **Mobile specifics:** design for intermittent connectivity. Show cached/local data first when the app is offline-capable, show sync status, and avoid heavy work in screen initialization.

## Request template (state this to the user or in the plan)

```
Goal: <user outcome>
Module / screens / blocks: <names>
Reuse: <patterns, blocks, layout>
States: loading / empty / error / populated
Responsive: phone / tablet / desktop
Styling: theme only
Accessibility: labels, focus, contrast, keyboard
Out of scope: <what must not change>
```

## Reference files

- `references/ui-review-checklist.md` – read after every UI change.
- `references/pattern-map.md` – design element to OutSystems UI pattern mapping.
