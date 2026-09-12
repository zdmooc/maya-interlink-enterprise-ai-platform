Never commit secrets.

Provide:

```text
.env.example
Secret templates
External Secrets / Vault / Sealed Secrets patterns where appropriate

```

All real credentials stay outside Git.

---

# 34. EVENT PLATFORM

Applications must use Kafka-compatible event contracts.

Use a lightweight Kafka-compatible option locally if needed.

Enterprise target should demonstrate Kafka architecture suitable for regulated payments.

Required patterns:

```text
schema/versioning
correlation IDs
idempotency
outbox
DLQ
replay
audit
event retention
observability

```

---

# 35. DATA PLATFORM

Baseline components may include:

```text
PostgreSQL
Qdrant
MinIO/S3
Kafka

```

Integrate Snowflake conceptually and technically when credentials/environment are available.

Keep vector database choice behind an abstraction where practical.

Because existing TradeOps assets use Qdrant, evaluate reuse before replacing it.

---

# 36. OPENSHIFT AI / OPEN DATA HUB

Study Red Hat AI Accelerator patterns.

Capabilities should eventually include:

```text
OpenShift AI / Open Data Hub Operator
DataScienceCluster
Data Science Projects
Workbenches
Pipelines
Model Registry
Model Serving
KServe
vLLM
GPU Operator where relevant
NFD
Serverless where relevant
Service Mesh where relevant

```

Do not install every operator merely because it exists.

Every component must have a demonstrated requirement.

---

# 37. MODEL SERVING

Enterprise target:

```text
OpenShift AI
   ↓
KServe
   ↓
vLLM
   ↓
GPU

```

Local fallback may use:

```text
small CPU model
Ollama
small vLLM-compatible model where resources permit
remote model through AI Gateway

```

The platform must work even when the developer laptop has no enterprise GPU.

---

# 38. ENTERPRISE AI GATEWAY

Implement an abstraction between applications and model providers.

For executable baseline evaluate/reuse:

```text
LiteLLM

```

For enterprise/reference architecture evaluate:

```text
Envoy AI Gateway

```

The gateway should conceptually support:

```text
multi-provider routing
authentication
authorization
rate limiting
quotas
budget controls
fallback
model aliases
provider abstraction
logging
metrics
cost tracking

```

Create an ADR comparing the options.

---

# 39. RAG

Build RAG as an enterprise capability, not just a notebook.

Include:

```text
document ingestion
chunking
embedding
vector storage
retrieval
context filtering
metadata
data classification
citations/evidence
evaluation
observability

```

Initial corpus can contain:

```text
synthetic payment runbooks
ISO 20022 documentation created for the project
payment operating procedures
architecture standards
incident procedures

```

Do not embed copyrighted/proprietary documents without permission.

---

# 40. AGENTS

Agent architecture must follow explicit state transitions.

A baseline pattern may be:

```text
PLAN
  ↓
RETRIEVE
  ↓
TOOL CALLS
  ↓
EVALUATE
  ↓
DECIDE
  ↓
HUMAN REVIEW when required

```

Reuse generic patterns from `TradeOps-GenAI-Integration` where valuable.

Refactor domain-specific trading concepts out.

---

# 41. MCP

Build payment-oriented MCP tools such as:

```text
payment.get_status
payment.get_iso_message
payment.get_history
kafka.get_events
observability.get_logs
observability.get_metrics
runbook.search
reconciliation.get_status

```

MCP servers must implement security controls:

```text
authentication where appropriate
tool allowlisting
timeouts
input validation
output validation
rate limiting
logging
secret redaction
no arbitrary shell execution

```

---

# 42. LLMOPS

Implement:

```text
prompt versioning
evaluation datasets
model configuration
model aliases
deployment promotion
rollback
RAG evaluation
agent evaluation
cost evaluation
latency evaluation
security evaluation

```

Use Promptfoo or another well-justified evaluation tool.

Integrate evaluation into CI.

---

# 43. AI OBSERVABILITY

Use OpenTelemetry as the common telemetry foundation.

For AI-specific observability evaluate/implement Phoenix first unless a better current option is justified.

Track:

```text
requests
latency
TTFT where available
tokens
cost
model
provider
RAG retrieval
agent steps
tool calls
errors
evaluation scores
confidence

```

