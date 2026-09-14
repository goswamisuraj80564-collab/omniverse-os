OMNIVERSE OS — EXECUTION SOURCE OF TRUTH
Status: FROZEN FOR INITIAL BUILD / CHANGE-CONTROLLED Project: OMNIVERSE OS Purpose: Canonical execution plan for a brand-new project Rule: No legacy code, folders, dependencies, architecture, credentials, or assumptions from earlier projects may be imported into this repository.
0. NON-NEGOTIABLE PROJECT RULES
This repository starts from zero.
Existing projects such as Rio/Riot/God Node are reference material only; no code is copied into the new repository.
The source of truth is this document plus the current repository state.
Every architectural change must update the Architecture Decision Record (ADR), dependency map, and affected file map before implementation.
No destructive rewrite of a working subsystem without a migration plan and rollback path.
No AI-generated code is trusted merely because an AI produced it. It must pass validation and tests.
No generated/untrusted code runs on the control-plane host. It executes in a sandbox provider.
Production secrets never enter model prompts, source files, logs, artifacts, or memory.
Every external integration is accessed through an adapter/connector boundary.
Every important operation receives an audit event.
Autonomous changes require policy checks; high-risk production changes require human approval.
Provider-specific APIs must not leak into domain logic. Use provider-neutral ports/interfaces.
The initial system is designed to be small enough to build, but every major boundary must be scalable.
“Success” means verified evidence, not a model assertion.
Every release must be reproducible and rollbackable.
1. PRODUCT DEFINITION
OMNIVERSE OS is a programmable layer between human intent and the digital world.
Core promise:
Describe what should exist. The system plans it, builds it, tests it, verifies it, deploys it, observes it, and continuously proposes improvements.
It is not initially positioned as:
a generic chatbot
a simple no-code builder
a single-model wrapper
a single-agent coding assistant
a game engine only
a plugin directory only
The core product is an AI creation and execution operating system.
Primary object hierarchy:
Organization
└── Workspace
    └── Project
        ├── World State
        ├── Artifacts
        ├── Agents
        ├── Tools / Connectors
        ├── Workflows
        ├── Memory
        ├── Policies
        ├── Environments
        ├── Evaluations
        ├── Deployments
        └── Evolution Proposals
2. THE CORE EXECUTION LOOP
Every major request should ultimately pass through a controlled lifecycle:
USER INTENT
   ↓
INTENT COMPILER
   ↓
PLAN / TASK GRAPH
   ↓
POLICY CHECK
   ↓
MODEL ROUTER
   ↓
AGENT RUNTIME
   ↓
TOOL / MCP / CONNECTOR FABRIC
   ↓
SANDBOX
   ↓
BUILD / RUN / TEST
   ↓
EVALUATION + SECURITY
   ↓
VERIFICATION
   ↓
APPROVAL GATE (when required)
   ↓
DEPLOYMENT
   ↓
OBSERVABILITY
   ↓
MEMORY / WORLD STATE UPDATE
   ↓
EVOLUTION PROPOSAL
   ↺
