# Detailed Design — Overview

This folder contains per-Major-Block detailed designs, created after Architecture (HLD) is complete.

## Purpose
- Bridge between Architecture (what are the major pieces) and Implementation (build & test).
- Each file describes the internal structure of one Major Block: classes, methods, data flow, error handling.

## When to create
- After `04_Architecture/` is finalized and before implementation begins.
- One file per Major Block identified in Architecture.

## File naming
- `{MajorBlockName}.md` — e.g., `Auth_Module.md`, `Search_Engine.md`, `API_Gateway.md`

## What each file should contain
1. **Block overview** — purpose, responsibilities, boundaries
2. **Internal components** — classes/modules/functions with signatures
3. **Data flow** — input → processing → output within the block
4. **Dependencies** — external services, packages, other blocks
5. **Error handling strategy** — how failures are handled within this block
6. **Open questions** — unknowns to resolve during implementation

## Cross-cutting concerns
Document concerns that span multiple blocks here in `_overview.md`:
- Logging strategy
- Authentication/authorization flow
- Configuration management
- Shared data models / DTOs
