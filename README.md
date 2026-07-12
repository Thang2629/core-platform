# core-platform

> Shared monorepo foundation for: `ai-workspace`, `commerce-platform`.
> Contains auth, user management, RBAC, design system, and reusable packages — avoiding the need for every flagship product to rebuild its own infrastructure from scratch.

## 🎯 Why this repo exists

Instead of building 2-3 standalone products, the core parts (authentication, permissions, UI kit, API client) are extracted into a shared foundation — saving time while demonstrating architectural thinking: modularization, package reuse, monorepo management.

## 🛠️ Tech Stack

- **Monorepo**: Turborepo, pnpm workspaces
- **Backend**: NestJS, Prisma, PostgreSQL, Redis (cache/session)
- **Shared frontend**: React, TypeScript, TailwindCSS, Storybook
- **Infra**: Docker, GitHub Actions (CI)

## 📁 Structure

```
core-platform/
├── apps/
│   └── api/                 # Shared NestJS backend
├── packages/
│   ├── ui/                  # Design system (Storybook)
│   ├── auth-core/           # JWT, refresh token, RBAC guard/decorator
│   ├── api-client/          # Typed fetch wrapper + React Query hooks
│   ├── db/                  # Prisma schema, migrations
│   └── config/              # Shared eslint, tsconfig, prettier
└── docs/
    └── features/            # One .md file per feature (see convention below)
```

## ✅ Modules (MVP)

| Module | Description | Status |
|---|---|---|
| Auth | Register, login, refresh token rotation, logout | ⬜ |
| User | Profile CRUD, avatar | ⬜ |
| RBAC | Role, Permission, Guard/Decorator | ⬜ |
| UI Kit | Button, Input, Modal, Toast, Form primitives | ⬜ |
| API Client | Typed client + React Query integration | ⬜ |
| File Upload | Shared upload service (S3/Cloudinary) | ⬜ |
| Notification | Email/in-app notification service | ⬜ |
| CI/CD | Lint, test, build pipeline for the whole monorepo | ⬜ |

> Switch ⬜ → ✅ when done. Each completed module should have a matching file under `docs/features/`.

## 📝 Feature doc convention (for AI agent)

When a feature/module is complete, create `docs/features/<feature-name>.md` using this template:

```markdown
# [Feature name]

## Problem
What business/technical problem needs solving?

## Solution
The main approach and flow (can include a mermaid sequence diagram).

## Architecture & Technical Decisions
- Why this approach instead of alternatives?
- What trade-offs were accepted?

## Usage
Code snippet showing how another app in the monorepo consumes this module.

## What's missing / Roadmap
What hasn't been done yet, planned extensions.
```

Suggested prompt for the AI agent:
> "Read the code in `packages/auth-core` and write `docs/features/auth-jwt-refresh.md` following the template in the README, focusing on explaining the architectural decisions and trade-offs, not just listing the API."

## 🔗 Related repos

- [`ai-workspace`](../ai-workspace) — uses `auth-core`, `ui`, `api-client`
- [`commerce-platform`](../commerce-platform) — uses `auth-core`, `ui`, `api-client`
