---
stepsCompleted: [1, 2, 3, 4, 5, 6, 7, 8]
inputDocuments:
  - _bmad-output/planning-artifacts/prd.md
  - _bmad-output/planning-artifacts/ux-design-specification.md
  - _bmad-output/planning-artifacts/research/technical-beads-dolt-llm-invocation-options-research-2026-03-08.md
workflowType: 'architecture'
lastStep: 8
status: 'complete'
completedAt: '2026-03-08'
project_name: 'ideastream'
user_name: 'Richard'
date: '2026-03-08'
---

# Architecture Decision Document

_This document builds collaboratively through step-by-step discovery. Sections are appended as we work through each architectural decision together._

## Project Context Analysis

### Requirements Overview

**Functional Requirements:**
The PRD defines 44 functional requirements across seven major capability groups:

1. Project and work organisation (FR1-FR8): project containers, repository association, free-text capture, assignment correction, bead linkage.
2. Task intake and dispatch (FR9-FR15): separation of organisational capture from delegated execution, explicit lifecycle states, and agent-invokable command surface.
3. Planning and execution management (FR16-FR21): translation of tasks into actionable units, inspectable execution state, retry/reroute/manual completion paths.
4. Cross-project visibility and prioritisation (FR22-FR26): orientation across projects, next-action clarity, progress legibility.
5. Repository and workflow safety (FR27-FR32): trunk protection, branch-scoped delegated work, inspectable proposed changes, safe recovery.
6. Traceability, inspection, and recovery (FR33-FR37): historical trace, failure diagnostics, operator-understandable outcomes.
7. CLI, guidance, and adoption support (FR38-FR44): standalone CLI distribution, setup docs, command discoverability, repository-local instruction shaping.

Architecturally, these imply a workflow/state-centric core domain with explicit boundaries between capture, planning, dispatch, execution, and recovery, plus strong projection layers for status visibility.

**Non-Functional Requirements:**
Key NFR drivers include:

- Performance: low-friction capture and responsive cross-project status views.
- Reliability: no silent failures; deterministic operation outcomes with clear state transitions.
- Security/safety: strict separation between accepted repository state and delegated in-progress work; trunk protection as a hard architectural constraint.
- Integration robustness: recoverable integration failures with preserved operational state.
- UX and accessibility (from UX spec): WCAG 2.2 AA baseline, keyboard-first interactions, colour-independent state communication, reduced-motion respect, responsive behaviour across mobile/tablet/desktop.

These NFRs require architecture that is observable, fail-safe by default, and explicit in state semantics across all interfaces.

**Scale & Complexity:**
Complexity is medium-high due to interaction of multiple concerns rather than raw enterprise scale:

- Dual-surface product model (CLI execution + web cockpit visibility)
- Confidence-gated assignment and conditional auto-dispatch logic
- Cross-project state aggregation and exception triage
- Traceable event timeline and recovery workflows
- Repository branch safety and audit guarantees

- Primary domain: full-stack developer tool (CLI-first orchestration with web visibility surface)
- Complexity level: medium-high
- Estimated architectural components: 10-14 core components/services (CLI interface, API/orchestration layer, domain/state engine, assignment engine, dispatch planner, execution adapter(s), repository workflow manager, event log/audit store, read-model/query projections, web UI backend, web frontend, observability layer, auth/config boundary, integration adapters)

### Technical Constraints & Dependencies

- Hard constraint: delegated work must not endanger trunk; branch-isolation and safe promotion paths are mandatory.
- Product is language-agnostic at repository level; architecture should avoid language-specific coupling in core workflows.
- CLI is canonical operational interface (`idea` command family) with deterministic output contracts.
- Web Mission Cockpit must maintain semantic parity with CLI lifecycle and operation receipts.
- Direct model invocation and agent orchestration are distinct concerns; architecture should keep inference provider coupling behind an adapter boundary.
- Repository-local instruction files (e.g., agent guidance) must be supportable as part of behavioural configuration.
- Distribution expectations include npm, Homebrew, and Windows-compatible installation path.

### Cross-Cutting Concerns Identified

- Unified lifecycle state model shared across CLI, backend workflows, and web projections.
- Idempotency and concurrency control for capture/assignment/bead creation/dispatch transitions.
- Auditability and traceability (actor, timestamp, transition, artefact linkage) for trust and recovery.
- Exception-first operability (blocked/failed/needs-review) with clear remediation actions.
- Observability: structured logs, domain events, and health metrics for project and dispatch status.
- Safety guardrails: policy enforcement for repository operations and promotion to accepted state.
- UX consistency: deterministic mapping between command receipts and web state representation.
- Accessibility and responsive standards as non-negotiable quality constraints for the web surface.

