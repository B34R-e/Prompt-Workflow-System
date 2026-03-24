# Major_Construction_Practices_Checklist

Purpose
- Sanity check before and during construction: verify that key coding, teamwork, QA, and tooling practices have been consciously chosen.
- This checklist does NOT teach construction practices. It evaluates whether decisions have been made.

How to use
- For each item mark: PASS / PARTIAL / FAIL / N/A.
- Keep notes only for PARTIAL/FAIL.
- If any "Critical" item is FAIL → stop and resolve before continuing construction.

Applicability
- Informal/PoC: many items can be N/A or answered informally.
- Large/formal: most items should be explicitly addressed.

Critical items (FAIL = blocker)
- Coding conventions defined (names, comments, layout)
- Architecture-implied coding practices defined (error handling, security, class interfaces)
- Revision control tool selected
- Language and framework selected

A) Coding
[ ] Have you defined how much design will be done up front and how much will be done at the keyboard, while the code is being written?
[ ] Have you defined coding conventions for names, comments, and layout?
[ ] Have you defined specific coding practices that are implied by the architecture, such as how error conditions will be handled, how security will be addressed, what conventions will be used for class interfaces, what standards will apply to reused code, how much to consider performance while coding, and so on?
[ ] Have you identified your location on the technology wave and adjusted your approach to match? If necessary, have you identified how you will program into the language rather than being limited by programming in it?

B) Teamwork
[ ] Have you defined an integration procedure—that is, have you defined the specific steps a programmer must go through before checking code into the master sources?
[ ] Will programmers program in pairs, or individually, or some combination of the two?

C) Quality Assurance
[ ] Will programmers write test cases for their code before writing the code itself?
[ ] Will programmers write unit tests for their code regardless of whether they write them first or last?
[ ] Will programmers step through their code in the debugger before they check it in?
[ ] Will programmers integration-test their code before they check it in?
[ ] Will programmers review or inspect each other's code?

D) Tools
[ ] Have you selected a revision control tool?
[ ] Have you selected a language and language version or compiler version?
[ ] Have you selected a framework such as J2EE or Microsoft .NET or explicitly decided not to use a framework?
[ ] Have you decided whether to allow use of nonstandard language features?
[ ] Have you identified and acquired other tools you'll be using—editor, refactoring tool, debugger, test framework, syntax checker, and so on?

Output (when used by agent)
- Provide a short "Construction Practices Health Summary":
  - PASS/PARTIAL/FAIL counts
  - Top FAIL/PARTIAL items + actions
  - Assumptions/unknowns (max 5)
