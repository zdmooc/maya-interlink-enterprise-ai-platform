The same platform is shown from different architectural viewpoints.

Do NOT create seven independent platforms.

---

# 58. MAKEFILE UX

The repository must have a discoverable command surface.

Eventually:

```bash
make help

```

should expose groups such as:

```text
ENVIRONMENT
make doctor
make status
make clean

LOCAL
make local-up
make local-down

PLATFORM
make platform-install
make platform-verify

AI
make ai-install
make ai-verify

PAYMENTS
make demo-sct
make demo-sctinst
make demo-wero
make demo-payment-investigation

GENAI
make demo-rag
make demo-agent

OBSERVABILITY
make monitoring
make dashboards

TESTS
make lint
make test
make smoke
make e2e
make resilience

ARCHITECTURE
make architecture
make diagrams

EVIDENCE
make evidence

CLOUD
make cloud-plan
make cloud-apply
make cloud-destroy

INTERVIEW
make interview PROFILE=<profile>

```

All commands should be idempotent where reasonably possible.

---

# 59. EVIDENCE

A demonstration must produce proof.

Create an evidence mechanism such as:

```text
evidence/
└── runs/
    └── <timestamp>/
        ├── SUMMARY.md
        ├── cluster-info.txt
        ├── nodes.txt
        ├── pods.txt
        ├── routes.txt
        ├── argocd-apps.txt
        ├── policies.txt
        ├── payment-request.xml
        ├── payment-response.xml
        ├── kafka-events.json
        ├── agent-decision.json
        ├── rag-results.json
        ├── evaluation-results.json
        └── metrics.txt

```

Do not commit secrets into evidence.

Redact credentials/tokens automatically.

---

# 60. CI/CD

Create GitHub Actions incrementally.

Eventually validate:

```text
Markdown
YAML
Shell
Python
Java where applicable
Terraform
Kustomize
Helm
Kubernetes manifests
Kyverno
container images
security
secrets
LLM evaluations

```

Potential tools:

```text
yamllint
shellcheck
ruff
pytest
terraform fmt
terraform validate
tflint
checkov where useful
kubeconform
helm lint
kyverno test
gitleaks
trivy
promptfoo

```

Do not install every tool merely for appearance.

Every CI check must protect a real quality attribute.

---

# 61. GITHUB WORKFLOW

Create appropriate:

```text
.github/
├── workflows/
├── ISSUE_TEMPLATE/
├── PULL_REQUEST_TEMPLATE.md
└── CODEOWNERS

```

Do NOT invent squad GitHub accounts.

Use the real repository owner for CODEOWNERS when appropriate.

Model squads through issue labels such as:

```text
squad:architecture
squad:cloud-infra
squad:openshift
squad:ai-data
squad:payments

cloud:azure
cloud:aws
cloud:gcp
cloud:onprem

type:architecture
type:infra
type:feature
type:security
type:test
type:demo
type:bug

```

---

# 62. REPOSITORY STRUCTURE

Target architecture:

```text
maya-interlink-enterprise-ai-platform/
│
├── README.md
├── LICENSE
├── Makefile
├── ROADMAP.md
├── CHANGELOG.md
├── CONTRIBUTING.md
│
├── .github/
│
├── architecture/
│   ├── framework/
│   │   ├── togaf/
│   │   ├── metamodel/
│   │   ├── viewpoints/
│   │   └── principles/
│   │
│   ├── enterprise/
│   │   ├── archimate/
│   │   ├── capabilities/
│   │   ├── value-streams/
│   │   └── target-state/
│   │
│   ├── solution/
│   │   ├── c4/
│   │   ├── structurizr/
│   │   ├── sequences/
│   │   ├── hld/
│   │   └── lld/
│   │
│   ├── security/
│   ├── data/
│   ├── technology/
│   └── adr/
│
├── organization/
│   ├── tribe/
│   ├── squads/
│   ├── chapters/
│   └── RACI.md
│
├── program/
│
├── reuse/
│
├── infrastructure/
│   ├── terraform/
│   └── ansible/
│
├── gitops/
│   ├── bootstrap/
│   ├── base/
│   └── environments/
│       ├── local/
│       ├── aws/
│       ├── azure/
│       └── gcp/
│
├── platform/
│   ├── openshift/
│   ├── openshift-ai/
│   ├── policy-engine/
│   ├── iam/
│   ├── observability/
│   ├── finops/
│   └── greenops/
│
├── ai-platform/
│   ├── gateway/
│   ├── model-serving/
│   ├── registry/
│   ├── rag/
│   ├── agents/
│   ├── mcp/
│   ├── llmops/
│   ├── evaluation/
│   └── observability/
│
├── data-platform/
│   ├── kafka/
│   ├── postgres/
│   ├── vector-db/
│   ├── object-storage/
│   └── snowflake/
│
├── domains/
│   └── payments/
│       ├── common/
│       ├── iso20022/
│       ├── sct/
│       ├── sct-inst/
│       ├── sdd/
│       ├── wallet/
│       ├── simulators/
│       └── investigation-agent/
│
├── tests/
│   ├── unit/
│   ├── integration/
│   ├── smoke/
│   ├── e2e/
│   ├── resilience/
│   ├── security/
│   └── ai-evaluation/
│
├── demos/
│
├── evidence/
│
└── scripts/
    ├── bootstrap/
    ├── verify/
    ├── demo/
    ├── evidence/
    └── cloud/

```