## Starter Template Evaluation

### Primary Technology Domain

Dual-surface developer tooling with explicitly separated codebases:

- CLI operational product (`cli`)
- Website/Mission Cockpit (`web`)

### Starter Options Considered

1. Website starter: create-next-app (16.1.6, recently maintained)

- Strong fit for web cockpit, TypeScript, Tailwind, accessibility-focused UI work.
- Good long-term maintenance signal.

2. CLI starter: create-oclif (1.17.0)

- Rejected due to deprecation warnings and unsupported status in current CLI output.

3. CLI baseline: manual TypeScript bootstrap with maintained runtime libs

- Uses current maintained packages (for example `commander`, `tsx`, `typescript`).
- Avoids deprecated scaffolding and keeps CLI architecture fully under project control.

### Selected Starter Strategy: Two Separate Folders

**Rationale for Selection:**
The product is intentionally CLI-first with a separate visibility web surface. Keeping them fully separated reduces coupling risk, simplifies release strategy, and preserves clear operational boundaries for architecture and implementation stories.

### Folder Strategy

- `cli/`: standalone Node/TypeScript CLI project
- `web/`: standalone Next.js web project

### Initialization Commands

**Website (Mission Cockpit):**

```bash
npx create-next-app@latest web --ts --eslint --tailwind --app --src-dir --turbopack --import-alias "@/*" --use-pnpm
```

**CLI (separate project bootstrap):**

```bash
mkdir cli && cd cli
pnpm init
pnpm add commander zod
pnpm add -D typescript tsx @types/node eslint @typescript-eslint/parser @typescript-eslint/eslint-plugin
pnpm tsc --init
```

### Architectural Decisions Provided by This Strategy

**Language & Runtime:**

- Both projects use TypeScript, but with independent configs and lifecycles.

**Styling Solution:**

- Tailwind in web project only; CLI has no UI styling dependencies.

**Build Tooling:**

- Next.js/Turbopack in web project.
- Dedicated CLI toolchain (`tsc` + `tsx`) in CLI project.

**Testing Framework:**

- Intentionally deferred for explicit architecture decision in later steps, per project.

**Code Organization:**

- Hard separation of concerns by folder and deployable unit.
- Shared contracts, if needed, should be introduced later as explicit packages, not implicit coupling.

**Development Experience:**

- Independent run/test/release workflows for CLI and web.
- Cleaner boundaries for versioning, packaging, and deployment strategy.

**Note:** Project initialization using these commands should be the first implementation story.

## Core Architectural Decisions

### Decision Priority Analysis

**Critical Decisions (Block Implementation):**

- Persistent task storage is Beads-backed with Dolt durability; no separate application database in MVP.
- All task entities are represented and persisted as beads (single source of truth for work items).
- Web-to-core boundary is enforced through a minimal server: `web` -> server API -> `cli` -> Beads/Dolt.
- Only `cli` is allowed to communicate with Beads; no direct Beads access from web code.
- Project configuration is split between repository-local config (versioned in Git) and residual user/global config in a `.dotfile`.

**Important Decisions (Shape Architecture):**

- API style for web/server boundary is minimal REST for MVP.
- MVP security model is local-trust with operational hardening; full authentication is deferred until explicit multi-user or internet-exposed deployment requirements appear.
- Web read-models are server-sourced; optimistic updates are allowed only for low-risk UI transitions and must reconcile with CLI-derived authoritative state.
- Deployment topology is local-first for MVP: web server, CLI, and Beads runtime on the same machine boundary.

**Deferred Decisions (Post-MVP):**

- Full authentication/authorization subsystem and identity provider integration.
- Multi-tenant hosting model and remote access controls.
- Additional persistence systems beyond Beads/Dolt unless a non-bead domain requires distinct storage semantics.

### Data Architecture

- **Primary data system:** Beads on Dolt.
- **Version evidence:** Dolt `v1.83.4` (published 2026-03-06), Beads `v0.59.0` (published 2026-03-06).
- **Data model principle:** Task and workflow state is bead-native; avoid parallel task stores.
- **Configuration model:**
  - Repository-specific configuration in-project and persisted via Git.
  - Remaining machine/user configuration in a `.dotfile`.