No system component may bypass the execution/policy boundary merely because it is an AI agent.
3. ARCHITECTURAL PRINCIPLES
3.1 Control Plane vs Execution Plane
Control Plane
Responsible for:
identity
project state
orchestration
policies
model routing
connector registry
task state
approvals
audit events
billing/cost state
deployment intents
Execution Plane
Responsible for:
code execution
builds
tests
browser sessions
generated assets
package installation
temporary files
agent workspace
long-running processes
Generated/untrusted code belongs in the execution plane only.
3.2 Ports and Adapters
The domain layer defines contracts. Providers implement adapters.
Examples:
ModelProvider
SandboxProvider
StorageProvider
VectorStoreProvider
IdentityProvider
SearchProvider
DeploymentProvider
ObservabilityProvider
WorkflowProvider
This allows providers to be changed without rewriting the application core.
3.3 Evidence-first execution
A successful task should produce:
changed files
test results
command logs
evaluation results
security checks
artifact references
deployment status
trace ID
final decision
4. TARGET REPOSITORY STRUCTURE
omniverse-os/
│
├── README.md
├── AGENTS.md
├── CONTRIBUTING.md
├── SECURITY.md
├── LICENSE
├── CHANGELOG.md
├── .env.example
├── .gitignore
├── .editorconfig
├── docker-compose.yml
├── Makefile
├── pyproject.toml
├── package.json
├── pnpm-workspace.yaml
│
├── apps/
│   ├── web/
│   │   ├── app/
│   │   ├── components/
│   │   ├── features/
│   │   ├── lib/
│   │   ├── hooks/
│   │   ├── styles/
│   │   └── tests/
│   ├── mobile/
│   └── admin/
│
├── services/
│   ├── api/
│   │   ├── routes/
│   │   ├── dependencies/
│   │   ├── middleware/
│   │   └── tests/
│   ├── control-plane/
│   ├── agent-runtime/
│   ├── workflow-runtime/
│   ├── model-gateway/
│   ├── connector-gateway/
│   ├── sandbox-gateway/
│   ├── artifact-service/
│   ├── evaluation-service/
│   ├── deployment-service/
│   ├── evolution-service/
│   └── notification-service/
│
├── packages/
│   ├── domain/
│   ├── schemas/
│   ├── config/
│   ├── security/
│   ├── policy/
│   ├── agents/
│   ├── tools/
│   ├── mcp/
│   ├── connectors/
│   ├── memory/
│   ├── world-model/
│   ├── models/
│   ├── workflow/
│   ├── storage/
│   ├── deployment/
│   ├── observability/
│   ├── evaluation/
│   ├── billing/
│   └── sdk/
│
├── plugins/
│   ├── official/
│   └── examples/
│
├── connectors/
│   ├── github/
│   ├── storage/
│   ├── communication/
│   ├── databases/
│   ├── payments/
│   └── productivity/
│
├── infra/
│   ├── local/
│   ├── docker/
│   ├── terraform/
│   ├── kubernetes/
│   └── policies/
│
├── migrations/
├── seeds/
├── evals/
├── fixtures/
├── tests/
│   ├── unit/
│   ├── integration/
│   ├── contract/
│   ├── security/
│   └── e2e/
│
├── docs/
│   ├── architecture/
│   ├── adr/
│   ├── api/
│   ├── plugins/
│   ├── connectors/
│   ├── runbooks/
│   └── operations/
│
└── scripts/
    ├── bootstrap/
    ├── checks/
    ├── migrations/
    └── release/
The tree is intentionally larger than v0 because the boundaries are explicit. Empty modules must not be implemented as fake systems; they can remain stubs with contracts until their phase is reached.
5. FILE RESPONSIBILITIES
Root
README.md
Human-readable project entry point. Must contain:
product definition
local setup
architecture link
current phase
development commands
environment requirements
safety notes
links to canonical documents
AGENTS.md
Instructions for coding agents operating in the repository. Must include:
source-of-truth hierarchy
allowed paths
forbidden actions
test requirements
change protocol
migration rules
secret handling
architecture boundaries
CHANGELOG.md
Human-readable release/change history.
.env.example
Only variable names and safe placeholders. Never real credentials.
6. DOMAIN MODEL
Initial canonical entities:
Organization
Workspace
Project
Environment
User
Membership
AgentDefinition
AgentRun
Task
TaskDependency
Workflow
WorkflowRun
ToolDefinition
ToolInvocation
MCPServer
Connector
ConnectorCredential
Plugin
Artifact
ArtifactVersion
MemoryItem
WorldEntity
WorldRelation
Policy
ApprovalRequest
Evaluation
EvaluationRun
Deployment
DeploymentVersion
AuditEvent
UsageRecord
CostRecord
EvolutionProposal
Every entity gets:
immutable ID
tenant/workspace scope where relevant
timestamps
status
version where mutable
provenance where generated
7. WORLD MODEL
The World Model is the project's canonical semantic state.
Initial graph concepts:
Project
 ├─ CONTAINS → Artifact
 ├─ USES → Tool
 ├─ USES → Model
 ├─ HAS → Agent
 ├─ HAS → Policy
 ├─ DEPENDS_ON → Connector
 ├─ PRODUCES → Deployment
 ├─ EVALUATED_BY → Evaluation
 ├─ HAS_MEMORY → MemoryItem
 └─ EVOLVES_TO → Proposal
