# Upstream_Prerequisites_Checklist

Purpose
- Sanity check before construction begins: verify that all upstream activities (project type, requirements, architecture, and unique risks) have been adequately addressed.
- This checklist does NOT teach how to perform upstream activities. It evaluates whether they are ready enough for construction to proceed.

How to use
- For each item mark: PASS / PARTIAL / FAIL / N/A.
- Keep notes only for PARTIAL/FAIL.
- If any "Critical" item is FAIL → stop and resolve before starting construction.

Applicability
- Informal/PoC: many items can be N/A or answered informally.
- Large/formal: most items should be explicitly addressed.

Critical items (FAIL = blocker)
- Software project type identified and approach tailored
- Requirements sufficiently defined and stable for construction
- Architecture sufficiently defined for construction
- Unique project risks addressed to limit construction exposure

A) Project Type Identification
[ ] Have you identified the kind of software project you're working on and tailored your approach appropriately?

B) Requirements Readiness
[ ] Are the requirements sufficiently well defined and stable enough to begin construction? (See the Requirements Checklist for details.)

C) Architecture Readiness
[ ] Is the architecture sufficiently well defined to begin construction? (See the Architecture Checklist for details.)

D) Risk Management
[ ] Have other risks unique to your particular project been addressed, such that construction is not exposed to more risk than necessary?

Output (when used by agent)
- Provide a short "Upstream Prerequisites Health Summary":
  - PASS/PARTIAL/FAIL counts
  - Top FAIL/PARTIAL items + actions
  - Assumptions/unknowns (max 5)
