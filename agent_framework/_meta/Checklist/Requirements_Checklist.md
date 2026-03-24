# Requirements_Checklist

Purpose
- Sanity check during construction: assess how solid your requirements are (requirements Richter scale).
- This checklist does NOT teach requirements development. It evaluates what you have.

How to use
- For each item mark: PASS / PARTIAL / FAIL / N/A.
- Keep notes only for PARTIAL/FAIL.
- If any “Critical” item is FAIL → stop/back up and fix requirements before serious construction.

Applicability
- Informal/PoC: many items can be N/A or answered informally.
- Large/formal: most items should be explicitly addressed.

Critical items (FAIL = blocker)
- Inputs specified (source/accuracy/range/frequency)
- Outputs specified (destination/accuracy/range/frequency/format)
- User tasks specified
- Requirements avoid specifying design
- Requirements are testable
- Success and failure definitions included

A) Specific Functional Requirements
[ ] Are all the inputs to the system specified, including their source, accuracy, range of values, and frequency?
[ ] Are all the outputs from the system specified, including their destination, accuracy, range of values, frequency, and format?
[ ] Are all output formats specified for Web pages, reports, and so on?
[ ] Are all the external hardware and software interfaces specified?
[ ] Are all the external communication interfaces specified, including handshaking, error-checking, and communication protocols?
[ ] Are all the tasks the user wants to perform specified?
[ ] Is the data used in each task and the data resulting from each task specified?

B) Specific Nonfunctional (Quality) Requirements
[ ] Is the expected response time, from the user’s point of view, specified for all necessary operations?
[ ] Are other timing considerations specified, such as processing time, data-transfer rate, and system throughput?
[ ] Is the level of security specified?
[ ] Is the reliability specified, including the consequences of software failure, the vital information that needs to be protected from failure, and the strategy for error detection and recovery?
[ ] Are minimum machine memory and free disk space specified?
[ ] Is the maintainability of the system specified, including its ability to adapt to changes in specific functionality, changes in the operating environment, and changes in its interfaces with other software?
[ ] Is the definition of success included? Of failure?

C) Requirements Quality
[ ] Are the requirements written in the user’s language? Do the users think so?
[ ] Does each requirement avoid conflicts with other requirements?
[ ] Are acceptable tradeoffs between competing attributes specified—for example, between robustness and correctness?
[ ] Do the requirements avoid specifying the design?
[ ] Are the requirements at a fairly consistent level of detail?
[ ] Are the requirements clear enough to be turned over to an independent group for construction and still be understood? Do the developers think so?
[ ] Is each item relevant to the problem and its solution? Can each item be traced to its origin in the problem environment?
[ ] Is each requirement testable? Will it be possible for independent testing to determine whether each requirement has been satisfied?
[ ] Are all possible changes to the requirements specified, including the likelihood of each change?

D) Requirements Completeness
[ ] Where information isn’t available before development begins, are the areas of incompleteness specified?
[ ] Are the requirements complete in the sense that if the product satisfies every requirement, it will be acceptable?
[ ] Are you comfortable with all the requirements? Have you eliminated requirements that are impossible to implement and included just to appease your customer or your boss?

Output (when used by agent)
- Provide a short “Requirements Health Summary”:
  - PASS/PARTIAL/FAIL counts
  - Top 3 FAIL/PARTIAL items + actions
  - Assumptions/unknowns (max 5)