- **Rationale:** Preserves a single operational truth source, improves traceability, and reduces divergence risk between interfaces.

### Authentication & Security

- **MVP auth decision:** Defer full auth stack.
- **MVP security stance:** Local-trust assumptions with strict boundary controls.
- **Guardrails:**
  - Server validates and sanitizes all web requests before CLI invocation.
  - CLI invocation allow-list limits callable commands.
  - Explicit repository safety checks before mutating operations.
  - Structured audit logs for every state-changing action.
- **Trigger for auth introduction:** Multi-user requirements, remote exposure, or shared-host deployment.

### API & Communication Patterns

- **Boundary architecture:** `web` never calls Beads directly.
- **Mandatory path:** `web` -> server REST endpoints -> `cli` adapter -> Beads.
- **Command contract:** Server owns input validation, idempotency keys for mutating requests, and normalized error mapping.
- **Error semantics:** REST responses provide stable machine-readable error codes and user-facing summaries while preserving CLI diagnostic detail in logs.

### Frontend Architecture

- **State source of truth:** Server-provided read models derived from CLI/Beads state.
- **UI update strategy:**
  - Read-heavy status views pull from server projections.
  - Mutations are command-style API calls; optimistic updates allowed only where rollback is deterministic.
- **Consistency requirement:** Web status semantics must map directly to CLI lifecycle semantics.

### Infrastructure & Deployment

- **MVP topology:** Local-first deployment with tightly scoped process boundaries.
- **Service responsibilities:**
  - `cli`: canonical operational and Beads integration surface.
  - Minimal server: web-facing API facade and policy enforcement layer.
  - `web`: visibility, quick-capture UX, inspection and triage views.
- **Operational principle:** Keep Beads connectivity private to CLI path to minimize blast radius and simplify policy enforcement.

### Decision Impact Analysis

**Implementation Sequence:**

1. Bootstrap `cli` and implement stable command contracts for required bead operations.
2. Implement minimal server adapter that invokes CLI with strict validation and error mapping.
3. Scaffold `web` and bind views/actions to server APIs (never directly to Beads).
4. Implement configuration loading precedence (repo config then `.dotfile`) and operational safety checks.
5. Add observability and audit logging across server->CLI->Beads command flow.

**Cross-Component Dependencies:**

- Web UX reliability depends on deterministic CLI output contracts and server normalization rules.
- Server API stability depends on stable CLI command schemas and error codes.
- Repository safety guarantees depend on CLI-level guardrails enforced regardless of web behaviour.
- Configuration behaviour across components depends on consistent precedence and schema validation in both server and CLI paths.

## Implementation Patterns & Consistency Rules

### Pattern Categories Defined

**Critical Conflict Points Identified:**
12 areas where AI agents could make different choices and break interoperability across `web`, server, `cli`, and execution-agent flows.

### Naming Patterns

**Database Naming Conventions:**
Not applicable for standalone app tables in MVP because task persistence is Beads-managed.
For internal app metadata/config caches (if introduced later):

- Table names: `snake_case_plural` (example: `sync_checkpoints`)
- Columns: `snake_case` (example: `last_synced_at`)
- IDs: `<entity>_id` for foreign references

**API Naming Conventions:**

- REST endpoints: plural, resource-oriented (example: `/api/projects`, `/api/beads/:beadId`)
- Route params: `camelCase` in code, path token form in URL (example: `:beadId`)
- Query params: `camelCase` (example: `projectId`, `status`)
- Versioning: prefix route group with `/api/v1/...` once external clients are supported

**Code Naming Conventions:**

- TypeScript types/interfaces: `PascalCase`
- Functions/variables: `camelCase`
- Constants/env keys: `UPPER_SNAKE_CASE`
- Files:
  - React components: `PascalCase.tsx` (example: `BeadTimeline.tsx`)
  - Non-component modules: `kebab-case.ts` (example: `run-cli-command.ts`)
- CLI commands: kebab-case verbs/nouns (example: `idea bead-show`)

### Structure Patterns

**Project Organization:**

- `cli/`: canonical command handlers and Beads integration adapters.
- `web/`: UI plus minimal server API boundary.
- Browser client code in `web` must not communicate directly with Beads.
- Server API handlers own validation, idempotency, and CLI invocation.

**Supported Beads Access Paths:**

