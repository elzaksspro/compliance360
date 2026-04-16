# Compliance360
### Every Obligation. Every Entity. One Intelligence Layer.

> **Microsoft AI Skills Week 2026 — RegTech Hackathon**
> Organised by Microsoft · NITDA · Data Science Nigeria

---

## 🇳🇬 What is Compliance360?

Compliance360 is a universal compliance intelligence platform for Nigeria's regulatory environment. It continuously pipelines regulatory obligations from 23+ Nigerian regulatory bodies, maps them to registered entity profiles via an ontology-driven knowledge graph, and delivers personalised compliance intelligence through a real-time dashboard, notification engine, and an LLM-powered research assistant.

**The problem:** Nigeria's regulatory landscape spans CBN, FIRS, CAC, NDPC, NITDA, NFIU, SCUML, SEC, NAICOM, PenCom, NSITF, ITF, FCCPC, NAFDAC, and 9+ other agencies — issuing obligations simultaneously across tax, data protection, corporate governance, AML/CFT, labour, and sector-specific compliance. No unified platform exists to track, map, and intelligently surface these obligations for all entity types.

**The solution:** Compliance360 solves this with five interconnected layers — a live web pipeline, an ontology-driven knowledge graph, a network analysis engine, an LLM research assistant, and a real-time notification system.

---

## 🎯 Live Demo

