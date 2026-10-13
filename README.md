🚨 PanicPatch

AI-Powered Production Incident Investigation & Reliability Engineering

Production broke. Let’s fix the why.

PanicPatch is an AI-assisted incident investigation platform designed to help Site Reliability Engineers (SREs) and DevOps engineers investigate production incidents using application logs, metrics, observability tools, Large Language Models (LLMs), and Retrieval-Augmented Generation (RAG).

Instead of simply alerting engineers that a service is failing, PanicPatch aims to help them understand what happened, identify evidence-backed root-cause hypotheses, retrieve relevant troubleshooting procedures, and determine what to investigate next.

🚧 Project Status: Under active development. Features will be marked as implemented as they are built and tested.

⸻

🎯 The Problem

Production incidents can require engineers to investigate multiple sources of information, including:

* Application logs and error traces
* Metrics and monitoring dashboards
* Service health checks and dependency failures
* Operational runbooks and troubleshooting documentation
* Historical incident reports

Manually correlating this information can increase investigation time and make troubleshooting more difficult.

PanicPatch explores how AI can assist this process by combining observability data with relevant operational knowledge to generate structured, evidence-based investigation reports.

💡 Our Solution

PanicPatch will provide a controlled environment for simulating production incidents and investigating them through a combination of traditional observability and AI-assisted diagnostics.

Planned Features

* 🚨 Incident Simulation: Reproduce HTTP 500 errors, elevated latency, and dependency failures.
* 📊 Observability: Collect application metrics and visualize service behavior.
* 📝 Structured Logging: Capture timestamped events and diagnostic information.
* 🤖 LLM-Powered Investigation: Analyze incident context and generate structured reports.
* 🔎 RAG-Based Runbook Retrieval: Retrieve relevant troubleshooting documentation using semantic search.
* 🧠 Evidence-Based Diagnosis: Separate observed facts from hypotheses and identify missing evidence.
* 🛠️ Diagnostic Recommendations: Suggest investigation steps for engineer review.
* 🧪 AI Evaluation: Test diagnostic quality against known incident scenarios.
* ⚙️ CI/CD Automation: Run automated tests through GitHub Actions.
* 🔐 Human-in-the-Loop Safety: Keep remediation decisions under engineer control.

⸻

🏗️ Architecture

The following diagram represents the planned architecture.

                   INCIDENT SIMULATION
                           |
                           v
                   FASTAPI APPLICATION
                           |
              +------------+------------+
              |            |            |
              v            v            v
           Metrics       Logs      Health Checks
              |            |            |
              v            +------------+
          PROMETHEUS
              |
              v
           GRAFANA
              |
              v
       INCIDENT INVESTIGATION
              |
              v
        INCIDENT CONTEXT
       Logs + Metrics + Errors
              |
              v
         RAG RETRIEVAL <--------- RUNBOOK DOCUMENTATION
              |                         |
              |                    Embeddings
              |                         |
              |                    Vector Store
              v
          LLM ANALYSIS
              |
              v
      STRUCTURED INCIDENT REPORT
              |
              v
       ENGINEER REVIEWS ACTIONS

The system will be implemented incrementally. The diagram describes the intended design, not a claim that all components are already operational.

⸻

🛠️ Technology Stack

Category	Technologies
Programming Language	Python
API Framework	FastAPI
Testing	Pytest
Containerization	Docker, Docker Compose
CI/CD	GitHub Actions
Monitoring	Prometheus
Visualization	Grafana
AI Integration	LLM API
AI Architecture	Retrieval-Augmented Generation (RAG)
Embeddings	Embedding models
Vector Search	Chroma or FAISS
Version Control	Git, GitHub
Infrastructure as Code	Terraform
Cloud Platform	AWS
Potential Extension	Kubernetes

Technologies will be introduced according to project priorities and validated through working implementations.

⸻

🧠 How AI Investigation Will Work

PanicPatch will combine incident evidence with relevant operational knowledge to support troubleshooting.

Example: Database Connection Failures

Suppose the simulated application starts returning HTTP 500 errors.

The collected logs contain:

10:15:01 INFO  Request received: /api/payments
10:15:02 INFO  Connecting to payment database
10:15:07 ERROR Database connection timeout
10:15:07 ERROR Payment request failed: HTTP 500

The investigation workflow will:

1. Collect relevant application logs and available metrics.
2. Identify the incident symptoms.
3. Retrieve relevant database troubleshooting runbooks through RAG.
4. Supply the incident evidence and retrieved documentation to an LLM.
5. Generate a structured investigation report.
6. Recommend diagnostic steps and reference relevant documentation.
7. Evaluate the report against the known simulated failure.

A report could identify database connectivity as a possible cause while recommending checks for database availability, connection limits, and connection-pool utilization.

