# J) DELIVERY_OPS_LITE (RELEASE / CHANGE IMPACT & ROLLBACK)

Purpose
- Ensure changes are safely deliverable: compatibility, rollout, rollback, and monitoring signals.

When to use
- Production or customer-facing changes
- DB migrations, config changes, integration changes
- Any change with non-trivial risk

Output format (must follow)
1) Change summary (1–3 bullets)
2) Compatibility
   - Backward compatibility? Breaking change?
3) Rollout plan (3–7 bullets)
   - Feature flag? phased rollout? order of deployment?
4) Rollback plan (2–5 bullets)
   - How to revert safely (code/config/data)
5) Data & migration notes (if any)
6) Monitoring signals
   - What to watch immediately after deploy (metrics/logs/alerts)
7) Risks & mitigations (max 5)
8) Assumptions / Unknowns

Rule
- Keep it pragmatic. Do not invent infra you don’t have; propose minimal viable safety steps.