- `web client -> web server API -> cli -> Beads`
- `direct CLI user -> cli -> Beads`
- `execution agent (for bead execution) -> bd CLI -> Beads`

Any new path to Beads must be explicitly approved as an architecture change.

**File Structure Patterns:**

- `web/src/app/api/*`: HTTP contract and response normalization only.
- `web/src/lib/cli-adapter/*`: server-side CLI invocation wrappers.
- `web/src/features/*`: feature-sliced UI modules (dashboard, quick-add, bead-detail).
- `cli/src/commands/*`: user-visible command entrypoints.
- `cli/src/core/*`: shared domain logic for task/bead operations.
- `cli/src/adapters/beads/*`: all Beads command execution and parsing.

### Format Patterns

**API Response Formats:**

- Success:
  - `{ "ok": true, "data": <payload>, "meta": { "requestId": "..." } }`
- Error:
  - `{ "ok": false, "error": { "code": "BEAD_NOT_FOUND", "message": "...", "details": {} }, "meta": { "requestId": "..." } }`
- Never return raw CLI stderr directly to browser clients.

**Data Exchange Formats:**

- JSON fields: `camelCase`
- Date/time: ISO 8601 UTC strings only (`YYYY-MM-DDTHH:mm:ss.sssZ`)
- Status values: fixed enum strings (`waiting`, `inProgress`, `blocked`, `completed`, `failed`, `needsReview`)
- IDs: opaque strings, never inferred client-side

### Communication Patterns

**Event System Patterns:**

- Internal event names: dot-delimited, lower-case (`bead.created`, `bead.stateChanged`)
- Payload shape:
  - `{ eventName, occurredAt, actor, beadId, projectId, payloadVersion, payload }`
- Event versioning: integer `payloadVersion`, increment on schema change

**State Management Patterns:**

- Server state is authoritative for web clients.
- Client mutations are command-style requests, then reconcile from server response.
- No direct client-side state mutation that implies durable success before server ack.
- Query cache keys use tuple style: `['beads', projectId, filters]`.

### Process Patterns

**Error Handling Patterns:**

- Server maps CLI exit/error classes to stable API error codes.
- Distinguish:
  - User-correctable errors (validation, missing project mapping)
  - Operational errors (CLI unavailable, Beads command failure)
  - Safety errors (repo guardrail violation)
- Every error logs `requestId`, command intent, and sanitized diagnostic context.

**Loading State Patterns:**

- Use explicit states per view: `idle`, `loading`, `success`, `error`.
- For command submissions:
  - disable duplicate submit
  - show pending indicator with cancellable affordance where safe
- Always refresh affected read models after mutation success.

### Enforcement Guidelines

**All AI Agents MUST:**

- Preserve the approved Beads access paths and do not introduce new access channels without architecture approval.
- Preserve response envelope and error code contract exactly for browser-facing APIs.
- Use the defined status enum and date formats across CLI, server, web, and execution-agent outputs.

**Pattern Enforcement:**

- Shared lint rules plus TypeScript type contracts for API envelopes.
- Contract tests for CLI adapter and API response normalization.
- PR checklist item: "Does this introduce any Beads path outside approved channels?"
- Pattern violations documented in architecture-decision change notes before merge.

### Pattern Examples

**Good Examples:**

- `POST /api/beads` -> server validates -> calls `cli` adapter -> returns normalized `{ok,data}`.
- CLI user runs `idea add ...` -> CLI validates -> writes to Beads.
- Execution agent runs `bd` commands for a claimed bead and emits state transitions using shared lifecycle vocabulary.

**Anti-Patterns:**

- Browser client invoking Beads directly.
- Returning mixed response shapes (`{data}` in one endpoint, raw arrays in another).
- Using multiple status vocabularies (`in-progress` vs `inProgress` vs `running`) across layers.

## Project Structure & Boundaries

### Complete Project Directory Structure

