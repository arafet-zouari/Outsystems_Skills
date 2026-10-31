# Risk categories and fixes

Groups: Architecture, Maintainability, Performance, Security. Names below are common patterns, not guaranteed to match your Architecture Dashboard wording; verify there.

| Category | Risk | Fix |
|---|---|---|
| Architecture | Upward or circular references | Move shared logic down a layer; use service actions |
| Architecture | Consumer calls external API directly | Create an integration module |
| Architecture | Large public surface | Reduce to what consumers need |
| Maintainability | Long undocumented flow | Split into smaller actions, add descriptions |
| Maintainability | Hard-coded values | Site Properties / Static Entities |
| Maintainability | Unused elements, reminder comments, disabled code | Delete |
| Performance | Query inside a loop | Fetch once outside loop |
| Performance | Unlimited records | Add limits and pagination |
| Performance | Chained aggregates | Combine with joins |
| Performance | Multiple server calls in a client action | One server action |
| Performance | Inline/screen CSS, large images | Theme, optimized assets |
| Performance | Long timers / timeouts | Batch and wake |
| Security | Screens open to everyone | Assign roles |
| Security | Unauthenticated exposed REST | Add authentication |
| Security | Client-supplied user ID trusted | Resolve identity on server |
| Security | SQL built by concatenation | Parameters |
| Security | DB operation in client logic | Server action with authorization |
