# GitOps & Kubernetes Portfolio

This repository demonstrates production-grade GitOps workflows using ArgoCD + Jenkins + Kubernetes.  

flowchart TB
    Dev[Developers]

    Git[Git Repositories<br/>(App + Config)]
    CI[CI Pipelines<br/>(Jenkins / Build + Test)]
    CD[GitOps CD<br/>(ArgoCD / Flux)]
    K8s[Kubernetes Cluster<br/>(Dev / QA / Prod)]
    Monitor[Observability & Metrics<br/>(Prometheus + Grafana)]
    Sec[Security & Policy Checks<br/>(Trivy + OPA + Vault)]
    AI[AI Assistance<br/>(LLM + RAG)]
    
    %% Developer Workflow
    Dev --> Git
    Git --> CI
    CI --> Git
    Git --> CD

    %% Deployment Workflow
    CD --> K8s
    K8s --> Monitor
    K8s --> Sec

    %% AI Integration
    CI --> AI
    Monitor --> AI
    Sec --> AI
    AI --> Dev

    %% Rollback / Feedback
    Monitor --> CD
    Sec --> CD

    flowchart TB
    App[Application / Services]

    Metrics[Metrics & Logs Collection<br/>(Prometheus + Loki)]
    Traces[Distributed Tracing<br/>(Jaeger / OpenTelemetry)]
    SLO[SLIs & SLOs]
    Alert[Alerts & Notifications<br/>(Grafana Alerting / Opsgenie)]
    Incident[Incident Management<br/>(PagerDuty / Jira)]
    AI[AI Assistance<br/>(LLM + RAG)]
    Postmortem[Postmortem & Knowledge Base]

    %% Application to observability
    App --> Metrics
    App --> Traces

    %% Metrics & Traces to SLO evaluation
    Metrics --> SLO
    Traces --> SLO

    %% Alerts
    SLO --> Alert
    Alert --> Incident

    %% AI Assistance
    Metrics --> AI
    Traces --> AI
    Incident --> AI
    AI --> Alert
    AI --> Dev[Developers & SREs]

    %% Postmortem loop
    Incident --> Postmortem
    Postmortem --> Dev
    Postmortem --> SLO

### 🔹 SLO vs SLA vs SLI

| Term | Definition | Example |
|------|------------|---------|
| **SLI** (Service Level Indicator) | Metric used to measure reliability | % of successful HTTP requests, latency < 200ms |
| **SLO** (Service Level Objective) | Target for that metric | 99.9% of requests must succeed in a month |
| **SLA** (Service Level Agreement) | Contractual commitment to customers | If availability < 99.9%, compensation is given |

✅ Think of it like:

SLI = measurement
SLO = internal goal
SLA = external promise


