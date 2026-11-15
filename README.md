# Go Kids Play — Operations Management Case Study

[Türkçe sürüm](README.tr.md) · [Architecture](docs/architecture.md) · [Screenshot note](docs/screenshots/README.md)

Go Kids Play is a private commercial application designed to coordinate the day-to-day work of a children's play-centre. It brings customer records, memberships, timed play sessions, payments, staff access and operational reporting into one workflow-oriented system.

> **Portfolio scope:** This repository is a source-code-free case study. The private application source, Git history, credentials, customer data and infrastructure details are not included. It is documentation, not an installable or open-source release.

## The business problem

A play-centre has several connected workflows happening at the same time: registering families, starting and monitoring play sessions, applying packages or memberships, collecting split payments, handling cancellations, coordinating birthday events and reconciling the day. Managing those workflows in separate tools makes it harder for staff to see the current operational state and for managers to review what happened.

The application is structured around a shared operational record so front-desk and management tasks can be handled from the same system while access remains role-aware.

## Verified workflows

The following capabilities are represented by application pages, service modules and database migrations in the private codebase.

### Customer and membership management

- Customer and child profiles, search, activity history, notes, tags and wallet views
- Membership packages, sales, usage tracking, pause/resume and cancellation flows
- Personal entitlements, campaign-aware packages and membership reporting
- Customer transaction history and CSV-oriented reporting support

### Timed play sessions

- Timed and unlimited play-session models
- Live session list with filtering, countdowns and dense/table views
- Pause, resume, extend, cancel and reason-based completion flows
- Realtime session synchronization and completion history

### Payments and cash operations

- Cash, card and wallet payment splits
- Session extensions, cancellation/refund records and refund history
- Register opening, expected-total calculation, closing and closing history
- Atomic retail checkout/void database operations and stock-related workflows

### Birthday events and operations

- Birthday package definitions and event records
- Event status, participant, timeline, package and payment management
- Upcoming-event views and organization-level reporting

### Staff and access control

- Role-based route and module access
- Per-user permission overrides
- Staff directory, shift records and account lifecycle operations
- Branch-aware access boundaries for multi-location operation

### Reporting

- Revenue periods and payment-method breakdowns
- Attendance, daily traffic and peak-hour analysis
- Customer, package, birthday-event and staff insights
- Retail, waste, discount, day-end and operational-note reports

### Mobile and desktop delivery

- Installable PWA manifest with standalone display support
- Responsive navigation and mobile-oriented operational screens
- Parent-facing and TV/kiosk routes in the application structure
- Electron packaging configuration for macOS, Windows and Linux

## Technology

- **Application:** Next.js 14 App Router, React 18, TypeScript
- **UI:** Tailwind CSS, Radix UI primitives, shadcn components, Lucide icons, Recharts
- **Backend and data:** Supabase, PostgreSQL, SQL migrations, RPC functions, Row Level Security
- **Realtime:** Supabase Realtime for operational session updates
- **Delivery:** PWA manifest and Electron desktop packaging

## Architecture highlights

- A service layer separates UI components from Supabase queries and RPC calls.
- PostgreSQL functions group multi-step financial and operational changes into database-side operations.
- Branch identifiers, Row Level Security policies and role checks provide the basis for location-scoped access.
- A shared session store combines initial loading, realtime events, reconnect resynchronization and local countdown updates.
- Reliability helpers cover retry behavior, safe RPC handling, network state, audit logging and realtime supervision.
- The same Next.js interface is configured for browser/PWA use and Electron-based desktop packaging.

See [docs/architecture.md](docs/architecture.md) for a component-level overview and the boundaries of this review.

## Current status and limitations

- The review confirms code paths and schema definitions; it does **not** independently confirm production deployment, production safety, commercial results or active user counts.
- No automated test suite or test script was identified in the inspected project structure, and this case study does not claim passing tests or a clean quality gate.
- The payment-terminal abstraction currently defaults to a mock provider; a production terminal integration is not claimed.
- Some dashboard presentation widgets use sample data while other panels use service-backed data.
- The parent phone/OTP flow contains demo-oriented behavior and should not be presented as a verified production authentication flow.

## Screenshots

No application screenshots are published in this version. The existing demo-data generator writes through the configured Supabase client, while offline mode does not provide isolated synthetic data for every requested operational screen. Rather than risk connecting to production or construct a separate mock product solely for screenshots, the visual step was intentionally omitted. Details are recorded in [docs/screenshots/README.md](docs/screenshots/README.md).

## Repository contents

```text
.
├── README.md
├── README.tr.md
└── docs
    ├── architecture.md
    └── screenshots
        └── README.md
```

No application source code, database dump, environment file, credential or private Git history is included.