Initial implementation should use relational tables plus explicit relation records where practical. A dedicated graph database is deferred until workload proves the need.
8. INTENT COMPILER
Input:
natural-language goal
Output:
{
  "goal": "...",
  "constraints": [],
  "capabilities": [],
  "resources": [],
  "permissions": [],
  "budget": {},
  "quality_target": {},
  "deployment_target": {},
  "approval_policy": {},
  "acceptance_tests": []
}
Pipeline:
Parse request.
Identify project scope.
Retrieve relevant project memory.
Resolve available capabilities.
Detect missing requirements.
Build task graph.
Estimate cost/risk.
Determine approval level.
Produce an executable plan.
The intent compiler must not directly execute external actions.
9. AGENT SYSTEM
Agents are typed workforce members, not uncontrolled personas.
Every AgentDefinition contains:
id
name
role
instructions
allowed_tools
allowed_connectors
allowed_models
memory_scope
budget_policy
risk_level
input_schema
output_schema
handoff_policy
approval_policy
Initial agents:
Planner
Architect
Researcher
Builder
CodeReviewer
TestEngineer
SecurityReviewer
UXReviewer
DataEngineer
DeploymentEngineer
CostOptimizer
ReleaseManager
EvolutionAnalyst
Do not activate all of them in v1 runtime. Start with Planner → Builder → Verifier.
10. AGENT ORCHESTRATION
Use a task graph, not an uncontrolled chat swarm.
Task A
 ├── Task B
 ├── Task C
 │    └── Task D
 └── Task E
Every task records:
input references
model used
tools used
sandbox used
output artifacts
retries
state transitions
evidence
cost
trace ID
State must be durable for long-running workflows.
11. MODEL GATEWAY
The Model Gateway is the only approved model access boundary.
Interface:
complete()
stream()
embed()
classify()
transcribe()
generate_image()
generate_video()
moderate()
Provider adapter examples:
OpenAIAdapter
AnthropicAdapter
GoogleAdapter
OpenRouterAdapter
LocalModelAdapter
The actual initial provider list can be decided by deployment budget, availability, and policy at implementation time.
Routing inputs:
capability
quality target
latency target
context size
privacy class
cost ceiling
provider health
model health
availability
Routing strategies:
primary
fallback
cheapest-compatible
best-quality
fastest
privacy-first
task-specialized
Never hard-code provider-specific logic into domain services.
12. COST GOVERNOR
Every model/tool/sandbox invocation receives a budget context.
Project budget
  ↓
Workflow budget
  ↓
Task budget
  ↓
Tool/model budget
Before expensive execution:
estimate cost
compare with remaining budget
apply policy
continue or request approval
Record:
provider
model
input units
output units
cached units if applicable
estimated price
actual price when available
task/project attribution
Rate limits and fallback routing belong behind the model gateway, not in random agents.
13. TOOL RUNTIME
Tools are capability objects with strict schemas.
Each tool contains:
name
version
description
input_schema
output_schema
permissions
risk_level
network_policy
secret_requirements
idempotency_policy
timeout
observability_hooks
Tool classes:
Pure/local tools
API tools
MCP tools
Sandbox tools
Browser/computer tools
Agent-as-tool
All tools pass through policy/observability boundaries.
14. MCP FABRIC
MCP is a first-class connector protocol, not the domain model.
MCP lifecycle:
Discover
 ↓
Register
 ↓
Validate manifest
 ↓
Apply permissions
 ↓
Health check
 ↓
Expose tools/resources
 ↓
Observe
 ↓
Rotate/revoke
MCP server registry fields:
server_id
transport
endpoint
version
publisher
trust_level
permissions
available_tools
available_resources
health_status
credential_ref
Third-party MCP servers run according to their trust class and must not automatically receive broad project access.
15. PLUGIN SYSTEM
Plugin package:
plugin/
├── plugin.yaml
├── manifest.schema.json
├── src/
├── tests/
├── permissions.yaml
├── README.md
└── CHANGELOG.md
Manifest must define:
plugin identity
version
capabilities
dependencies
required secrets
endpoints
permissions
risk class
compatible platform version
health check
installation hooks
rollback metadata
Plugin lifecycle:
SUBMIT
 ↓
