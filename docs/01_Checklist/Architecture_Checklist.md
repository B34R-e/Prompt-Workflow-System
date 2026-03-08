# Architecture_Checklist

Purpose
- Pragmatic evaluation of architecture quality from the programmer’s end of the software food chain.
- Not a comprehensive architecture guide. Use it to assess readiness for construction.

How to use
- Read 00_Project_Scope + 01_Problem_Definition + 02_Requirements first.
- For each item mark: PASS / PARTIAL / FAIL / N/A.
- If any “Blocker” item is FAIL → do not proceed with serious construction until addressed.

Applicability
- Informal/PoC: many items can be N/A or informal.
- Large/formal: most items should be explicitly addressed.

Architecture blockers (FAIL = blocker)
- Overall organization clear + justified
- Major building blocks defined (responsibilities + interfaces)
- Requirements covered sensibly by building blocks
- Critical classes described + justified (80/20)
- Data design described + justified (including DB organization)
- Coherent error-handling strategy
- Implementing programmer is comfortable with the architecture

A) Specific Architectural Topics
[ ] Is the overall organization of the program clear, including a good architectural overview and justification?
[ ] Are major building blocks well defined, including their areas of responsibility and their interfaces to other building blocks?
[ ] Are all the functions listed in the requirements covered sensibly, by neither too many nor too few building blocks?
[ ] Are the most critical classes described and justified?
[ ] Is the data design described and justified?
[ ] Is the database organization and content specified?
[ ] Are all key business rules identified and their impact on the system described?
[ ] Is a strategy for the user interface design described?
[ ] Is the user interface modularized so that changes in it won’t affect the rest of the program?
[ ] Is a strategy for handling I/O described and justified?
[ ] Are resource-use estimates and a strategy for resource management described and justified for scarce resources like threads, database connections, handles, network bandwidth, and so on?
[ ] Are the architecture’s security requirements described?
[ ] Does the architecture set space and speed budgets for each class, subsystem, or functionality area?
[ ] Does the architecture describe how scalability will be achieved?
[ ] Does the architecture address interoperability?
[ ] Is a strategy for internationalization/localization described?
[ ] Is a coherent error-handling strategy provided?
[ ] Is the approach to fault tolerance defined (if any is needed)?
[ ] Has technical feasibility of all parts of the system been established?
[ ] Is an approach to overengineering specified?
[ ] Are necessary buy-vs.-build decisions included?
[ ] Does the architecture describe how reused code will be made to conform to other architectural objectives?
[ ] Is the architecture designed to accommodate likely changes?

B) General Architectural Quality
[ ] Does the architecture account for all the requirements?
[ ] Is any part overarchitected or underarchitected? Are expectations in this area set out explicitly?
[ ] Does the whole architecture hang together conceptually?
[ ] Is the top-level design independent of the machine and language that will be used to implement it?
[ ] Are the motivations for all major decisions provided?
[ ] Are you, as a programmer who will implement the system, comfortable with the architecture?

Output (when used by agent)
- Provide a short “Architecture Health Summary”:
  - PASS/PARTIAL/FAIL counts
  - Top 3 risks (impact + mitigation)
  - Missing decisions (max 5)