Do not create empty directories solely to match this tree.

Create directories when their iteration actually uses them.

---

# 63. RELEASE ROADMAP

Use the following controlled roadmap.

## v0.1 — Executable Architecture Foundation

Deliver:

```text
repository baseline
README
architecture vision
TOGAF baseline
ArchiMate baseline
C4 baseline
organisation model
5 squads
chapters
RACI
program workflow
reuse catalog
source map
ADRs
Makefile
make doctor
local CRC detection
architecture generation
basic CI

```

This is the ONLY iteration to implement first.

Stop after v0.1.

---

## v0.2 — OpenShift GitOps & Security Foundation

Deliver:

```text
Argo CD bootstrap
GitOps structure
Keycloak baseline
Kyverno baseline
namespace strategy
RBAC
resource policies
NetworkPolicy baseline
secrets strategy
platform verification

```

---

## v0.3 — Event & Data Platform

Deliver:

```text
Kafka-compatible event backbone
PostgreSQL
vector database
object storage
schemas/contracts
correlation
outbox/DLQ/replay patterns
observability

```

---

## v0.4 — AI Runtime Foundation

Deliver:

```text
RHOAI compatibility assessment
ODH fallback where needed
KServe/model serving
small model
vLLM/Ollama option
AI project
basic model endpoint
verification

```

---

## v0.5 — Enterprise AI Gateway & LLMOps

Deliver:

```text
LiteLLM executable gateway
Envoy AI Gateway reference architecture
multi-model abstraction
quotas/budgets
Promptfoo
AI observability
model/provider ADR

```

---

## v0.6 — Enterprise RAG, Agents & MCP

Deliver:

```text
RAG
vector retrieval
Agent Controller
MCP
HITL
audit
agent evaluation

```

Reuse TradeOps generic assets where suitable.

---

## v0.7 — European Payment Platform

Deliver:

```text
Payment API
payment orchestrator
ISO 20022
Kafka events
SCT
SCT Inst
rail simulator
payment status
reconciliation baseline

```

Reuse Payment Hub assets where appropriate.

---

## v0.8 — AI Payment Investigation

Deliver:

```text
Payment Investigation Agent
RAG payment knowledge
MCP payment tools
Kafka event investigation
logs/metrics investigation
root cause
recommendation
evidence
HITL

```

This becomes the flagship interview demo.

---

## v0.9 — Enterprise Operations

Deliver:

```text
SRE
SLO
resilience
failure injection
security hardening
OpenCost
Kepler optional
AI FinOps
runbooks
postmortem

```

---

## v0.10 — Azure Architecture & Demo

Deliver:

```text
Azure landing zone model
network
identity
private connectivity
Terraform
OKD lab option
ARO enterprise target
Azure AI integration
Azure interview profile
plan/apply/destroy

```

---

## v0.11 — AWS Architecture & Demo

Deliver:

```text
AWS landing zone model
network
IAM
Terraform
OKD lab option
ROSA enterprise target
AWS AI integration
AWS interview profile
plan/apply/destroy

```

---

## v0.12 — GCP Architecture & Demo

Deliver:

```text
GCP foundation
network
IAM
Terraform
OKD/OCP lab
enterprise target
GCP AI integration
GCP interview profile
plan/apply/destroy

```

---

# v1.0 — Enterprise AI Platform for European Payments

Definition:

A complete:

```text
Enterprise Architecture
+
Hybrid Multi-Cloud Architecture
+
OpenShift Platform
+
AI Platform
+
Payments Platform
+
RAG
+
Agents
+
MCP
+
LLMOps
+
Security
+
Observability
+
SRE
+
FinOps
+
GreenOps
+
Interview Demonstration Suite

```

The same business/application architecture should be demonstrable on multiple deployment targets.

---

# 64. REFERENCE 12-WEEK PROGRAM

Maintain a planning model such as:

```text
Weeks 1-2
