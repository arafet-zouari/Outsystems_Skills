# O11 UI review checklist

## Structure
- [ ] Reactive (or Mobile) module; built from OutSystems UI patterns
- [ ] Repeated UI extracted into Blocks
- [ ] Screens and Blocks named clearly (plural entity for lists, singular + Detail for detail)

## Styling
- [ ] No inline styles on widgets
- [ ] No screen-level CSS that belongs in the theme
- [ ] No fixed widths that break small viewports

## Data on screen
- [ ] Aggregates limited and fetching only needed attributes
- [ ] Independent aggregates (not chained) so they load in parallel
- [ ] Secondary content fetched on demand
- [ ] No server calls in client events that can be avoided

## States and feedback
- [ ] Loading state
- [ ] Empty state with next action
- [ ] Error handling with user-safe message
- [ ] Submit buttons show loading; no double submit

## Accessibility
- [ ] Inputs labelled; icon-only buttons have accessible names
- [ ] Logical tab order; visible focus
- [ ] Contrast at least WCAG AA

## Security on screens
- [ ] Screens have roles; none open to Anonymous unless intentionally public
- [ ] No sensitive data in client variables or Block parameters
- [ ] Restricted actions enforced server-side, not just hidden

## Mobile (if applicable)
- [ ] Works offline or degrades clearly
- [ ] Local storage used deliberately and kept small
- [ ] Heavy work is not in screen initialization

## Validation
- [ ] No new TrueChange errors; warnings reviewed
