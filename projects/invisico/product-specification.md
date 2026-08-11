---
title: "Invisico — Product Specification & Architecture"
type: project
ingested_via: gitlab-clone
ingested_at: 2026-08-11
git_source: git@gitlab.com:spottmedia/invisico.git
repo_path: /opt/hermes/workspace/invisico-repo
---

# Invisico — Product Specification & Architecture

**Source:** `git@gitlab.com:spottmedia/invisico.git`  
**Status:** Live SaaS product (MVP shipped)  
**Canonical docs:** `docs/project-guide.md`, `CLAUDE.md`

---

## What It Is

A **decision-support application** (not a chatbot). Users describe a problem; the system assembles a council of 3 counselors with distinct reasoning styles, then delivers perspectives + structured synthesis that surfaces disagreements and trade-offs.

**Core insight:** The cognitive friction between perspectives produces better decisions.

---

## Target User

- **Primary**: CEOs, founders, senior leaders making consequential decisions
- **Secondary**: Ambitious professionals seeking structured thinking frameworks
- **NOT**: casual self-help, students, general consumers

---

## How It Works: The Council Engine Pipeline

```
User describes problem
  → Coordinator (1 LLM call: interpret, select counselors, frame brief, identify tensions)
  → Persona Runner (3 parallel calls: each counselor responds independently)
  → Synthesis Engine (1 LLM call: surface agreements, disagreements, reflection question)
  → Context Manager (1 LLM call: summarize session for follow-ups)
  → Store + render
```

**Call budget:**
- Initial session: 6 LLM calls total
- Follow-up round: 5 LLM calls (reuses same counselors)
- Max follow-ups per session: 5

---

## Technology Stack

| Layer | Choice |
|-------|--------|
| **Backend** | Python 3.12+, FastAPI, Uvicorn |
| **Database** | SQLModel (SQLAlchemy + Pydantic), PostgreSQL |
| **Frontend** | Nuxt 4 SPA (`ssr: false`) + Nuxt UI v4 + Tailwind v4 + Pinia |
| **LLM** | Anthropic Claude API (direct async, no LangChain) |
| **Auth** | Email + password (bcrypt), JWT with `jti` claim |
| **Deployment** | Docker Compose (backend, platform, Postgres, Valkey, edge proxy) |
| **Task runner** | `just` with modular `.just/` recipes |
| **Secrets** | Doppler |
| **Infrastructure** | Single server (46.101.73.49) |

**Deliberately NOT using:** React, Redis, Celery, vector DBs, LangChain, Kubernetes, OAuth.

---

## Counselor Personas (Library)

Each counselor has a distinct archetype and system prompt. Loaded at startup from YAML.

| Name | Archetype | Domains | Role |
|------|-----------|---------|------|
| Marcus Aurelius | Philosopher | ethics, leadership, personal | wisdom & principle |
| Charlie Munger | Strategist | strategy, financial, leadership | contrarian thinking |
| Peter Drucker | Operator | operational, leadership, strategy | systems & execution |
| Steve Jobs | Builder | strategy, operational, personal | design & integration |
| Warren Buffett | Life Alignment | financial, personal, strategy | long-term perspective |

**Authenticity standard (binding on all user-facing surfaces):** Invisico simulates **perspectives informed by** thinkers' published ideas, never the people themselves, never endorsed by them. Copy must be "informed by / AI interpretation," never "chat with / meet" or first-person biographical "I."

---

## Repository Structure

### Key Directories

```
invisico-repo/
├── docs/                      # Canonical project docs
│   ├── project-guide.md       # THIS (master file index)
│   ├── north-star.md          # Mission, core insight, success definition
│   ├── prd.md                 # Product requirements
│   ├── mvp-spec.md            # Most detailed spec (scope, data model, acceptance)
│   ├── architecture.md        # System architecture, data flow, security
│   ├── stack.md               # Tech choices with justifications
│   ├── roadmap.md             # Phased delivery plan
│   ├── decision-log.md        # Assumptions, conflicts, exclusions
│   ├── policy/authenticity-attribution-standard.md  # BINDING on all surfaces
│   ├── platform/              # Conventions (auth, docker, nuxt, testing, etc.)
│   └── decisions/ADR-*.md     # Architecture decision records
├── backend/                   # FastAPI app
│   ├── app/
│   │   ├── models/            # SQLModel definitions
│   │   ├── schemas/           # Pydantic request/response
│   │   ├── services/          # Business logic
│   │   ├── routes/            # API endpoints
│   │   └── counselors/        # Persona execution
│   └── tests/
├── clients/                   # Frontend (Nuxt 4 SPA)
│   ├── nuxt/                  # Main app
│   └── assets/
├── counselors/                # Persona YAML (loaded at startup)
├── infra/                     # Infrastructure-as-code
├── ops/                       # DevOps scripts
│   ├── nginx/                 # Prod edge config (built as container)
│   └── postgres/              # Database backups
├── .just/                     # Modular just recipes
├── CLAUDE.md                  # Agent-specific background (52KB, conventions, gotchas)
├── AGENTS.md                  # Non-Claude agent notes
├── docker-compose.yml         # Dev services
├── docker-compose.prod.yml    # Prod overrides
├── Caddyfile                  # Dev edge proxy config
├── .infra-contract.yml        # Authoritative infra requirements
└── .gitlab-ci.yml             # CI/CD pipeline
```

---

## Network & Edge Topology

