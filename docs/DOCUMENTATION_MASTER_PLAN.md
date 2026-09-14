OMNIVERSE OS — Documentation Master Plan
Status: PLANNING / DOCUMENTATION ARCHITECTURE Purpose: Convert the OMNIVERSE OS execution architecture into a complete, machine-readable, upgradeable documentation system before implementation.
0. Governing rule
This file does not replace OMNIVERSE_EXECUTION_SOURCE_OF_TRUTH.md.
Hierarchy:
Repository code + tests = actual behavior.
OMNIVERSE_EXECUTION_SOURCE_OF_TRUTH.md = intended master architecture.
ADRs = approved architectural decisions and exceptions.
This file = documentation-system blueprint.
CURRENT_STATE.md = live project status.
Other docs = subsystem detail.
No implementation starts until the documentation map is stable enough to guide the first vertical slice.
1. Design goals
The documentation system must be:
Human-readable.
AI-readable.
Cross-linked.
Non-duplicative.
Versionable in Git.
Explicit about dependencies and connections.
Explicit about inputs, outputs, states, events, permissions, failure behavior, tests, and rollback.
Provider-neutral.
Capability-extensible.
Safe for autonomous coding agents.
Useful after long gaps in conversation.
Usable from a phone as the primary control surface.
Detailed enough to support advanced implementation without forcing premature complexity.
2. Repository documentation tree
omniverse-os/
├── README.md
├── AGENTS.md
├── CONTRIBUTING.md
├── SECURITY.md
├── CHANGELOG.md
├── .env.example
├── OMNIVERSE_EXECUTION_SOURCE_OF_TRUTH.md
│
└── docs/
    ├── architecture/
    │   ├── SYSTEM_ARCHITECTURE.md
    │   ├── CONTROL_PLANE_MAP.md
    │   ├── EXECUTION_PLANE_MAP.md
    │   ├── CONNECTION_MAP.md
    │   ├── DATA_FLOW_MAP.md
    │   ├── EVENT_FLOW_MAP.md
    │   ├── WORKFLOW_MAP.md
    │   ├── FILE_MAP.md
    │   ├── DEPENDENCY_MAP.md
    │   ├── TRUST_BOUNDARY_MAP.md
    │   ├── INTENT_ARCHITECTURE.md
    │   ├── PROJECT_WORLD_ARCHITECTURE.md
    │   ├── AGENT_ARCHITECTURE.md
    │   ├── ORCHESTRATION_ARCHITECTURE.md
    │   ├── MODEL_GATEWAY_ARCHITECTURE.md
    │   ├── COST_GOVERNOR_ARCHITECTURE.md
    │   ├── MEMORY_ARCHITECTURE.md
    │   ├── CONTEXT_ARCHITECTURE.md
    │   ├── DECISION_ARCHITECTURE.md
    │   ├── capabilities/
    │   │   ├── CAPABILITY_ARCHITECTURE.md
    │   │   ├── CAPABILITY_DISCOVERY.md
    │   │   ├── CAPABILITY_REGISTRY.md
    │   │   ├── CAPABILITY_RESOLUTION.md
    │   │   ├── CAPABILITY_LIFECYCLE.md
    │   │   ├── TOOL_ARCHITECTURE.md
    │   │   ├── TOOL_RUNTIME.md
    │   │   ├── TOOL_DISCOVERY.md
    │   │   ├── MCP_ARCHITECTURE.md
    │   │   ├── PLUGIN_ARCHITECTURE.md
    │   │   ├── PLUGIN_LIFECYCLE.md
    │   │   ├── CONNECTOR_ARCHITECTURE.md
    │   │   ├── CONNECTOR_LIFECYCLE.md
    │   │   ├── PROVIDER_ARCHITECTURE.md
    │   │   └── EXTENSION_ARCHITECTURE.md
    │   ├── execution/
    │   │   ├── SANDBOX_ARCHITECTURE.md
    │   │   ├── EXECUTION_RUNTIME.md
    │   │   ├── ARTIFACT_ARCHITECTURE.md
    │   │   ├── BROWSER_COMPUTER_USE.md
    │   │   ├── MEDIA_EXECUTION.md
    │   │   ├── BUILD_EXECUTION.md
    │   │   └── JOB_EXECUTION.md
    │   ├── security/
    │   │   ├── SECURITY_ARCHITECTURE.md
    │   │   ├── IDENTITY_ARCHITECTURE.md
    │   │   ├── AUTHORIZATION_ARCHITECTURE.md
    │   │   ├── SECRET_ARCHITECTURE.md
    │   │   ├── TRUST_MODEL.md
    │   │   ├── THREAT_MODEL.md
    │   │   ├── SUPPLY_CHAIN_SECURITY.md
    │   │   ├── PROMPT_INJECTION_DEFENSE.md
    │   │   ├── SANDBOX_SECURITY.md
    │   │   └── DATA_PROTECTION.md
    │   ├── verification/
    │   │   ├── VERIFICATION_ARCHITECTURE.md
    │   │   ├── APPROVAL_ARCHITECTURE.md
    │   │   ├── EVALUATION_ARCHITECTURE.md
    │   │   ├── QUALITY_GATES.md
    │   │   └── FAILURE_HANDLING.md
    │   ├── platform/
    │   │   ├── API_ARCHITECTURE.md
    │   │   ├── API_VERSIONING.md
    │   │   ├── DATABASE_ARCHITECTURE.md
    │   │   ├── DATA_MODEL.md
    │   │   ├── EVENT_ARCHITECTURE.md
    │   │   ├── STORAGE_ARCHITECTURE.md
    │   │   ├── SEARCH_ARCHITECTURE.md
    │   │   ├── VECTOR_ARCHITECTURE.md
    │   │   ├── CONFIGURATION_ARCHITECTURE.md
    │   │   └── TENANCY_ARCHITECTURE.md
    │   └── operations/
    │       ├── OBSERVABILITY_ARCHITECTURE.md
    │       ├── LOGGING_ARCHITECTURE.md
    │       ├── AUDIT_ARCHITECTURE.md
    │       ├── WORKFLOW_RUNTIME.md
    │       ├── RELIABILITY_ARCHITECTURE.md
    │       ├── DEPLOYMENT_ARCHITECTURE.md
    │       ├── RELEASE_ARCHITECTURE.md
    │       ├── ROLLBACK_ARCHITECTURE.md
    │       ├── DIGITAL_TWIN_ARCHITECTURE.md
    │       ├── EVOLUTION_ENGINE.md
    │       ├── MEDIA_3D_ARCHITECTURE.md
    │       ├── GAME_WORLD_ARCHITECTURE.md
    │       └── SCALING_ARCHITECTURE.md
    │
    ├── contracts/
    │   ├── INTENT_CONTRACT.md
    │   ├── PROJECT_CONTRACT.md
    │   ├── TASK_CONTRACT.md
    │   ├── AGENT_CONTRACT.md
    │   ├── MODEL_CONTRACT.md
    │   ├── TOOL_CONTRACT.md
    │   ├── CAPABILITY_CONTRACT.md
    │   ├── PLUGIN_CONTRACT.md
    │   ├── CONNECTOR_CONTRACT.md
    │   ├── MCP_CONTRACT.md
    │   ├── SANDBOX_CONTRACT.md
    │   ├── ARTIFACT_CONTRACT.md
    │   ├── MEMORY_CONTRACT.md
    │   ├── EVALUATION_CONTRACT.md
    │   ├── VERIFICATION_CONTRACT.md
    │   ├── DEPLOYMENT_CONTRACT.md
    │   └── EVENT_CONTRACT.md
    │
    ├── knowledge/
    │   ├── SYSTEM_INDEX.md
    │   ├── COMPONENT_INDEX.md
    │   ├── CONNECTION_INDEX.md
    │   ├── CONTRACT_INDEX.md
    │   ├── DEPENDENCY_INDEX.md
    │   ├── EVENT_INDEX.md
    │   ├── STATE_MACHINE_INDEX.md
    │   ├── CAPABILITY_INDEX.md
    │   └── DECISION_INDEX.md
    │
    ├── engineering/
    │   ├── CODING_STANDARDS.md
    │   ├── ARCHITECTURE_RULES.md
    │   ├── API_RULES.md
    │   ├── DATABASE_RULES.md
    │   ├── TESTING_RULES.md
    │   ├── SECURITY_RULES.md
    │   ├── DEPENDENCY_RULES.md
    │   ├── ERROR_HANDLING.md
    │   ├── LOGGING_RULES.md
    │   ├── OBSERVABILITY_RULES.md
    │   ├── MIGRATION_RULES.md
    │   ├── VERSIONING_RULES.md
    │   └── CHANGE_CONTROL.md
    │
    ├── operations/
    │   ├── CURRENT_STATE.md
    │   ├── HANDOFF.md
    │   ├── NEXT_ACTIONS.md
    │   ├── RELEASE_STATE.md
    │   └── INCIDENT_STATE.md
    │
    └── adr/
        ├── 000-template.md
        └── numbered decisions...
