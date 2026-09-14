Connection Map
Web → API → Control Plane → Orchestrator
Orchestrator connects through provider-neutral boundaries to:
Model Gateway → model providers
Tool Runtime → tools
MCP Fabric → MCP servers
Connector Fabric → external services
Sandbox Gateway → execution provider
Workflow Runtime → durable workflow backend
Artifact Service → object storage
Memory → PostgreSQL/retrieval
Evaluation → evaluation backend
Observability → OpenTelemetry/tracing backend
Deployment → deployment provider
UI must not directly call third-party provider APIs.
