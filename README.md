# Jim — Autonomous AI BDR Agent

Jim is a **production-grade autonomous AI BDR** designed to research leads, generate personalized outreach, and execute multi-step outbound workflows with measurable business impact.

This repository focuses on **engineering, evaluation, and deployment**, not marketing polish. Jim is built to demonstrate how modern agent systems behave under real-world constraints: latency, reliability, cost, safety, and observability.

---

## Why This Project Matters

Most AI agent demos stop at prompt chaining. Jim goes further.

This project demonstrates how to:
- Build **stateful, multi-step agents** that plan, act, verify, and recover
- Maintain **persona consistency and hallucination control** across long-running workflows
- Balance **LLM quality vs. latency and cost** in production
- Instrument agents with **evaluation, metrics, and observability**
- Deploy AI systems that interact with **real external systems** (CRMs, email providers, APIs)

These are the same challenges faced by teams building:
- AI employees (BDRs, analysts, operators)
- Agentic product features
- LLM platforms and evaluation tooling
- Production GenAI systems with business accountability

---

## Core Capabilities

### Lead Research & Context Assembly
- Retrieval-augmented generation using web data, CRM records, and internal documents
- Structured enrichment to avoid prompt bloat and context collapse
- Permissions-aware data access

### Personalized Outreach
- Persona-driven prompt templates with strict output constraints
- Email, LinkedIn, and call-script generation
- Deterministic formatting and length guarantees

### Agent Orchestration
- Planner → Executor → Verifier architecture (LangGraph)
- Tool calling for CRM sync, scheduling, and enrichment
- Retry, fallback, and self-correction logic

### Evaluation & Quality Control
- Automatic checks for:
  - Hallucinations
  - Persona drift
  - CTA presence
  - Length and formatting violations
- Human-labeled relevance scoring
- Spam and readability analysis

### Production Deployment
- FastAPI service with async execution
- Dockerized and Kubernetes-ready
- Rate limiting, backoff, and PII-safe handling

---

## High-Level Architecture

```
Web UI
  ↓
FastAPI Backend
  ↓
Agent Orchestrator (Planner / Executor / Verifier)
  ↓
RAG Retriever → Vector Store
  ↓
LLM Runtime (Claude / GPT)
  ↓
Outbound Executors (Email / CRM / Calendar)
```

---

## Example Agent Flow

1. Ingest lead list
2. Retrieve company and role-specific context
3. Plan outreach strategy
4. Generate personalized message
5. Verify constraints and quality
6. Execute send and log to CRM
7. Schedule follow-ups and monitor replies

Each step is observable, testable, and auditable.

---

## Quickstart

```bash
git clone https://github.com/yourusername/jim-ai-bdr.git
cd jim-ai-bdr
pip install -r requirements.txt
```

Create environment variables:
```bash
cp .env.example .env
```

Run locally:
```bash
uvicorn app.main:app --reload --port 8000
```

---

## Evaluation Examples

```python
def test_email_constraints(output):
    assert len(output.split()) <= 100
    assert "meeting" in output.lower()
    assert "{{" not in output
```

Metrics tracked:
- Reply rate
- Persona consistency score
- Hallucination rate
- Latency per step
- Cost per outreach

---

## Deployment

- Docker + Kubernetes supported
- Async task execution via queues
- Horizontal scaling for multi-user workloads
- Safe rate limits for outbound communication

---

## What This Project Signals to Reviewers

This repository demonstrates:
- Hands-on experience with **agent systems in production**
- Strong understanding of **LLM failure modes**
- Ability to design **evaluation and observability** for AI behavior
- Comfort operating across **model, infra, and product layers**
- Bias toward **shipping real systems**, not prototypes

---

## Roadmap

- Multi-language outreach
- Voice-based agent workflows
- Reinforcement learning from reply outcomes
- Unified evaluation dashboard

---

## License

MIT
