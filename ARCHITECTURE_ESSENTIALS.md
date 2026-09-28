# Architecture Essentials

These are non-negotiable guardrails for every coding session.

1. Platform Core remains independent of Mobility.
2. Mobility is a domain module, not the foundation.
3. Future verticals reuse Platform Core rather than duplicating identity, payments, notifications, location or search.
4. Clients never access the database directly.
5. Payment state is server-authoritative and provider-verified.
6. Seat availability is segment-aware and transactionally protected.
7. Booking/payment commands are idempotent.
8. Location access follows least-exposure privacy rules.
9. Organization data is tenant-isolated.
10. Important state transitions are explicit and auditable.
11. External providers are behind adapters.
12. Provider-specific logic never enters domain rules.
13. A person may have multiple roles.
14. Future vertical functionality is not implemented in the Mobility MVP.
15. Architectural integrity is not traded for rapid feature additions.
16. Bookings use controlled states, not scattered booleans.
17. Directional routes are distinct: Kasoa -> Accra is not Accra -> Kasoa.
18. Pickup uses designated stops, not arbitrary roadside points.
19. Offline queues may carry safe operational updates; financial confirmation never comes from offline/client state.
20. Start modular; distribute only when demonstrated need exists.

## Required review
Every significant change must be checked against these rules and update affected documentation, tests, API contracts and ADRs.
