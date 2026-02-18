<!--
Sync Impact Report:
Version change: 1.0.0 → 1.0.0 (initial constitution for Todo Full-Stack Web Application)
Added sections: Core Principles (6), Additional Constraints, Development Workflow, Governance
Templates requiring updates: N/A (initial creation)
Follow-up TODOs: None
-->

# Todo Full-Stack Web Application Constitution

## Core Principles

### I. Spec-First Development
Every implementation MUST start from and reference specs (@specs/features/task-crud.md, @specs/api/rest-endpoints.md, @specs/database/schema.md, etc.). Update specs first if anything is missing or unclear. No direct code generation without spec alignment. This ensures traceability and consistent understanding across the team.

### II. Agent-Based Implementation
All code changes are generated via agents/skills only. Review outputs strictly. No manual coding allowed. This enforces consistency and ensures all changes follow established patterns and practices.

### III. Multi-User Security & Isolation (NON-NEGOTIABLE)
Strict user isolation on EVERY database query and route. Backend MUST verify JWT independently → extract user_id → enforce user isolation. No data leak possible. Return 401 Unauthorized if no/invalid token. This protects user privacy and prevents data breaches.

### IV. Technology Stack Adherence
Frontend: Next.js 16+ (App Router), TypeScript, Tailwind CSS. Backend: Python FastAPI + SQLModel ORM. Database: Neon Serverless PostgreSQL. Authentication: Better Auth with JWT. This ensures consistency and leverages proven technologies.

### V. API Contract Compliance
Stick exactly to documented endpoints (/api/{user_id}/tasks for list/create, /api/{user_id}/tasks/{id} for get/update/delete, PATCH /api/{user_id}/tasks/{id}/complete). All require valid JWT. Filter responses by authenticated user_id matching path user_id. This ensures predictable and secure API behavior.

### VI. Quality & Testing Mindset
Favor testable code (small functions, dependencies injectable). Global handlers in backend, proper UX feedback (toasts) in frontend. Use indexes, avoid N+1 queries in SQLModel. Follow PEP8 in Python, ESLint/Prettier style in TS/Next.js. This produces maintainable, performant code.

## Additional Constraints

### Technology Stack Requirements
- Monorepo structure: .spec-kit/config.yaml, specs/ (organized by overview.md, features/, api/, database/, ui/), CLAUDE.md (root + frontend/ + backend/), frontend/ (Next.js 16+ App Router), backend/ (FastAPI), docker-compose.yml
- Frontend: Prefer server components. Client components only for interactivity. Use /lib/api.ts for all backend calls.
- Backend: Routes under /api/. Use Pydantic for request/response models. HTTPException for errors.
- Database: Connection via DATABASE_URL env. Models in backend/models.py. Enforce timestamps, indexes (user_id, completed).
- Authentication: Shared secret via BETTER_AUTH_SECRET env var.

### Security Requirements
- User isolation mandatory: every task operation checks ownership via user_id from JWT.
- Input validation: title 1-200 chars required, description ≤1000 chars optional.
- No hard-coded secrets, bypassing auth, global state abuse, inline styles in frontend, raw SQL without SQLModel.

### Performance Standards
- Responsiveness: All UI must be mobile-friendly (Tailwind responsive classes).
- Performance: Use indexes, avoid N+1 queries in SQLModel.
- Clean code: Meaningful names, no duplication.

## Development Workflow

### Process Priorities
1. Read/update relevant spec first.
2. Generate plan (via plan-full-feature skill or main-agent).
3. Delegate to specialized agents/skills (backend-agent, frontend-agent, etc.).
4. Implement → review → test → integrate (docker-compose).
5. Iterate only via spec changes if requirements evolve.

### Review Process
- All changes must be reviewed for constitution compliance
- Verify spec alignment before implementation
- Check security requirements (especially user isolation)
- Validate technology stack adherence

### Quality Gates
- All tests must pass before merging
- Code must follow specified style guides
- API contracts must be respected
- Security requirements must be met

## Governance

This constitution supersedes all other practices for the Todo Full-Stack Web Application project. All development activities must comply with these principles. Amendments require documentation, approval, and migration plan if applicable. All PRs/reviews must verify compliance with these principles. Complexity must be justified with clear benefits.

**Version**: 1.0.0 | **Ratified**: 2026-02-13 | **Last Amended**: 2026-02-13