Avoid deploying multiple overlapping observability products without a demonstrated need.

---

# 44. PLATFORM OBSERVABILITY

Use:

```text
Prometheus
Grafana
OpenTelemetry

```

Potentially integrate existing Dynatrace/ELK knowledge as reference architectures without making proprietary tooling mandatory.

Expose:

```text
infrastructure metrics
OpenShift metrics
application metrics
Kafka metrics
payment business metrics
AI metrics
SLOs

```

---

# 45. FINOPS

Use OpenCost where appropriate.

Demonstrate:

```text
cluster cost
namespace cost
application cost
AI workload cost
GPU cost where available
model/inference cost
cost per business transaction

```

Eventually correlate:

```text
cost per million payments
cost per million tokens

```

---

# 46. GREENOPS

Use Kepler or equivalent where technically feasible.

Demonstrate the architecture for:

```text
energy
CPU/resource utilisation
workload efficiency
AI inference efficiency

```

Potential metrics:

```text
energy per workload
energy per payment
energy per 1M inference tokens

```

GreenOps must not block the core platform if laptop resources are insufficient.

Make it an optional profile.

---

# 47. SRE

Implement:

```text
SLI
SLO
SLA modelling
health checks
readiness
liveness
capacity
HA
DR
RPO
RTO
runbooks
postmortems
alerting

```

---

# 48. FAILURE INJECTION

The platform must demonstrate failures.

Eventually support commands such as:

```bash
make failure-kafka
make failure-payment-timeout
make failure-database
make failure-llm
make failure-rag

```

and recovery/investigation:

```bash
make investigate
make recover

```

The Payment Investigation Agent should analyse synthetic failures.

---

# 49. INTERVIEW DEMONSTRATION PROFILES

Create:

```text
demos/
├── enterprise-architect/
├── azure-solution-architect/
├── aws-solution-architect/
├── gcp-solution-architect/
├── openshift-architect/
├── ai-platform-architect/
└── payment-solution-architect/

```

Every interview profile must eventually contain:

```text
README.md
DEMO-SCRIPT.md
ARCHITECTURE.md
TALK-TRACK.md
QUESTIONS-TO-EXPECT.md
VERIFY.md

```

Where technically possible also provide:

```text
run.sh
verify.sh

```

---

# 50. ENTERPRISE ARCHITECT INTERVIEW DEMO

Show:

```text
business problem
capability map
TOGAF
ArchiMate
AS-IS
TARGET
gap analysis
roadmap
transition architecture
governance
ADRs

```

---

# 51. AZURE INTERVIEW DEMO

Show:

```text
landing zone
network
identity
security
private connectivity
ARO
AI services / Foundry
Terraform
OpenShift integration
AI platform deployment

```

---

# 52. AWS INTERVIEW DEMO

Show:

```text
accounts
VPC
routing
identity
security
ROSA
AI provider integration
Terraform
OpenShift integration
AI platform deployment

```

---

# 53. GCP INTERVIEW DEMO

Show:

```text
organisation/projects
Shared VPC
network
IAM
OpenShift
AI provider integration
Terraform foundation
AI platform deployment

```

---

# 54. OPENSHIFT INTERVIEW DEMO

Show:

```text
cluster
nodes
projects
RBAC
SCC
operators
storage
network
Argo CD
Kyverno
observability
HA/DR
OpenShift AI / ODH
model serving

```

---

# 55. AI PLATFORM ARCHITECT INTERVIEW DEMO

Show:

```text
OpenShift AI / ODH
AI Gateway
models
model serving
RAG
agents
MCP
LLMOps
evaluation
AI observability
governance
FinOps

```

---

# 56. PAYMENT SOLUTION ARCHITECT INTERVIEW DEMO

Show:

```text
ISO 20022
Payment API
Payment orchestration
Kafka
SCT / SCT Inst
reconciliation
resilience
Payment Investigation Agent

```

---

# 57. SINGLE INTERVIEW ENTRY POINT

Eventually support:

```bash
make interview PROFILE=enterprise
make interview PROFILE=azure
make interview PROFILE=aws
make interview PROFILE=gcp
make interview PROFILE=openshift
make interview PROFILE=ai-platform
make interview PROFILE=payments

```
