Dependency Map
Core dependencies must be kept minimal.
Required foundation
PostgreSQL
one primary model provider
one sandbox provider
object storage
authentication
Optional/replaceable providers
model providers
workflow engine
vector database
graph database
observability/evaluation backend
deployment provider
All provider dependencies must be isolated behind adapters.