STATIC SCAN
 ↓
DEPENDENCY SCAN
 ↓
SANDBOX TEST
 ↓
CONTRACT TEST
 ↓
SECURITY REVIEW
 ↓
PUBLISH
 ↓
MONITOR
 ↓
DEPRECATE / REVOKE
Marketplace is Phase 6+, not a prerequisite for the core engine.
16. CONNECTOR FABRIC
Connector categories:
Source Control
Cloud Storage
Databases
Communication
Payments
Productivity
Search/Web
Design
Analytics
Deployment
AI Providers
Each connector exposes a narrow capability interface.
Example:
GitHubConnector
 ├── list_repos
 ├── read_file
 ├── create_branch
 ├── create_commit
 ├── create_pr
 └── inspect_checks
Agents do not receive raw credentials. They receive scoped connector handles.
17. SANDBOX FABRIC
Required abstraction:
SandboxProvider
 ├── create
 ├── start
 ├── exec
 ├── read_file
 ├── write_file
 ├── install
 ├── snapshot
 ├── restore
 ├── logs
 ├── upload_artifact
 ├── download_artifact
 └── destroy
Initial candidates:
Daytona
E2B
container runtime
managed cloud execution
Use one primary provider first. Keep the interface provider-neutral.
Required controls:
filesystem isolation
network policy
CPU/RAM/time limits
package policy
process limits
secret injection only when authorized
outbound domain policy
artifact scanning
automatic expiration
18. ARTIFACT SYSTEM
Everything generated by the platform is an artifact.
Examples:
source files
builds
binaries
images
video
datasets
test reports
logs
screenshots
evaluation reports
deployment bundles
Artifact metadata:
artifact_id
project_id
run_id
version
hash
mime_type
size
storage_ref
created_by
created_at
provenance
Use content hashes for integrity and deduplication.
19. MEMORY SYSTEM
Four memory levels:
Working Memory
Project Memory
Organization Memory
Knowledge / Retrieval Memory
Memory items need:
source
confidence
scope
timestamp
validity
provenance
embedding where useful
Never store secrets in semantic memory.
Memory write policy:
candidate fact
 ↓
validation
 ↓
provenance
 ↓
deduplication
 ↓
store
20. EVALUATION LAB
Evaluation categories:
Functional correctness
Code quality
Security
Reliability
UX
Cost
Latency
Task completion
Regression
Model quality
Evaluator types:
deterministic tests
schema checks
static analysis
security scanners
code evaluators
LLM-as-judge
human review
production feedback
Every important agent/workflow needs a small regression dataset.
21. VERIFICATION CONTRACT
A task is not SUCCESS merely because a model returned text.
Canonical state model:
PLANNED
RUNNING
WAITING_APPROVAL
VERIFYING
REAL_SUCCESS
DEGRADED_SUCCESS
FAILED
CANCELLED
Rules:
REAL_SUCCESS requires all mandatory acceptance checks.
DEGRADED_SUCCESS requires explicit explanation of incomplete checks.
FAILED means required outcome was not achieved.
No code path may silently turn an error into REAL_SUCCESS.
This is mandatory for all builders and deployment workflows.
22. SECURITY PLANE
Security boundaries:
Identity
Permissions
Secrets
Tool authorization
Sandbox isolation
Network egress
Artifact scanning
Prompt injection defense
Audit logging
Rate limiting
Abuse detection
Deployment approval
Threat model must cover:
malicious prompts
malicious files
hostile webpages
compromised plugins
compromised MCP servers
package supply-chain attacks
credential exfiltration
SSRF
sandbox escape
excessive agency
destructive tool calls
data leakage
23. APPROVAL ENGINE
Risk levels:
LOW
MEDIUM
HIGH
CRITICAL
Examples:
LOW:
read project docs
run unit tests
MEDIUM:
create branches
install packages
HIGH:
modify production configuration
access sensitive external systems
CRITICAL:
production deletion
credential changes
financial action
irreversible migration
High/critical operations require explicit approval unless an organization policy explicitly permits them.
24. OBSERVABILITY
Every major run gets:
trace ID
workflow ID
task ID
agent ID
model call spans
tool spans
sandbox spans
connector spans
evaluation spans
deployment spans
Prefer OpenTelemetry-compatible instrumentation so telemetry is portable.
External systems may include Langfuse or an equivalent observability/evaluation system.
Do not leak secrets or full sensitive user content into traces.
25. DEPLOYMENT FABRIC
Deployment abstraction:
DeploymentProvider
 ├── validate
 ├── build
 ├── deploy
 ├── health
 ├── logs
 ├── rollback
 └── destroy