3. File classification
3.1 Canonical
These govern the project:
OMNIVERSE_EXECUTION_SOURCE_OF_TRUTH.md
README.md
AGENTS.md
docs/operations/CURRENT_STATE.md
ADRs
3.2 Architecture reference
Explains how subsystems fit together. Architecture docs must not silently override the source of truth.
3.3 Contracts
Define machine-checkable boundaries. Contract files should be stable and referenced by code tests.
3.4 Knowledge/index
Optimized for discovery by people and AI systems. Index files link to authoritative documents; they must not become a second source of truth.
3.5 Engineering rules
Implementation standards that constrain code without duplicating domain architecture.
3.6 Operational state
Mutable operational documents. CURRENT_STATE.md is the live status record.
4. Standard template for every architecture MD
Every architecture document uses this structure unless there is a clear reason not to:
# Title
Status
Authority
Scope
Purpose
Non-goals
Upstream dependencies
Downstream consumers
Inputs
Outputs
Core components
Internal connections
External connections
Data owned
Events emitted
Events consumed
State machine
Security boundary
Permissions
Failure modes
Retry / idempotency
Observability
Cost considerations
Performance considerations
Testing requirements
Rollback / recovery
Upgrade path
Implementation phases
Open decisions
Related contracts
Related ADRs
Related source-of-truth sections
Related code paths
5. Standard template for every contract MD
# Contract
Status
Owner
Version
Purpose
Schema / interface
Inputs
Outputs
Errors
State transitions
Preconditions
Postconditions
Idempotency
Timeouts
Security requirements
Compatibility rules
Backward compatibility
Test cases
Related architecture
6. Master system connection graph
Human / Voice / Mobile / Web
            |
            v
      Intent Interface
            |
            v
      Intent Compiler
            |
            v
       Task / Plan Graph
            |
            v
        Policy Engine
            |
            +----------------------+
            |                      |
            v                      v
   Capability Fabric          Cost Governor
            |
    +-------+--------+---------+----------+-------+
    |       |        |         |          |       |
    v       v        v         v          v       v
  Models  Tools    Plugins    MCP    Connectors  APIs
    |       |        |         |          |       |
    +-------+--------+---------+----------+-------+
            |
            v
      Agent Runtime
            |
            v
     Workflow Runtime
            |
            v
      Sandbox Fabric
            |
       +----+----+
       |         |
       v         v
     Build     Execute
       |         |
       +----+----+
            |
            v
        Evaluation
            |
            v
        Verification
        /          \
     success      failure
       |            |
       v            v
   Artifact       Recovery
       |
       v
   Deployment
       |
       v
 Observability / Audit
       |
       v
 Memory / World State
       |
       v
 Evolution Proposal
       |
       +---------> next controlled change
