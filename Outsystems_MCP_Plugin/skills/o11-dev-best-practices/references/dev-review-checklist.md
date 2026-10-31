# O11 dev review checklist (before publish)

## Architecture
- [ ] References point downward in the Architecture Canvas; no circular dependencies
- [ ] Entities live in the module that owns the data
- [ ] External systems wrapped in an integration module
- [ ] Impact checked for any change to public/exposed elements

## Data
- [ ] Aggregates/SQL have limits and only needed attributes
- [ ] No Aggregate/SQL inside loops
- [ ] No chained aggregates that could be one join
- [ ] SQL parameterized
- [ ] Indexes considered for large filtered/sorted entities
- [ ] Purge/archive plan for growing entities

## Logic
- [ ] Client actions avoid multiple server calls
- [ ] No database operations in client-side logic
- [ ] Exceptions handled and logged with context
- [ ] No hard-coded URLs, IDs or credentials
- [ ] No unused actions, aggregates, queries, variables or disabled code
- [ ] Public elements and parameters have descriptions
- [ ] Timers are batched, idempotent and within timeout

## Security
- [ ] Every screen has roles
- [ ] Server actions authorize access
- [ ] Exposed REST APIs authenticated
- [ ] Secrets stored as secret Site Properties
- [ ] No sensitive entities exposed through open screens

## Validation and delivery
- [ ] No new TrueChange errors; warnings reviewed
- [ ] Changes reviewed in Compare-and-Merge before accepting
- [ ] Publish and deployment follow the normal lifecycle
