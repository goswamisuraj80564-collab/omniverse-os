OMNIVERSE OS
An AI creation and execution operating system: intent → plan → build → verify → deploy → evolve.
Start here
Read OMNIVERSE_EXECUTION_SOURCE_OF_TRUTH.md.
Read docs/operations/CURRENT_STATE.md when it exists.
Read the latest ADRs under docs/adr/.
Follow AGENTS.md before changing code.
Project rule
This is a brand-new project. Do not import code, dependencies, folders, credentials, or architecture from earlier projects.
Initial build target
The first vertical slice is:
user intent → structured plan → agent build → isolated sandbox → tests → verification → artifact → preview → deploy → evidence
Everything else is layered on top of this foundation.
Source of truth
The canonical execution plan is:
OMNIVERSE_EXECUTION_SOURCE_OF_TRUTH.md
The repository is the durable handoff mechanism. Do not rely on chat history to recover project state.