7. Master responsibility model
Interfaces
Own intent capture and presentation only.
API
Own request validation, authentication context propagation, and orchestration entry points.
Control plane
Own project state, policies, orchestration, approvals, cost state, capability metadata, and audit state.
Capability fabric
Own discovery and lifecycle of usable capabilities.
Agent runtime
Own agent behavior and task execution decisions within declared permissions.
Model gateway
Own model selection and provider access.
Tool runtime
Own normalized tool invocation.
Sandbox fabric
Own untrusted execution.
Artifact service
Own immutable artifact metadata and storage references.
Evaluation
Own quality measurement.
Verification
Own final evidence-based state transitions.
Deployment
Own release execution and rollback.
Observability
Own traces, metrics, logs, and audit correlation.
8. Universal capability architecture
Capability is the common language between user intent and execution providers.
A capability record should conceptually contain:
capability_id
name
version
category
publisher
provider
manifest
input_schema
output_schema
required_permissions
required_secrets
network_policy
runtime_requirements
dependencies
compatibility
risk_level
trust_level
cost_profile
latency_profile
health
installation_state
lifecycle_state
provenance
observability_hooks
rollback_metadata
Capability lifecycle
DISCOVERED
  -> CANDIDATE
  -> VALIDATING
  -> APPROVED
  -> REGISTERED
  -> READY
  -> RUNNING
  -> DEGRADED
  -> DISABLED
  -> REVOKED
