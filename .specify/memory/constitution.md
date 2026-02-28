<!--
  Sync Impact Report
  ===================
  Version change: N/A (blank template) → 1.0.0
  Modified principles: N/A (initial ratification)
  Added sections:
    - Core Principles (6 principles defined)
    - Technology Stack & Constraints
    - Reference Documents
    - Governance
  Removed sections: None (template placeholders replaced)
  Templates requiring updates:
    - .specify/templates/plan-template.md ✅ No update needed (dynamic Constitution Check)
    - .specify/templates/spec-template.md ✅ No update needed (generic template)
    - .specify/templates/tasks-template.md ✅ No update needed (generic template)
    - .specify/templates/checklist-template.md ✅ No update needed (generic template)
  Follow-up TODOs: None
-->

# Debatable Constitution

## Core Principles

### I. Quality Discourse First

Every feature decision MUST reinforce that Debatable values _how_ people
debate, not _what_ they believe. Non-negotiable rules:

- The multi-dimensional rating system (debate skill, respectfulness,
  relevance, persuasiveness) is the core product differentiator and
  MUST be protected in all design and implementation choices.
- Features that could encourage popularity-contest dynamics (e.g.,
  simple upvote/downvote) MUST NOT be introduced without
  constitutional amendment.
- Rating dimensions MUST remain independently scored on a 1–5 scale;
  collapsing them into a single score requires amendment.

**Rationale**: The rating system is the moat. Protecting its integrity
ensures the platform stays differentiated from generic social video
apps.

### II. TypeScript + Next.js + Supabase Stack

All code MUST adhere to the following technology constraints:

- **Frontend & API**: Next.js (App Router) with TypeScript in strict
  mode.
- **Database & Auth**: Supabase (Postgres) for data persistence,
  authentication (Google OAuth), and file storage.
- **Styling**: Tailwind CSS. No additional CSS frameworks.
- **Deployment**: Vercel.
- All source files MUST be TypeScript (`.ts` / `.tsx`). No plain
  JavaScript files in the repository.

**Rationale**: A unified, modern stack reduces context switching,
enables full-stack type safety, and aligns with the solo-developer-
with-AI workflow.

### III. Production Architecture, Prototype Scope

Code MUST be structured for long-term growth even though the immediate
goal is an investor demo. Non-negotiable rules:

- Feature-based folder organization (not file-type grouping).
- Database changes MUST use migrations (Supabase CLI).
- Environment configuration via `.env` files with typed validation.
- Clean separation between API routes and business logic.
- No shortcuts that would require a rewrite when scaling to beta.

**Rationale**: Building demo-quality code that must later be rewritten
wastes more time than building beta-ready structure from day one.

### IV. Pragmatic Testing

This project deliberately overrides strict TDD. Testing strategy:

- TypeScript strict mode serves as the first line of defense against
  bugs.
- Integration tests are REQUIRED for critical paths: authentication
  flow, video upload, and rating submission.
- TDD (red-green-refactor) is REQUIRED only for complex business
  logic such as rating calculations and aggregation.
- Unit tests for UI components MUST NOT be written during the
  prototype phase — this is intentional scope control, not neglect.

**Rationale**: A solo developer building an investor demo must allocate
testing effort where it delivers the most confidence per hour invested.

### V. Documentation as a First-Class Citizen

Everything MUST be documented. Non-negotiable rules:

- Design decisions MUST be recorded (in specs, plan docs, or inline
  comments referencing a decision).
- API contracts MUST be documented before implementation begins.
- Data model changes MUST include migration notes.
- Seed data scripts MUST be documented and reproducible.
- A future developer MUST be able to onboard from documentation
  alone, without requiring verbal context transfer.

**Rationale**: Solo developer with AI assistance means the
documentation _is_ the team's shared memory. If it is not written
down, it does not exist.

### VI. Mobile-First, Web-Native

All UI MUST be designed for mobile phone browsers first, desktop
second. Non-negotiable rules:

- Layouts MUST be responsive with mobile as the base breakpoint.
- Touch targets MUST meet minimum size guidelines (44×44 CSS pixels).
- API routes are the shared backend contract — designed to serve a
  future React Native client without modification.
- No desktop-only interactions (hover-dependent features MUST have
  touch equivalents).

**Rationale**: The target audience debates on their phones. A future
React Native app will share the same API, so the backend contract
MUST be client-agnostic from the start.

## Technology Stack & Constraints

| Layer     | Technology                   | Notes                   |
| --------- | ---------------------------- | ----------------------- |
| Framework | Next.js (App Router)         | Latest stable           |
| Language  | TypeScript (strict mode)     | Latest stable           |
| Database  | Supabase (Postgres)          | Hosted                  |
| Auth      | Supabase Auth (Google OAuth) | —                       |
| Storage   | Supabase Storage             | Video files, thumbnails |
| Styling   | Tailwind CSS                 | Latest stable           |
| Deploy    | Vercel                       | Production & preview    |
| Testing   | Vitest / Playwright          | Integration tests only  |

## Reference Documents

- **Project Context**: `.specify/memory/brainstorm.md` — full project
  background, feature brainstorm, and product vision.
- **Technical Specifications**: `documents/design-prototype.md` — data
  model, API routes, project structure, and feature specs.
- **Prototype Prompts**: `documents/speckit-prototype-prompts.md` —
  command prompts for speckit workflow.

## Governance

- This constitution supersedes all other project practices, templates,
  and ad-hoc decisions. When in conflict, the constitution wins.
- Amendments MUST be documented with:
  - A description of the change and its rationale.
  - An updated version number following semantic versioning.
  - An updated `Last Amended` date.
- All implementation plans MUST pass a Constitution Check gate before
  proceeding (see plan template).
- Compliance reviews SHOULD occur at each phase checkpoint in the
  task workflow.

**Version**: 1.0.0 | **Ratified**: 2026-02-21 | **Last Amended**: 2026-02-21