Target types:
web app
API service
worker
scheduled job
container
static site
generated game/world package
Every deployment version must point to an immutable artifact set.
26. DIGITAL TWIN
A project twin is a simulated representation of the deployed system.
Initial uses:
synthetic users
API load
workflow simulation
failure injection
UX test scenarios
cost simulation
configuration comparison
The twin should never write to real production systems by default.
27. EVOLUTION ENGINE
Evolution pipeline:
Observe
 ↓
Detect opportunity/problem
 ↓
Generate proposals
 ↓
Estimate impact
 ↓
Simulate
 ↓
Evaluate
 ↓
Human approval if required
 ↓
Create change
 ↓
Deploy canary
 ↓
Measure
 ↓
Promote / rollback
Evolution proposals must contain:
problem
hypothesis
change
expected_gain
expected_cost
risk
affected_components
evaluation_plan
rollback_plan
No uncontrolled self-modifying production code.
28. UI / PRODUCT DESIGN SYSTEM
The UI is a control center, not a toy chatbot.
Primary surfaces:
Dashboard
Project Workspace
Intent Composer
Agent Activity
Plan / Task Graph
File Explorer
Live Preview
Sandbox Terminal
Artifacts
Evaluations
Deployments
Integrations
Plugins
Costs
Security
Audit
Evolution
Settings
Project screen should allow:
conversational intent
plan inspection
task approval
live progress
evidence inspection
diff review
preview
deployment control
Mobile is a control surface. Desktop/web remains the richer engineering surface.
29. VOICE LAYER
Voice is an interface to the same intent system, not a separate brain.
Pipeline:
Audio
 ↓
Speech recognition
 ↓
Intent compiler
 ↓
Normal execution path
 ↓
Voice/text response
This avoids duplicating business logic between voice and text.
30. INITIAL API SURFACE
Representative endpoints:
POST   /v1/projects
GET    /v1/projects/:id
POST   /v1/projects/:id/intents
GET    /v1/runs/:id
POST   /v1/runs/:id/approve
POST   /v1/runs/:id/cancel
GET    /v1/runs/:id/trace
GET    /v1/tasks/:id
POST   /v1/tools/:id/invoke
GET    /v1/connectors
POST   /v1/connectors
GET    /v1/plugins
POST   /v1/plugins
GET    /v1/artifacts/:id
POST   /v1/deployments
POST   /v1/deployments/:id/rollback
GET    /v1/evaluations
GET    /v1/costs
GET    /v1/audit
API schemas live in packages/schemas and are versioned.
31. DATABASE FOUNDATION
Initial recommended baseline:
PostgreSQL
 ├── identity references
 ├── projects
 ├── tasks
 ├── workflows
 ├── agents
 ├── tools
 ├── connectors
 ├── policies
 ├── approvals
 ├── artifacts metadata
 ├── deployments
 ├── evaluations
 ├── memory metadata
 ├── audit events
 └── cost records
Semantic retrieval may start with PostgreSQL + pgvector.
Object storage:
S3-compatible storage / R2 / equivalent
Do not add a separate graph database or dedicated vector database until a measurable requirement exists.
32. INITIAL TECHNOLOGY BASELINE
The exact language choice must be recorded before code begins. Recommended split:
Web
TypeScript + React/Next.js or equivalent modern web stack.
Core services
Python is recommended for AI/orchestration-heavy services, with TypeScript available for front-end and connector SDKs.
Data
PostgreSQL.
Cache/queue
Redis-compatible service only when needed; do not introduce it simply because it is familiar.
Observability
OpenTelemetry-compatible instrumentation + selected evaluation/tracing provider.
Execution
One sandbox provider initially.
Models
One primary production provider plus one fallback provider. Additional models are added only behind ModelGateway.
Containers
OCI/Docker-compatible packaging.
33. DEPENDENCY POLICY
Dependency categories:
CORE
SECURITY-SENSITIVE
RUNTIME
DEVELOPMENT
OPTIONAL PROVIDER
Rules:
Pin production dependency ranges deliberately.
Record why every major dependency exists.
Run vulnerability scanning.
Avoid duplicate libraries solving the same core problem.
Optional providers live in adapters.
SDK upgrades require compatibility tests.
Never install arbitrary packages from an agent into the control plane.
34. CONNECTION MAP
Web
 ↓