The AI must not present an unverified hypothesis as a confirmed root cause. Conclusions should be supported by evidence, and uncertainty should be communicated explicitly.

⸻

🔎 Understanding RAG in PanicPatch

Retrieval-Augmented Generation allows the investigation engine to consult relevant documentation before generating an answer.

Our planned RAG workflow is:

1. Create operational runbooks covering common incident scenarios.
2. Split the documents into searchable chunks.
3. Generate embeddings for the document chunks.
4. Store the embeddings in a vector store.
5. Retrieve relevant passages when an incident occurs.
6. Provide the retrieved passages and incident evidence to the LLM.
7. Generate a response grounded in the retrieved information.
8. Evaluate retrieval relevance and answer quality.

Potential runbook topics include:

* HTTP 500 errors
* Database connection timeouts
* High API latency
* Container failures
* Service health-check failures
* Elevated error rates

The initial implementation will use synthetic logs and self-created documentation in a controlled development environment.

⸻

📈 Reliability and AI Evaluation

PanicPatch will aim to evaluate both system reliability and AI investigation quality.

Evaluation Area	Planned Measurement
Incident Detection	Whether expected failures are detected
Application Reliability	Error rates and response latency
Monitoring	Availability of relevant metrics and alerts
RAG Retrieval	Relevance of retrieved runbook passages
Diagnostic Quality	Agreement with known incident causes
Evidence Grounding	Whether conclusions are supported by available evidence
Recommendation Quality	Relevance and safety of suggested next steps
Failure Handling	Behavior when the LLM or a dependency is unavailable

Evaluation results will be recorded as the project develops. No performance improvements or accuracy claims will be made without measurements.

⸻

🔐 Security and Safety

PanicPatch is intended as an AI-assisted investigation tool, not an autonomous production remediation system.

The design will prioritize:

* Read-only incident analysis
* Human review of recommendations
* Controlled failure simulation
* Secure API-key management through environment variables
* Protection against exposing secrets in logs or prompts
* Input validation and API error handling
* Clear separation between evidence and AI-generated hypotheses
* Testing for unsupported conclusions and unsafe recommendations

Automated remediation is outside the initial scope.

⸻

🗺️ Development Roadmap

Phase 1 — Application Foundation

* Set up the Python project and Git workflow
* Implement the FastAPI application
* Add health-check endpoints
* Implement structured logging
* Create controlled incident scenarios
* Add automated tests

Phase 2 — Containers and CI/CD

* Build a Docker image
* Configure Docker Compose
* Add GitHub Actions workflows
* Automate test execution
* Improve configuration and secret management

Phase 3 — Observability

* Expose Prometheus metrics
* Configure Prometheus scraping
* Build Grafana dashboards
* Create alert rules
* Validate monitoring against simulated failures

Phase 4 — LLM Integration

* Integrate an LLM API
* Design incident investigation prompts
* Implement structured incident reports
* Add error handling and cost controls
* Distinguish facts from hypotheses

Phase 5 — RAG Implementation

* Create operational runbooks
* Generate embeddings
* Implement vector search
* Retrieve relevant documentation
* Ground LLM responses in retrieved context
* Evaluate retrieval quality

Phase 6 — End-to-End SRE + AI

* Integrate monitoring data and incident logs
* Implement reusable investigation workflows
* Evaluate diagnoses against known incidents
* Add AI guardrails
* Test component failures and degraded operation

Phase 7 — Cloud and Infrastructure

* Explore Terraform-based infrastructure
* Deploy to AWS if the core system is stable
* Document deployment and security decisions
* Evaluate Kubernetes as an extension

Phase 8 — Portfolio and Documentation

* Document the final architecture
* Add verified screenshots and demonstrations
* Publish setup and usage instructions
* Document evaluation results and limitations
* Prepare technical interview explanations

⸻

🚀 Getting Started

Setup instructions will be added once the initial application is implemented and tested.

Planned Prerequisites

* Python 3.11 or a compatible supported version
* Git
* Docker Desktop
* An LLM API key for the AI integration phase

An LLM API key will not be required for the initial application and monitoring milestones.

⸻

🎓 Project Objectives

PanicPatch is a hands-on engineering project exploring the intersection of:

* Site Reliability Engineering
* DevOps and CI/CD
* Observability and incident management
* Large Language Models
* Retrieval-Augmented Generation
* AI evaluation and operational safety

The objective is to build a working platform that demonstrates how AI can assist engineers in investigating production-style incidents while preserving evidence-based reasoning and human oversight.

⸻

👩‍💻 Author

A personal engineering project focused on SRE, DevOps, observability, and AI-assisted operations.

⸻

⭐ Follow the project as it evolves from a basic incident simulator into an AI-assisted reliability engineering platform.
