Architecture / organisation / runnable foundation

Weeks 3-4
OpenShift / GitOps / security

Weeks 5-6
AI runtime / model serving / AI Gateway

Weeks 7-8
RAG / Agents / MCP / event platform

Weeks 9-10
Payments / ISO 20022 / Payment Investigation

Week 11
SRE / security / FinOps / resilience

Week 12
E2E / evidence / interview demonstrations

```

Cloud-specific demonstrations may continue as dedicated increments.

---

# 65. DEFINITION OF DONE FOR EVERY RELEASE

A release is NOT complete unless:

```text
Architecture updated
ADRs updated
Code/config committed
No secrets committed
CI passes
Deployment procedure exists
Verification procedure exists
Rollback/destroy procedure exists where relevant
Known limitations documented
Evidence produced where possible
README updated
CHANGELOG updated
Version/tag prepared
Demo instructions updated

```

For executable releases additionally require:

```text
make doctor
make install/deploy
make verify

```

or equivalent to succeed in the supported test environment.

---

# 66. RELEASE REPORT FORMAT

At the end of each iteration report:

```text
RELEASE:
vX.Y.Z

STATUS:
PASS / PARTIAL / BLOCKED

DELIVERED:
...

REUSED:
...

ARCHITECTURE DECISIONS:
...

TESTS:
...

KNOWN LIMITATIONS:
...

HOW TO RETRIEVE:
git clone ...
git checkout vX.Y.Z

HOW TO DEPLOY:
...

HOW TO VERIFY:
...

HOW TO DESTROY/ROLLBACK:
...

NEXT ITERATION:
...

```

Then STOP and wait for explicit owner instruction before implementing the next release.

---

# 67. QUALITY PRINCIPLES

Apply:

```text
API-first
event-driven
cloud-native
GitOps
IaC
Policy-as-Code
Security-by-Design
Observability-by-Design
SRE
FinOps
GreenOps
Zero Trust
least privilege
portable application architecture
human-in-the-loop AI
synthetic demonstration data
architecture-as-code

```

---

# 68. ARCHITECTURAL BOUNDARIES

Keep responsibilities clear.

Example Azure:

```text
Azure Solution Architect
owns:
VNet
subnets
DNS
firewall
private connectivity
Entra
landing zone
ARO infrastructure

OpenShift Architect
owns:
cluster platform
projects
operators
RBAC
GitOps
OpenShift AI
platform policies

```

Do the same for AWS and GCP.

---

# 69. CONTROL PLANE VS RUNTIME PLANE

Explicitly model:

## AI Control Plane

```text
identity
governance
catalog
policy
AI Gateway
evaluation
cost control
registry
observability

```

## AI Runtime Plane

```text
model serving
RAG
agents
MCP
payment workloads
data connectors

```

Document centralised vs distributed decisions.

---

# 70. PORTABILITY

Payment applications should not know whether they run on:

```text
CRC
OKD
OCP
ARO
ROSA
GCP OCP

```

Use Kubernetes/OpenShift abstractions and overlays.

Likewise, applications should not directly depend on:

```text
OpenAI
Azure
AWS
Google
Claude
Mistral

```

Use AI Gateway/model aliases.

---

# 71. SECURITY SAFETY RULE

This is a demonstration platform.

Never create mechanisms for real financial execution.

Payment rails, customers, fraud decisions and transaction data are synthetic.

AI should not autonomously:

```text
move real money
block real accounts
approve financial transactions
execute production remediation

```

High-impact decisions require deterministic controls and human approval.

---

# 72. NO FAKE IMPLEMENTATIONS

Do not create placeholder files claiming a capability exists.

If a component is architectural only, explicitly mark it:

```text
REFERENCE ONLY
NOT DEPLOYED

```

If a cloud path has only Terraform plan support, say:

```text
PLAN-VALIDATED
NOT LIVE-DEPLOYED

```

Do not claim tests passed if they were not executed.

Do not claim RHOAI works on a given OCP version unless verified.

Do not claim a cloud environment was deployed without actual deployment evidence.

---

# 73. NO UNNECESSARY COMPLEXITY

Do not build:

```text
custom service mesh
custom IAM
custom Kafka
custom vector database
custom AI Gateway
custom model server

```

unless there is a compelling architecture reason.

Integrate mature products.

Our value is:

```text
architecture
integration
automation
governance
payments expertise
operability
demonstrability

```

not rewriting infrastructure products.

---

# 74. FIRST EXECUTION — DO THIS NOW

For the first run of this master prompt:

## Step 1

Inspect:

```text
zdmooc/maya-interlink-enterprise-ai-platform

```

and confirm its current state.

## Step 2

Audit the relevant existing `zdmooc` repositories listed above.

Do not deeply analyse irrelevant repositories.

Create a capability/reuse matrix.

## Step 3

Confirm the most relevant upstream reference repositories are still maintained/current.

## Step 4

Implement ONLY:

# v0.1.0 — Executable Architecture Foundation

Create a coherent initial repository containing at least:

```text
README.md
LICENSE
Makefile
ROADMAP.md
CHANGELOG.md

architecture/
organization/
program/
reuse/
scripts/
.github/

```

with meaningful files only.

## Step 5

Implement:

```bash
make help
make doctor
make architecture
make verify

```

`make doctor` must safely inspect the local environment without making destructive changes.

## Step 6

Document the local CRC/OpenShift environment requirements and compatibility checks.

## Step 7

Generate initial:

```text
TOGAF Architecture Vision
architecture principles
capability map
initial ArchiMate model/view
initial C4 model
target hybrid multi-cloud diagram
organisation/Tribe/Squads
RACI
program workflow
dependency strategy
reuse catalog
initial ADR set

```

## Step 8

Add initial CI validation.

## Step 9

Validate everything that can be validated without credentials.

## Step 10

Prepare/tag:

```text
v0.1.0

```

when technically possible.

## Step 11

Return the release report containing exact commands for the repository owner to run locally.

Then STOP.

Do NOT implement v0.2 until explicitly instructed.

---

# FINAL SUCCESS CRITERION

At v1.0, before an interview, the repository owner should be able to choose:

```bash
make interview PROFILE=enterprise
make interview PROFILE=azure
make interview PROFILE=aws
make interview PROFILE=gcp
make interview PROFILE=openshift
make interview PROFILE=ai-platform
make interview PROFILE=payments

```

and use the SAME coherent enterprise platform to demonstrate the architecture from the perspective of the requested role.

The strongest complete scenario must remain:

```text
European Payment
      ↓
ISO 20022
      ↓
Event Platform
      ↓
Failure
      ↓
Payment Investigation Agent
      ↓
RAG + MCP + Logs + Metrics + Events
      ↓
Evidence-based diagnosis
      ↓
Human-approved recommendation

```

running on an architecture that demonstrates:

```text
TOGAF
ArchiMate
C4
Hybrid Multi-Cloud
Terraform
OpenShift / OKD
OpenShift AI / Open Data Hub
GitOps
Kyverno
IAM
Kafka
AI Gateway
KServe/vLLM
RAG
Agents
MCP
LLMOps
Security
Observability
SRE
FinOps
GreenOps
European Payments

```

This repository must demonstrate that its owner can **design the enterprise architecture, understand the cloud foundations, build the platform, deploy it, validate it, operate it, troubleshoot it, govern it, and explain it clearly in a senior architecture interview.**