Automatic capability resolution
Task requirement
    -> capability query
    -> installed capability scan
    -> registry discovery
    -> candidate ranking
    -> policy check
    -> trust check
    -> dependency check
    -> compatibility check
    -> cost check
    -> sandbox/preparation
    -> registration
    -> execution
Automatic preparation is never equivalent to unrestricted host execution.
9. Tool / plugin / MCP / connector relationship
Capability
├── Native Tool
├── MCP Tool
├── Plugin Capability
├── Connector Capability
├── Model Capability
├── Sandbox Capability
└── External API Capability
They share a common capability contract but retain protocol-specific implementations.
10. Provider-neutral boundaries
At minimum:
ModelProvider
SandboxProvider
StorageProvider
VectorStoreProvider
IdentityProvider
SearchProvider
WorkflowProvider
DeploymentProvider
ObservabilityProvider
No provider SDK imports should leak into domain code.
11. State architecture
Core state categories:
Project state
Task state
Run state
Workflow state
Agent state
Capability state
Tool state
Connector state
Sandbox state
Artifact state
Evaluation state
Approval state
Deployment state
Evolution proposal state
All state machines require explicit transitions and rejection of invalid transitions.
12. Event architecture
Events are facts, not commands.
Core event families:
Intent events
Plan events
Task events
Agent events
Model events
Tool events
Capability events
Connector events
Sandbox events
Artifact events
Evaluation events
Verification events
Approval events
Deployment events
Security events
Cost events
Evolution events
Every important event should carry:
event_id
event_type
version
timestamp
tenant_id
workspace_id
project_id
run_id
causation_id
correlation_id
actor
payload
provenance
13. Data ownership rules
PostgreSQL remains the initial system of record.
Objects belong in object storage when they are large or immutable.
Search/retrieval is a derived capability, not the primary source of truth.
Graph databases are deferred until measurable workload justifies them.
14. API architecture
API layers:
Public API
Internal service API
Provider adapter API
Capability API
Agent runtime API
Workflow API
Event API
Admin API
Version externally visible APIs.
Do not expose internal provider details through public contracts.
15. Security architecture
Security controls must exist at:
Identity
Authorization
Policy
Capability selection
Tool execution
Connector access
Secret injection
Network egress
Sandbox
Artifact handling
Deployment
Audit
High-risk operations require approval unless explicit organization policy permits them.
16. Phone-first architecture
The phone is the primary control surface, not the primary compute plane.
Mobile responsibilities
Authentication
Project selection
Intent input
Voice input
Plan review
Approval
Run monitoring
Logs/evidence viewing
Diff review
Artifact viewing
Preview
Deployment control
Rollback approval
Costs
Security alerts
Notifications
Cloud execution responsibilities
AI inference
Agent runtime
Workflow execution
Builds
Sandboxing
Media generation
Database
Object storage
Evaluation
Deployment
Observability
This keeps the mobile experience lightweight while preserving powerful backend execution.
17. Mobile reliability model
The mobile app must tolerate:
intermittent connectivity
background suspension
slow networks
reconnects
partial responses
long-running jobs
The UI should use durable run IDs and server state rather than relying on one open HTTP connection.
Core mobile sync concept:
Mobile intent
 -> server run created
 -> mobile may disconnect
 -> server continues
 -> mobile reconnects
 -> run state restored
 -> evidence displayed
