# Api Testing

## Purpose
Contract, authz, validation, idempotency, rate-limit and error-envelope tests.

## Product context
Tap & Order is a Ghana-focused multi-vertical super-app. Platform Core is the reusable foundation; Mobility is the first production domain. The first controlled pilot is the directional Kasoa -> Accra corridor. Marketplace, Delivery, Energy/Gas, Services, Property and other verticals are future domains and must not leak fake functionality into the Mobility MVP.

## Architectural rules
- Mobile and web clients communicate through versioned APIs; they never access the database directly.
- Domain logic depends on platform interfaces, not provider SDKs. Payments, messaging, maps, storage and other vendors sit behind adapters.
- The server is authoritative for payment status, booking confirmation, seat availability, driver verification and trip state.
- Users may hold multiple roles. Organization-scoped data is tenant-isolated and authorization is enforced server-side.
- Critical booking and payment commands are idempotent. Important state transitions emit audit records and domain events.
- Location collection and exposure are minimized to operational need. Passenger views expose only journey-relevant vehicles.
- Ghanaian connectivity is treated as unreliable: clients may cache/queue safe operational updates, but never manufacture financial truth.

## MVP interpretation
This document governs the Mobility MVP only unless it explicitly describes an extension point. The architecture must make future verticals possible without implementing them now.

## Operational quality
Changes affecting this area require appropriate unit/integration/E2E coverage, structured logs, failure handling, analytics consideration, security review, documentation updates, and migration/API updates when contracts change.

## Open questions and decisions
Unresolved provider, regulatory, operational-association, fare-policy, retention, and rollout choices must be recorded in `docs/project/open-questions.md` or an ADR before they become production assumptions.