**[→ View live prototype](https://elzaksspro.github.io/compliance360)**

### Demo accounts

| Entity type | Email | Password |
|---|---|---|
| 🏢 Corporate | `corporate@demo.compliance360.ng` | `demo1234` |
| 👤 Individual | `individual@demo.compliance360.ng` | `demo1234` |
| 🏗️ Government | `government@demo.compliance360.ng` | `demo1234` |
| ⚖️ NGO / Trust | `ngo@demo.compliance360.ng` | `demo1234` |
| 🔍 Compliance Officer | `officer@demo.compliance360.ng` | `demo1234` |

---

## ✨ Core Features

### ⬡ Obligation Knowledge Graph
The centrepiece of Compliance360. A D3.js force-directed graph showing every regulation, obligation, deadline, institution, and risk factor for a registered entity — connected by semantic relations (governs, triggers, applies-to, supersedes, conflicts-with). Drag nodes, zoom, filter by domain (Tax / Data / Labour / Finance / AML / Digital), and click any node to inspect its properties.

### 🌐 Nigeria Compliance Landscape
A full-screen knowledge graph of Nigeria's entire regulatory ecosystem — 127 nodes across 23 agencies and 8+ industry sectors. Designed for compliance officers to research the regulatory landscape across all agencies simultaneously. Three sidebar tabs:
- **Filters** — domain, entity type, industry, relation type, compliance status
- **Analytics** — PageRank centrality rankings, compliance clusters, conflict and gap detection
- **Research** — LLM-powered chat interface grounded in the knowledge graph

### 🔔 Notification Engine
Real-time alerts delivered via in-app dashboard, email (SendGrid), and WhatsApp Business API. Triggered by:
- Deadline reminders (30 days / 7 days / 1 day advance)
- New obligation detected by pipeline
- Supersession events (regulation overridden or amended)
- Conflict alerts (contradictory regulatory requirements)

### ⟳ Supersession Tracker
Detects when new regulations override, amend, or extend previous ones — with clause-level diff showing exactly what changed. Full regulatory lineage timeline per domain (AML chain, Tax chain, Agent Banking chain). Supports full, partial, and implicit supersession detection.

### 🔄 Data Pipeline
Automated + manual compliance ingestion with full ontology mapping:
- **Automated** — Scrapy spiders on Airflow DAGs scraping 23 regulatory sources on configurable schedules
- **Manual** — Drag-and-drop PDF/DOCX upload or URL ingestion → NLP extraction pipeline → ontology mapping preview → approve/reject workflow
- **Review queue** — Low-confidence extractions flagged for human review with proposed mappings
- **Ontology tab** — OWL class hierarchy viewer, mapping rules engine, entity × cluster matrix

### 💬 LLM Research Assistant
Context-aware compliance Q&A powered by LangChain GraphCypherQAChain + Azure OpenAI GPT-4o. Every answer is grounded in the knowledge graph and cites source regulations. Entity context (type, sector, size, state) is injected into every query — so a microfinance bank gets different answers than a listed company.

### ✅ Compliance Checklist & Roadmap Generator
Interactive obligation checklist with phase grouping (Immediate / Short-term / Full compliance). Tracks completion progress with compliance score. Generates downloadable CBN-formatted Implementation Roadmap documents via FastAPI + python-docx.

---

## 🏗️ Entity Types Supported

| Entity | Sub-categories | Key Regulators | Obligations |
|---|---|---|---|
| 👤 Individual | Employee, Self-employed, Professional, Investor | FIRS, LIRS, PenCom, NHF, Professional bodies | 18+ |
| 🏢 Corporate | SME, Startup, Mid-size, Large, Listed, Fintech | FIRS, CAC, NDPC, NITDA, CBN, NSITF, ITF | 47+ |
| 🏛️ Trustee | Estate, Pension fund, Charitable, Unit trust | FIRS, CAC, PenCom, SEC, Probate Court | 23+ |
| 🏗️ Government | MDA, Parastatal, State Agency, LGA | GIFMIS, IPPIS, TSA, BPP, OAuGF | 34+ |
| ⚖️ NGO / Trust | Foundation, CBO, INGO, Faith-based | CAC Part F, SCUML, FIRS, NFIU | 21+ |

---

## 🧠 Technical Architecture

```
Regulatory Documents (CBN, FIRS, CAC, NDPC, NITDA, SEC, NFIU + 17 more)
        │
        ▼  [Layer 1 — Web Pipeline]
  Apache Airflow + Scrapy + PyMuPDF + Apache Tika
        │
        ▼  [Layer 2 — NLP Extraction]
  spaCy NER + LangChain + Azure OpenAI GPT-4o
  Entity extraction: Regulation, Obligation, Deadline, Penalty, Threshold
  Relation extraction: governs, supersedes, triggers, conflicts-with, applies-to
        │
        ▼  [Layer 3 — Ontology + Knowledge Graph]
  OWL/RDF (RDFLib) ── Neo4j / Azure Cosmos DB Gremlin API
  SPARQL + Cypher queries
        │
        ▼  [Layer 4 — Network Analysis]
  NetworkX: PageRank · Betweenness centrality · Louvain clustering
  BFS cascade traversal · Contradiction scoring · Gap detection
        │
        ▼  [Layer 5 — LLM Reasoning]
  LangChain GraphCypherQAChain · RAG (Azure Cognitive Search)
  Entity-context-aware prompts · Source citation injection
        │
        ▼  [Layer 6 — Platform + Notifications]
  FastAPI · React 18 · D3.js · WhatsApp Business API · SendGrid
```

---

## 🛠️ Technology Stack

| Category | Technology |
|---|---|
| LLM | Azure OpenAI GPT-4o |
| LLM Framework | LangChain ≥0.2 (GraphCypherQAChain, RAG) |
| Knowledge Graph | Neo4j 5.x / Azure Cosmos DB Gremlin |
| Ontology | OWL/RDF · RDFLib 7.x |
| Network Analysis | NetworkX 3.x · python-louvain |
| NLP | spaCy 3.7 (custom NER) |
| Web Pipeline | Apache Airflow · Scrapy · PyMuPDF |
| Search / RAG | Azure Cognitive Search |
| Backend API | FastAPI (Python 3.11+) |
| Frontend | React 18 · D3.js 7.x · Vis.js 9.x |
| Notifications | WhatsApp Business API · SendGrid |
| Cloud | Microsoft Azure (OpenAI, Cosmos DB, Container Apps, Blob Storage) |
| Auth | Azure Active Directory B2C |

---

## 📡 Web Pipeline — Regulatory Sources

| Regulator | Scope | Frequency |
|---|---|---|
| CBN — Central Bank of Nigeria | All financial institutions, AML | Every 6 hours |
| FIRS — Federal Inland Revenue Service | All entity types, tax | Every 6 hours |
| CAC — Corporate Affairs Commission | Corporate, NGO, Trustee | Daily |
| NDPC — National Data Protection Commission | All data processors | Daily |
| NITDA — IT Development Agency | Tech sector, IT contracts | Daily |
| NFIU — Financial Intelligence Unit | AML/CFT, STR filing | Daily |
| SCUML — Anti-Money Laundering | DNFBPs, NGOs | Daily |
| SEC — Securities Exchange Commission | Capital markets, Trustee | Daily |
| FCCPC — Consumer Protection | Digital services, lenders | Daily |
| PenCom, NSITF, ITF, NHF | Labour obligations | Daily |
| NAFDAC, SON, NESREA | Sector-specific | Daily |
| Federal Gazette | All entity types | Daily |
| State IRS (FCT, Lagos, Kano) | State tax obligations | Daily |

---

## 📋 API Endpoints (Full Platform)

| Endpoint | Method | Description |
|---|---|---|
| `POST /entities/register` | POST | Register entity → returns obligation set |
| `GET /entities/{id}/obligations` | GET | List obligations filtered by status/regulator |
| `GET /entities/{id}/score` | GET | Compliance score with domain breakdown |
| `POST /research/query` | POST | NL query → graph-grounded answer + citations |
| `POST /roadmap/generate` | POST | Generate CBN-formatted roadmap document |
| `GET /supersessions` | GET | All supersession events |
| `GET /supersessions/{id}/diff` | GET | Clause-level diff for a supersession |
| `GET /conflicts` | GET | Detected regulatory conflicts |
| `GET /gaps` | GET | Structural compliance gaps |
| `GET /pipeline/status` | GET | Pipeline health + document counts |
| `GET /landscape/export` | GET | Full compliance landscape report |

---

## 📁 Repository Structure

```
compliance360/
│
├── index.html              ← Full prototype (single-file demo)
├── README.md               ← This file
│
├── docs/
│   ├── Compliance360_SRS_v2.0.docx    ← Software Requirements Specification
│   └── Compliance360_TDD_v2.0.docx    ← Technical Design Document
│
└── (full platform — coming post-hackathon)
    ├── backend/            ← FastAPI + LangChain + Neo4j
    ├── pipeline/           ← Airflow DAGs + Scrapy spiders
    ├── ontology/           ← OWL/Turtle schema
    ├── nlp/                ← spaCy NER pipeline
    └── frontend/           ← React 18 + D3.js
```

---

## 👥 Team

Built for the **Microsoft AI Skills Week 2026 — RegTech Hackathon**
Abuja, Nigeria · April 2026

**Skills:** Ontology engineering · Knowledge representation · Network analysis · LangChain · Azure OpenAI · CBN macroprudential analytics · M&E frameworks · MLOps

---

## ⚖️ Disclaimer

Compliance360 provides regulatory intelligence support, not legal advice. All obligation information should be verified against primary regulatory sources before reliance. Citations are provided for every AI-generated response.

---

*Compliance360 · Microsoft AI Skills Week 2026 · Nigeria*