```text
ideastream/
├── README.md
├── .gitignore
├── .editorconfig
├── .github/
│   └── workflows/
│       ├── ci-cli.yml
│       ├── ci-web.yml
│       └── architecture-guardrails.yml
├── docs/
│   ├── architecture/
│   │   ├── boundaries.md
│   │   ├── api-contracts.md
│   │   └── decision-log.md
│   └── operations/
│       ├── local-setup.md
│       └── troubleshooting.md
├── cli/
│   ├── package.json
│   ├── tsconfig.json
│   ├── eslint.config.js
│   ├── .env.example
│   ├── src/
│   │   ├── index.ts
│   │   ├── commands/
│   │   │   ├── idea-add.ts
│   │   │   ├── idea-show.ts
│   │   │   ├── idea-status.ts
│   │   │   ├── bead-claim.ts
│   │   │   ├── bead-update.ts
│   │   │   └── bead-close.ts
│   │   ├── core/
│   │   │   ├── models/
│   │   │   │   ├── bead.ts
│   │   │   │   ├── project.ts
│   │   │   │   └── lifecycle.ts
│   │   │   ├── services/
│   │   │   │   ├── assignment-service.ts
│   │   │   │   ├── bead-service.ts
│   │   │   │   └── status-service.ts
│   │   │   ├── validation/
│   │   │   │   ├── input-schemas.ts
│   │   │   │   └── config-schemas.ts
│   │   │   └── config/
│   │   │       ├── repo-config.ts
│   │   │       ├── dotfile-config.ts
│   │   │       └── config-loader.ts
│   │   ├── adapters/
│   │   │   └── beads/
│   │   │       ├── bd-runner.ts
│   │   │       ├── bd-parser.ts
│   │   │       ├── bd-errors.ts
│   │   │       └── bd-contracts.ts
│   │   ├── telemetry/
│   │   │   ├── logger.ts
│   │   │   └── audit-events.ts
│   │   └── utils/
│   │       ├── date.ts
│   │       └── ids.ts
│   └── tests/
│       ├── unit/
│       ├── integration/
│       └── fixtures/
├── web/
│   ├── package.json
│   ├── next.config.ts
│   ├── tsconfig.json
│   ├── postcss.config.js
│   ├── eslint.config.js
│   ├── .env.example
│   ├── src/
│   │   ├── app/
│   │   │   ├── layout.tsx
│   │   │   ├── page.tsx
│   │   │   ├── projects/
│   │   │   │   └── [projectId]/page.tsx
│   │   │   ├── beads/
│   │   │   │   └── [beadId]/page.tsx
│   │   │   └── api/
│   │   │       ├── health/route.ts
│   │   │       ├── projects/route.ts
│   │   │       ├── beads/route.ts
│   │   │       ├── beads/[beadId]/route.ts
│   │   │       └── commands/
│   │   │           ├── add-task/route.ts
│   │   │           ├── claim-bead/route.ts
│   │   │           └── close-bead/route.ts
│   │   ├── features/
│   │   │   ├── cockpit/
│   │   │   ├── quick-add/
│   │   │   ├── bead-detail/
│   │   │   └── exception-triage/
│   │   ├── components/
│   │   │   ├── ui/
│   │   │   ├── status/
│   │   │   └── timeline/
│   │   ├── lib/
│   │   │   ├── api-client.ts
│   │   │   ├── api-envelope.ts
│   │   │   ├── cli-adapter/
│   │   │   │   ├── run-cli-command.ts
│   │   │   │   ├── normalize-response.ts
│   │   │   │   └── map-errors.ts
│   │   │   ├── events/
│   │   │   │   └── event-contracts.ts
│   │   │   └── validation/
│   │   │       └── request-schemas.ts
│   │   ├── state/
│   │   │   ├── query-client.ts
│   │   │   └── cache-keys.ts
│   │   ├── styles/
│   │   │   └── globals.css
│   │   └── types/
│   │       ├── api.ts
│   │       └── lifecycle.ts
│   ├── public/
│   │   └── assets/
│   └── tests/
│       ├── unit/
│       ├── integration/
│       └── e2e/
└── _bmad-output/
  ├── planning-artifacts/
  └── implementation-artifacts/
```

### Architectural Boundaries

**Integrated Server Boundary (MVP):**

- The mediation server is implemented by Next.js server-side runtime in `web/src/app/api/*`.
- Browser code cannot execute CLI commands.
- Browser-originated requests must pass through Next.js API handlers, which invoke CLI adapters server-side.

**API Boundaries:**

- Browser traffic only hits `web/src/app/api/*`.
- API handlers validate input and call CLI adapter only.
- No browser-originated direct Beads calls.

**Component Boundaries:**

- Feature modules in `web/src/features/*` consume typed API client only.
- UI components in `web/src/components/*` remain presentation-focused.
- CLI domain logic stays in `cli/src/core/*`; web never imports this code directly.

**Service Boundaries:**