API
 ↓
Control Plane
 ├── Auth
 ├── Policy
 ├── Project State
 ├── Orchestrator
 └── Audit

Orchestrator
 ├── Model Gateway → AI Providers
 ├── Tool Runtime → Local Tools
 ├── MCP Fabric → MCP Servers
 ├── Connector Fabric → External Services
 ├── Sandbox Gateway → Sandbox Provider
 ├── Workflow Runtime → Durable Workflow Backend
 ├── Artifact Service → Object Storage
 ├── Memory → PostgreSQL / Retrieval
 ├── Evaluation → Eval backend
 ├── Observability → OTel / tracing backend
 └── Deployment → Deployment Provider
No UI component directly talks to third-party provider APIs.
35. BOOTSTRAP ORDER
This is the exact recommended build order.
Phase 0 — Governance
Create:
repository
README.md
AGENTS.md
SOURCE_OF_TRUTH document
ADR template
SECURITY.md
CONTRIBUTING.md
.env.example
CI skeleton
Acceptance:
clean clone works
no secrets
documentation renders
Phase 1 — Domain + Schemas
Create:
domain entities
IDs
statuses
API schemas
error model
event model
Acceptance:
schema tests pass
migrations are repeatable
Phase 2 — Database + API
Build:
Postgres
migration system
project CRUD
task/run persistence
health endpoint
structured errors
Acceptance:
local API works
integration tests pass
Phase 3 — Model Gateway
Build:
provider interface
primary adapter
fallback adapter
model registry
usage records
cost estimation
Acceptance:
one request can route through gateway
fallback works in tests
Phase 4 — Agent Runtime
Build only:
Planner
Builder
Verifier
Acceptance:
prompt → plan → build → verify → evidence
Phase 5 — Sandbox
Connect one sandbox provider.
Acceptance:
create
execute
stream logs
persist workspace where needed
snapshot
destroy
Phase 6 — Tools + MCP
Build the tool registry and MCP boundary.
Acceptance:
tool discovery
schema validation
permissions
invocation trace
failure handling
Phase 7 — Memory + World State
Build project memory and world relations.
Acceptance:
retrieve relevant state
store decisions
provenance available
Phase 8 — Evaluation + Observability
Build:
traces
task metrics
eval runner
regression suite
cost analytics
Acceptance:
every run has evidence
regressions are detected
Phase 9 — Deployment
Build:
artifact packaging
deployment adapter
health checks
rollback
Phase 10 — Connector / Plugin Platform
Add official connectors first. Marketplace comes later.
Phase 11 — Digital Twin
Add simulated users and scenarios.
Phase 12 — Evolution Engine
Proposal → simulation → evaluation → approval → canary → rollback.
Phase 13 — Advanced Creation
Games, 3D worlds, media pipelines, advanced asset generation.
Phase 14 — Agent Economy / Marketplace
Only after trust, permissions, billing, sandboxing and evaluation are stable.
36. FIRST VERTICAL SLICE
Before building everything, deliver exactly one complete path:
User
 ↓
Create Project
 ↓
Prompt: “Build a small web app that does X”
 ↓
Intent Compiler
 ↓
Planner
 ↓
Builder
 ↓
Sandbox
 ↓
Tests
 ↓
Verifier
 ↓
Artifact
 ↓
Preview
 ↓
Deploy
 ↓
