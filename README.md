# Tap & Order Super App

Tap & Order is a modular Ghanaian super-app platform. **Mobility is the first production vertical; it is not the platform foundation.** The foundation is Platform Core: identity, authentication, organizations, permissions, payments, notifications, location/maps, search, analytics, audit, support, and feature flags.

## Initial product
The first production use case is organized route-based trotro transport in Ghana. Passengers can search directional routes and designated stops, reserve next-day scheduled trips, discover same-day vehicles that have not passed their pickup stop, book segment-aware seat inventory, pay digitally, receive notifications, and track relevant booked/approaching vehicles.

The controlled pilot corridor is **Kasoa -> Accra**. Nationwide rollout is explicitly out of MVP scope.

## Architecture
The system starts as a modular monolith with strict domain boundaries:
- **Platform Core**: reusable capabilities shared by every vertical.
- **Mobility Domain**: routes, stops, operators, vehicles, drivers, schedules, trips, bookings, segment seat inventory, and live tracking.
- **Future domains**: Marketplace, Delivery, Energy/Gas, Services, Property, Tickets, and others. They are documented for integration but not implemented in the MVP.

Mobile/web clients use APIs only and never access the database directly. External providers sit behind adapters. Payment, booking, seat availability, verification, and trip state are server-authoritative.

## Applications
Conceptual applications are:
- Passenger mobile app
- Driver mobile app
- Operator web dashboard
- Admin web platform

A single identity may hold multiple roles and organization memberships. Tenant-private operational data must remain isolated by organization.

## Core safety and correctness rules
Critical booking/payment operations are idempotent. Seat allocation is transactionally protected and segment-aware. Important state transitions are explicit and auditable. Location visibility is minimized to journey-relevant data. Financial confirmation always comes from the server/provider verification path, never the client.

## Documentation
Start with [ARCHITECTURE_ESSENTIALS.md](ARCHITECTURE_ESSENTIALS.md), then [ARCHITECTURE.md](ARCHITECTURE.md), [PRODUCT_REQUIREMENTS.md](PRODUCT_REQUIREMENTS.md), [TECH_STACK.md](TECH_STACK.md), and the `docs/` tree. The OpenAPI contract lives at `openapi/openapi.yaml`.

## Development order
1. Architecture and ADRs
2. Database/domain model
3. API contracts
4. Authentication/authorization
5. Payment architecture
6. Booking and seat-inventory state models
7. Live tracking
8. Security, testing, deployment
9. Only then production implementation

## Definition of done
A feature requires implementation, tests, loading/error/empty states where applicable, security review, analytics consideration, documentation/API updates, migrations, logging, accessibility review, mobile behavior verification, and failure-scenario handling.

## Status
Documentation-first architecture phase. Mobility is the only production vertical in MVP.