- CLI is canonical operational boundary for product commands.
- Web server layer is mediation/normalization boundary for browser requests.
- Execution agents can call `bd` directly in bead execution context.

**Data Boundaries:**

- Beads/Dolt is the source of truth for tasks and bead lifecycle.
- Repo-level config is read from project files in Git.
- Residual user/global config comes from `.dotfile`.

### Requirements to Structure Mapping

**Feature/FR Mapping:**

- FR1-FR8 (project/task/bead core): `cli/src/core/models`, `cli/src/core/services`, `web/src/app/api/projects`, `web/src/app/api/beads`
- FR9-FR21 (intake/dispatch/execution): `cli/src/commands/*`, `cli/src/adapters/beads/*`, `web/src/app/api/commands/*`
- FR22-FR26 (cross-project visibility): `web/src/features/cockpit`, `web/src/features/exception-triage`
- FR27-FR32 (repository safety): `cli/src/adapters/beads/bd-runner.ts`, `cli/src/core/services/*` guardrails
- FR33-FR37 (traceability/recovery): `cli/src/telemetry/audit-events.ts`, `web/src/features/bead-detail`, `web/src/components/timeline`
- FR38-FR44 (CLI/guidance/adoption): `cli/src/index.ts`, `docs/operations/*`, root CI workflows

**Cross-Cutting Concerns:**

- Validation: `cli/src/core/validation/*`, `web/src/lib/validation/*`
- Error mapping: `web/src/lib/cli-adapter/map-errors.ts`, `cli/src/adapters/beads/bd-errors.ts`
- Lifecycle enums: `cli/src/core/models/lifecycle.ts`, `web/src/types/lifecycle.ts`
- Audit/logging: `cli/src/telemetry/*`, web request IDs in API routes

### Integration Points

**Internal Communication:**

- `web` feature components -> `web` API client -> API routes -> CLI adapter -> CLI commands.
- CLI commands -> Beads adapter -> `bd` operations.

**External Integrations:**

- Beads runtime via `bd` in CLI and execution-agent contexts.
- Git repository as canonical storage for project-local config.
- Optional future integrations isolated under adapters.

**Data Flow:**

- Read: Beads -> CLI -> web API -> UI projections.
- Write from browser: UI -> web API -> CLI -> Beads.
- Write from direct CLI user: CLI -> Beads.
- Write from execution agent: `bd` -> Beads.

### File Organization Patterns

**Configuration Files:**

- Root: global repo standards and CI.
- `cli/.env.example` and `web/.env.example` separate runtime concerns.
- Config precedence: repo config first, then `.dotfile`, then environment overrides.

**Source Organization:**

- `cli` organized by command/core/adapter boundaries.
- `web` organized by app routes/features/components/lib boundaries.
- No cross-imports between `web` and `cli` source trees.

**Test Organization:**

- Per-project tests in each folder (`cli/tests`, `web/tests`).
- Unit plus integration plus selected e2e in `web`.
- CLI adapter contract tests mandatory.

**Asset Organization:**

- Web static assets in `web/public/assets`.
- CLI help templates/docs under `cli/src` or `docs`.

### Development Workflow Integration

**Development Server Structure:**

- `web` dev server for UI and API routes.
- CLI executable available locally for server adapter and direct user workflows.
- Beads available to both direct CLI and execution-agent contexts.

**Build Process Structure:**

- Independent build/test pipelines for `cli` and `web`.
- Shared guardrail checks at root CI level (contracts, lint, type checks).

**Deployment Structure:**

- Local-first MVP: `web` plus CLI plus Beads on same trust boundary.
- Future hosted web still preserves mediation boundary and approved Beads access paths.

## Architecture Validation Results

### Coherence Validation ✅

**Decision Compatibility:**
All major decisions are compatible:

- Separated `cli/` and `web/` codebases align with independent runtime responsibilities.
- Beads/Dolt as the task source of truth aligns with "all tasks are beads."
- Integrated Next.js server mediation for browser traffic does not conflict with direct CLI user flow or execution-agent `bd` flow.
- Configuration model (repo config plus `.dotfile`) is consistent with local-first MVP operation.

No hard contradictions detected after clarifying access paths:

- Browser path: `web client -> Next API route -> CLI -> Beads`
- Direct user path: `CLI -> Beads`
- Execution-agent path: `bd -> Beads`

**Pattern Consistency:**
Implementation patterns are consistent with architecture:

- Response envelopes and error mapping enforce stable web contracts.
- Shared lifecycle vocabulary prevents state drift across CLI, web, and agents.
- Explicit approved Beads access channels prevent accidental side-path integrations.

**Structure Alignment:**
Project structure supports chosen architecture:

- `cli/` contains canonical command and Beads adapters.
- `web/` contains UI plus integrated server API mediation.
- Boundaries and integration points are clear and enforceable.

### Requirements Coverage Validation ✅

**Epic/Feature Coverage:**
No epic file set was loaded; coverage validated against FR categories from PRD and UX specification.

**Functional Requirements Coverage:**
All FR groups are architecturally supported:

- FR1-FR8 by CLI core models/services and project/bead routes.
- FR9-FR21 by command execution and lifecycle transitions.
- FR22-FR26 by cockpit/status views and projection endpoints.
- FR27-FR32 by guardrails and mediated mutation paths.
- FR33-FR37 by audit events and trace-oriented UI.
- FR38-FR44 by standalone CLI structure and documentation/workflow support.

**Non-Functional Requirements Coverage:**

- Performance: low-friction command paths and server-side mediation.
- Reliability: normalized errors, deterministic envelopes, explicit lifecycle semantics.
- Security/safety: browser mediation boundary, CLI guardrails, trunk-protection design intent.
- Accessibility: web architecture supports UX-defined AA obligations.
- Integration robustness: adapter-based Beads integration and stable contracts.

### Implementation Readiness Validation ✅

**Decision Completeness:**
Critical implementation decisions are documented, including:

- storage model,
- boundary model,
- configuration precedence,
- approved access paths,
- mediation strategy.

**Structure Completeness:**
Directory structure is specific and actionable for implementation agents.

**Pattern Completeness:**
Conflict-prone areas are addressed (naming, formats, error semantics, access paths, lifecycle consistency, and enforcement).

### Gap Analysis Results

**Critical Gaps:** None identified.

**Important Gaps:**

- Auth model intentionally deferred; define trigger conditions and rollout ADR when moving beyond local-first.
- API versioning strategy is defined but should be activated when external/non-web clients are introduced.

**Nice-to-Have Gaps:**

- Add explicit contract-test matrix for all command-to-API mappings.
- Add a concise runtime topology diagram in docs for onboarding.

### Validation Issues Addressed

- Clarified ambiguity around "agent" by separating browser client, direct CLI users, and bead execution agents.
- Clarified integrated server semantics: browser cannot invoke CLI directly; server-side route handlers can.
- Clarified approved Beads access paths to avoid contradictory interpretations.

### Architecture Completeness Checklist

**✅ Requirements Analysis**

- [x] Project context thoroughly analyzed
- [x] Scale and complexity assessed
- [x] Technical constraints identified
- [x] Cross-cutting concerns mapped

**✅ Architectural Decisions**

- [x] Critical decisions documented with versions
- [x] Technology stack fully specified
- [x] Integration patterns defined
- [x] Performance considerations addressed

**✅ Implementation Patterns**

- [x] Naming conventions established
- [x] Structure patterns defined
- [x] Communication patterns specified
- [x] Process patterns documented

**✅ Project Structure**

- [x] Complete directory structure defined
- [x] Component boundaries established
- [x] Integration points mapped
- [x] Requirements to structure mapping complete

### Architecture Readiness Assessment

**Overall Status:** READY FOR IMPLEMENTATION

**Confidence Level:** High

**Key Strengths:**

- Clear and enforceable runtime boundaries.
- Single source of truth for task state (Beads/Dolt).
- Explicit support for three operational paths without ambiguity.
- Strong consistency rules to prevent multi-agent drift.

**Areas for Future Enhancement:**

- Formal auth/authorization evolution plan for hosted/multi-user scenarios.
- Extended observability dashboarding and SLO definitions.
- Optional decomposition of integrated server into separate package if operational complexity grows.

### Implementation Handoff

**AI Agent Guidelines:**

- Follow approved Beads access channels only.
- Keep browser interactions mediated by Next API routes.
- Preserve API envelope/error/lifecycle contracts.
- Treat CLI and execution-agent outputs as first-class state transitions.

**First Implementation Priority:**

1. Bootstrap `cli/` and command contracts.
2. Bootstrap `web/` with integrated API routes.
3. Implement CLI adapter and end-to-end command mediation path.
4. Validate lifecycle parity across web, CLI, and execution-agent flows.