Evidence
This vertical slice is the foundation. Do not jump to multi-agent complexity before it works.
37. FIRST DEMO ACCEPTANCE CRITERIA
A first demo is acceptable only if:
A user can create a project.
A user can submit natural-language intent.
The system produces a structured plan.
The system can execute code in a sandbox.
Generated code is testable.
Failed steps are represented as failures.
Evidence is shown.
The user can inspect the changes.
The result can be previewed.
No secret is exposed.
The run is traceable.
Costs can be attributed.
38. CHANGE-CONTROL PROTOCOL
When the project changes:
REQUEST
 ↓
CLASSIFY
 ↓
IMPACT ANALYSIS
 ↓
UPDATE THIS SOURCE OF TRUTH
 ↓
ADR (if architectural)
 ↓
FILE MAP
 ↓
IMPLEMENT
 ↓
TEST
 ↓
VERIFY
 ↓
UPDATE CHANGELOG
If a requested change conflicts with this architecture, do not silently implement it. Explain the conflict and propose the smallest compatible change.
39. CONTEXT-LOSS / HANDOFF PROTOCOL
This section exists specifically so work can continue without relying on conversational memory.
At the end of every major build session update:
docs/operations/CURRENT_STATE.md
It must contain:
current phase
current milestone
completed items
active item
blocked items
next exact commands/actions
files changed
tests passed
tests failing
pending decisions
dependencies added/removed
provider connections currently active
secrets required (names only, never values)
migration status
rollback instructions
The repository itself is the handoff mechanism.
40. “DO NOT FORGET” FILE SET
These files must remain current:
README.md
AGENTS.md
CHANGELOG.md
.env.example
docs/architecture/SYSTEM_ARCHITECTURE.md
docs/architecture/CONNECTION_MAP.md
docs/architecture/DEPENDENCY_MAP.md
docs/architecture/FILE_MAP.md
docs/architecture/WORKFLOW_MAP.md
docs/operations/CURRENT_STATE.md
docs/adr/*
This SOURCE_OF_TRUTH file governs all of them.
41. RECOVERY RULE
If conversational context is lost:
Read README.md.
Read this file.
Read CURRENT_STATE.md.
Read latest ADRs.
Inspect repository status.
Run health/tests.
Only then continue implementation.
Never reconstruct architecture from memory when the repository contains the canonical record.
42. MODEL / PROVIDER HEALTH
Track per provider:
availability
latency
error rate
rate-limit events
cost
output quality
safety events
Model routing can then select a provider based on actual evidence rather than static assumptions.
43. FAILURE HANDLING
Every external call needs:
timeout
retry policy
idempotency strategy
circuit breaker where warranted
fallback where safe
structured error
trace context
Never retry non-idempotent destructive operations blindly.
44. ASYNCHRONOUS WORK
Long-running actions use durable workflow execution.
Examples:
large builds
deployment
simulations
evaluations
media generation
dataset processing
bulk artifact generation
The API returns a run/task reference rather than holding an HTTP request open indefinitely.
45. MULTI-TENANCY FOUNDATION
Even the first version should carry tenant/workspace IDs through relevant persistence and authorization boundaries.
Do not depend on application code alone to separate tenant data.
Every query path must have explicit scope.
46. SECRETS
Secret flow:
User connects provider
 ↓
Credential store
 ↓
Scoped reference
 ↓
Authorized runtime
 ↓
Ephemeral injection
 ↓
Execution
 ↓
Secret removed from environment/logs
Never put API keys in:
prompts
Git
artifacts
telemetry
memory
screenshots
47. BROWSER / COMPUTER USE
Browser automation is powerful and risky.
Treat it as a high-capability tool with:
explicit domains
session isolation
credential scope
action logging
upload/download controls
approval for sensitive actions
It is a Phase 3+ capability, not part of the first core loop.
48. MEDIA / 3D / GAME EXTENSION
The creation engine is intentionally extensible.
Future capability modules:
Text
Image
Video
Audio
3D assets
3D scenes
Physics
NPC simulation
World generation
Game packaging
These must plug into the same artifact, tool, sandbox, evaluation and deployment contracts.
The core platform should not become coupled to a single 3D/game engine.
49. DESIGN QUALITY BAR
Every generated product must be evaluated on:
accessibility
responsive layout
performance
interaction consistency
visual hierarchy
error states
loading states
empty states
mobile usability
keyboard usability where relevant
AI-generated UI is not considered complete because it looks impressive in one screenshot.
50. PERFORMANCE TARGETS
Initial targets should be measured, not guessed.
Track:
API p50/p95 latency
first-token latency
tool latency
sandbox startup time
workflow duration
database query latency
artifact upload time
deployment time
cost per successful task
Only optimize after instrumentation exists.
51. TEST STRATEGY
Unit
Domain functions, policies, routing, schemas.
Contract
Provider and connector interfaces.
Integration
Database, queue/workflow, sandbox, storage.
Security
Prompt/tool injection, authorization, secrets, sandbox boundaries.
E2E
Intent → build → verify → deploy.
Regression
Known projects/tasks rerun against new versions.
52. CI/CD QUALITY GATES
Pull request checks:
format
lint
type check
unit tests
contract tests
security scan
dependency scan
build
Release checks:
integration tests
e2e smoke test
database migration check
artifact integrity
rollback test
53. INITIAL REPOSITORY BOOTSTRAP CHECKLIST
Before writing product logic:
create empty repository
initialize git
define license
create README
create AGENTS.md
create SOURCE_OF_TRUTH
create ADR template
create .env.example
configure formatting/linting/type checks
configure CI
create base package boundaries
create health endpoint
create app configuration
create test harness
create migration harness
verify clean clone
Only after this is complete should Phase 1 implementation begin.
54. CURRENT NEXT ACTIONS — EXACT ORDER
The next implementation session must do only the following in order:
Step 1
Create the fresh repository.
Step 2
Create the root governance/documentation files.
Step 3
Create the directory tree with empty or minimal contract files.
Step 4
Implement configuration + health check + structured logging.
Step 5
Implement domain IDs/statuses/schemas.
Step 6
Implement PostgreSQL migrations and project/task/run persistence.
Step 7
Implement the first API endpoints.
Step 8
Implement ModelProvider + ModelGateway using one provider.
Step 9
Implement Planner/Builder/Verifier contracts.
Step 10
Connect one sandbox provider.
Step 11
Complete the first vertical slice.
Step 12
Run tests, security checks and evidence review.
Step 13
Only after the vertical slice is stable, add MCP/connectors/memory.
Do not start marketplace, digital twin, game engine, autonomous evolution, or multi-provider complexity before the vertical slice works.
55. SUCCESS DEFINITION FOR THE PROJECT
The project is moving correctly when complexity is increasing after reliability, not before it.
The sequence is:
FOUNDATION
 → VERTICAL SLICE
 → RELIABILITY
 → MULTI-AGENT
 → CONNECTORS
 → MEMORY
 → EVALUATION
 → SCALE
 → EVOLUTION
 → CREATION WORLDS
That is the master execution strategy.
56. EXTERNAL RESEARCH BASIS
The architecture is informed by current documented patterns including:
OpenAI Agents SDK — agents, tools, handoffs, guardrails, sessions, MCP integration and tracing.
Model Context Protocol — standardized tool/resource/prompt connectivity.
Cloudflare AI Gateway — provider routing, analytics, rate limiting, retries, model fallback and caching patterns.
Daytona — isolated sandboxes, code/process execution, persistence and resource isolation.
Langfuse — prompt versioning, traces, evaluation and production feedback loops.
OpenTelemetry — vendor-neutral telemetry primitives.
Temporal — durable execution patterns for long-running workflows.
PostgreSQL/pgvector — relational source of truth plus initial semantic retrieval option.
These references are not dependencies by default. They establish patterns; the implementation must remain modular.
57. SOURCE-OF-TRUTH HIERARCHY
When documents disagree, use this order:
Current repository code + tests for actual behavior.
This execution source of truth for intended architecture.
Latest ADR for an approved exception/decision.
CURRENT_STATE.md for current work status.
README for human-facing overview.
Conversation/chat history for context only.
If code violates the architecture, record the discrepancy; do not silently rewrite it.
58. FINAL RULE
The platform must always be able to answer:
What is this system doing? Why is it doing it? Which model did it use? Which tools did it call? What changed? Where did it run? What evidence proves success? How much did it cost? What can be rolled back? What should happen next?
If the platform cannot answer these questions, it is not ready to be considered a reliable autonomous creation system.