18. Implementation layers
Layer 0 — Governance
Documentation, repository rules, CI, security policy.
Layer 1 — Contracts
IDs, schemas, states, events, ports.
Layer 2 — Persistence
PostgreSQL, migrations, artifact metadata.
Layer 3 — Control plane
Projects, policies, orchestration, approvals.
Layer 4 — Model gateway
Provider-neutral AI access.
Layer 5 — Agent runtime
Planner, Builder, Verifier first.
Layer 6 — Execution
Sandbox and tool runtime.
Layer 7 — Capability fabric
Capability registry/discovery/resolution.
Layer 8 — Evaluation/observability
Evidence and quality.
Layer 9 — Deployment
Preview, staging, production, rollback.
Layer 10 — Extensions
Plugins, connectors, MCP marketplace.
Layer 11 — Advanced systems
Digital twin, evolution, 3D/game/media.
19. First vertical slice
The first production-shaped path is:
Mobile/Web
 -> Intent
 -> Compile
 -> Plan
 -> Policy
 -> Planner
 -> Builder
 -> Sandbox
 -> Tests
 -> Verifier
 -> Artifact
 -> Preview
 -> Deploy
 -> Evidence
The first vertical slice should prove the architecture before platform breadth is expanded.
20. Documentation completion gates
Documentation is considered ready for implementation only when:
every major subsystem has an owner document;
every critical cross-boundary has a contract;
every major connection appears in a connection map;
state machines are explicit;
failure paths exist;
security boundaries are documented;
provider dependencies are isolated;
phone/cloud responsibilities are explicit;
upgrade paths are stated;
related ADRs are discoverable;
FILE_MAP.md identifies the code location and tests;
CURRENT_STATE.md can recover the work without chat history.
21. Implementation acceptance gates
A subsystem cannot be marked complete solely because its code runs.
Minimum gate:
Design
+ Contract
+ Implementation
+ Unit tests
+ Integration/contract tests
+ Security checks
+ Observability
+ Failure handling
+ Documentation
+ Rollback/recovery plan
22. Upgrade strategy
Every subsystem must expose a stable boundary before provider-specific optimization.
Upgrade sequence:
Contract
 -> implementation
 -> measurements
 -> bottleneck discovery
 -> new adapter/version
 -> compatibility tests
 -> migration
 -> canary
 -> promote
 -> rollback if needed
Never perform large rewrites merely to adopt a new provider.
23. What not to overbuild early
Do not implement all future capabilities at once.
Keep interfaces ready for:
multiple models
multiple sandboxes
multiple storage providers
plugin marketplace
MCP ecosystem
media and 3D
game/world generation
digital twin
evolution engine
But activate only the smallest set needed to make the first vertical slice real and reliable.
24. Final documentation production order
Produce and review documents in this order:
Existing 8 canonical files — audit and align.
Governance docs.
SYSTEM_ARCHITECTURE.md.
Control/execution/connection/data/event maps.
Core intelligence architecture.
Capability architecture family.
Execution and sandbox architecture.
Security architecture.
Verification/evaluation architecture.
Platform/data/API architecture.
Contracts.
Knowledge indexes.
Engineering rules.
Operations and deployment.
ADRs for decisions that become concrete during implementation.
25. Final rule
Do not generate documentation merely to increase the number of files.
Every file must answer at least one important question that another engineer or AI agent would otherwise have to guess.
The final documentation system must make these questions answerable:
What is OMNIVERSE?
What is the current state?
What is the intended architecture?
What owns this responsibility?
How does A connect to B?
What data crosses the boundary?
Which events are emitted?
Which permissions are required?
Where can this code execute?
Which provider is involved?
What happens when it fails?
How do we test it?
How do we observe it?
How do we roll it back?
How do we upgrade it?
What must an AI agent read before modifying it?
How can the phone control the system safely?
If a future change cannot be placed cleanly inside these rules, stop and update the architecture/ADR before coding.