**Single-hop to backend:**
```
client → edge proxy (Caddy in dev, nginx in prod) → backend:8000 OR platform:3000
```

**Prod setup (46.101.73.49):**
- No DigitalOcean Load Balancer
- No Cloudflare proxy
- No external CDN / WAF
- DNS via DNSMadeEasy; A-records point straight at droplet
- SSL via `acme.sh` on host (managed in `.infra-contract.yml`)
- Edge proxy IS the trust boundary
- Prod nginx: container `registry.gitlab.com/spottmedia/invisico/nginx:<tag>`, built from `ops/nginx/`

**IP header trust (critical for auth):**
- `X-Real-IP` = trusted (set by nginx from TCP remote; clients cannot spoof)
- `X-Forwarded-For` = append-only (safe for rate-limiting, unsafe for auth)

**Reference files (in reading order):**
1. `.infra-contract.yml` — authoritative services, runtime, ports, secrets, reverse-proxy type
2. `docker-compose.prod.yml` — prod-specific overrides
3. `ops/nginx/templates/*.{inc,template}` — prod edge config
4. `Caddyfile` — dev edge config

---

## Key Conventions & Standards

### Spelling
**American English throughout:** counselor (not counsellor), behavior (not behaviour), center (not centre), organize (not organise).

Exception: third-party identifiers and verbatim quotes keep original spelling.

### Frontend
- `main.css` MUST start with `@import "tailwindcss"` then `@import "@nuxt/ui"`
- `ssr: false` for FastAPI-backed SPA
- Nuxt UI v4: `:data` not `:rows`, `onSelect` not `click`, `:items` not `:options`
- **NO "moustaches"** — admin `<h1>` elements must NOT be preceded by redundant `<p>` captions
- **Dark mode:** use token-relative opacity classes (`text-primary-500/N`), never hard-coded `bg-white` (defeats dark mode)
- Page containers: global chrome uses `max-w-5xl`, content may narrow to `max-w-3xl`

### Backend
- App code in `backend/app/`
- Models in `backend/app/models/` (one per file)
- Schemas in `backend/app/schemas/` (separate from models)
- `psycopg2-binary` for database driver
- `utcnow()` helper: `datetime.now(UTC).replace(tzinfo=None)` (never `datetime.utcnow()`)
- Verify migrations with `alembic history` after creating revisions

### Auth (Tier 1 security)
- Pinia auth store (single boundary)
- JWT with `jti` claim from day one
- 4h default expiry, 24h max for rememberMe
- Password validation: 8+ chars, letter+digit, common password check
- All write endpoints require auth
- Resource ownership checks mandatory
- Inactive account check during login
- Dummy bcrypt for non-existent users (timing attack prevention)

### Docker
- Only `DOPPLER_TOKEN` and `NODE_ENV` in docker-compose.yml
- Named volumes for deps (node_modules, .venv)
- Healthchecks on postgres with `condition: service_healthy`
- Every runtime dependency in `depends_on`
- `.local` TLD for development

### Scratch Files
**Never write temp files to repo root.** Use designated folders:
- Screenshots → `.screenshots/`
- Self-review reports → `.scratch/`
- Playwright MCP state → `.playwright-mcp/` (gitignored)

All three in `.gitignore`, never committed. Any file in root that isn't a tracked project artefact is a bug.

---

## Development Workflow

### Run locally
```bash
just backend-test              # Tests via backend container
just frontend-test             # Frontend tests
just dev                       # Full stack (Compose)
```

### Deployment
Container test → push to GitLab registry → pull on prod droplet → `docker-compose -f docker-compose.prod.yml up -d`.

**Canonical test command:** `just backend-test` (runs inside container, not host).

---

## Core Files to Read First

1. **`docs/project-guide.md`** — master index and product overview
2. **`docs/mvp-spec.md`** — most detailed spec (data model, acceptance criteria)
3. **`CLAUDE.md`** — architecture, conventions, gotchas, network topology (52KB)
4. **`docs/policy/authenticity-attribution-standard.md`** — binding on all UX
5. **`docs/roadmap.md`** — phased delivery plan

---

## Known Gotchas & Rules

- **Prod edge config NOT in ops repo.** Everything is in THIS repo: `.infra-contract.yml`, `docker-compose.prod.yml`, `ops/nginx/`.
- **No request-scoped variables in global log formatter** (would break structured logging).
- **Host key verification** on GitLab/GitHub requires setup; use `StrictHostKeyChecking=no` if needed.
- **Test failures on host.** Canonical test path is `just backend-test` (inside container), not bare `pytest` on host.
- **Dark-mode breakers.** Hard-coded `bg-white`, `bg-black` without dark pair defeat dark mode. Use token-relative opacity instead.

---

## What Is NOT Included (By Design)

- Vector databases
- Celery / async task queue
- Redis (using Valkey instead)
- LangChain (direct Claude API calls)
- Kubernetes / orchestration
- OAuth (email+password only)
- General consumer features (e.g., account recovery, public share links)

---

## Success Metrics & North Star

See `docs/north-star.md` for:
- Definition of success (users making better decisions = observable behavior shift)
- Non-goals (NOT a tutoring app, NOT a therapist, NOT a brainstorm generator)
- Core tension (depth vs. accessibility; we choose depth)

---

## Contact & Ownership

- **Git repo:** `git@gitlab.com:spottmedia/invisico.git`
- **Prod server:** `46.101.73.49`
- **Infrastructure owner:** Simon Potter
- **Docs maintained:** SpottMedia platform team

