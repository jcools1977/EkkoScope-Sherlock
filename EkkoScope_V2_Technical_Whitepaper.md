# EkkoScope V2 Technical Whitepaper
## Generative Engine Optimization (GEO) Platform for AI Visibility Intelligence

**Version 2.0 | January 2026**

---

## Document Control

| Attribute | Value |
|-----------|-------|
| Version | 2.0 |
| Last Updated | January 12, 2026 |
| Classification | Technical Reference |
| Audience | Engineers, Investors, Enterprise Clients |

### Version History

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | December 2025 | Initial whitepaper with core visibility engine |
| 2.0 | January 2026 | Added Lead Capture, Sherlock, Eidetic, Sales Mode, Swarm Commander, Squeeze Pages |

---

## Executive Summary

EkkoScope V2 is an enterprise-grade SaaS platform that measures, monitors, and optimizes business visibility within AI assistant recommendations. As Large Language Models (ChatGPT, Perplexity, Gemini) increasingly influence consumer decisions, EkkoScope provides the intelligence layer for businesses to understand and improve their AI presence.

The platform combines real-time multi-LLM analysis, semantic gap detection, autonomous remediation agents, and persistent memory architecture to deliver actionable insights through a premium "Boardroom" interface designed for agency and enterprise clients.

**Key Differentiators:**
- Multi-LLM visibility analysis across ChatGPT, Perplexity, and Gemini
- Dual-layer memory architecture (local SQLite + Eidetic cloud storage)
- Sherlock semantic intelligence engine with vector-based gap analysis
- Autonomous FixEngine with 4 specialized AI agents
- Lead capture funnels with teaser audits for prospect conversion
- Sales Mode for automated cold outreach campaigns

---

## Table of Contents

1. [Problem Statement](#1-problem-statement)
2. [Platform Architecture](#2-platform-architecture)
3. [AI Visibility Engine](#3-ai-visibility-engine)
4. [Lead Capture & Teaser Audit System](#4-lead-capture--teaser-audit-system)
5. [User Management & Authentication](#5-user-management--authentication)
6. [EkkoBrain Memory System](#6-ekkobrain-memory-system)
7. [Eidetic Integration (MandelDB 2.0)](#7-eidetic-integration-mandeldb-20)
8. [Sherlock Semantic Intelligence Engine](#8-sherlock-semantic-intelligence-engine)
9. [FixEngine Core (Autonomous Remediation)](#9-fixengine-core-autonomous-remediation)
10. [PDF Report Generation](#10-pdf-report-generation)
11. [Sales Mode (Headless Prospecting)](#11-sales-mode-headless-prospecting)
12. [Swarm Commander (Domain Provisioning)](#12-swarm-commander-domain-provisioning)
13. [Payment Processing & Billing](#13-payment-processing--billing)
14. [Admin Portal](#14-admin-portal)
15. [API Reference](#15-api-reference)
16. [Security & Compliance](#16-security--compliance)
17. [Deployment & Infrastructure](#17-deployment--infrastructure)
18. [Roadmap](#18-roadmap)

---

## 1. Problem Statement

### 1.1 The AI Visibility Gap

Large Language Models (LLMs) increasingly influence consumer decisions through conversational AI assistants. When users ask questions like:

- "What's the best roofing company in Charleston?"
- "Where can I buy bulk packaging supplies?"
- "Who should I call for emergency HVAC repair?"

AI systems generate recommendations based on their training data, real-time web access, and contextual understanding. Unlike traditional search engines that return ranked links, LLMs synthesize responses that directly recommend specific businesses.

### 1.2 Market Impact

| Statistic | Implication |
|-----------|-------------|
| 60%+ of consumers use AI assistants for purchase research | Massive decision influence |
| 0% average AI visibility for SMBs | Critical competitive gap |
| No existing measurement tools | Blue ocean opportunity |

### 1.3 EkkoScope Solution

EkkoScope addresses this gap by:

1. **Programmatically querying** multiple AI providers
2. **Measuring brand presence** in synthesized responses
3. **Identifying competitors** capturing AI recommendations
4. **Providing actionable remediation** through AI agents
5. **Tracking visibility trends** over time

---

## 2. Platform Architecture

### 2.1 Technology Stack

| Layer | Technology | Purpose |
|-------|------------|---------|
| **Web Framework** | FastAPI + Uvicorn | Async API server |
| **Python Version** | 3.11+ | Runtime environment |
| **Templating** | Jinja2 | Server-side HTML rendering |
| **Styling** | Tailwind CSS | Utility-first CSS framework |
| **Database** | SQLite (SQLAlchemy ORM) | Local persistence |
| **Vector Database** | Pinecone | Semantic search & embeddings |
| **External Memory** | Eidetic AI (MandelDB) | Cloud-based knowledge graph |
| **PDF Generation** | FPDF2 | Report creation |
| **Payments** | Stripe | Subscription & checkout |
| **AI Providers** | OpenAI, Perplexity, Gemini | Multi-LLM analysis |

### 2.2 System Architecture Diagram

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                              EkkoScope V2 Platform                          │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  ┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐        │
│  │   Public Site   │    │   User Portal   │    │  Admin Portal   │        │
│  │  Landing/Audit  │    │   Dashboard     │    │  Client Mgmt    │        │
│  │   Squeeze Pages │    │   Reports       │    │  Onboarding     │        │
│  └────────┬────────┘    └────────┬────────┘    └────────┬────────┘        │
│           │                      │                      │                  │
│           └──────────────────────┼──────────────────────┘                  │
│                                  │                                          │
│                          ┌───────▼───────┐                                  │
│                          │  FastAPI Core │                                  │
│                          │   (main.py)   │                                  │
│                          └───────┬───────┘                                  │
│                                  │                                          │
│      ┌───────────────────────────┼───────────────────────────┐             │
│      │                           │                           │             │
│  ┌───▼───┐  ┌───▼───┐  ┌───▼───┐  ┌───▼───┐  ┌───▼───┐     │             │
│  │Visib. │  │Sherlock│  │  Fix  │  │Report │  │ Lead  │     │             │
│  │Engine │  │Engine  │  │Engine │  │  Gen  │  │Capture│     │             │
│  └───┬───┘  └───┬───┘  └───┬───┘  └───┬───┘  └───┬───┘     │             │
│      │          │          │          │          │          │             │
│      └──────────┴──────────┴──────────┴──────────┘          │             │
│                           │                                  │             │
│                   ┌───────▼───────┐                          │             │
│                   │   Database    │                          │             │
│                   │   (SQLite)    │                          │             │
│                   └───────┬───────┘                          │             │
│                           │                                  │             │
└───────────────────────────┼──────────────────────────────────┘             │
                            │                                                 │
         ┌──────────────────┼──────────────────┐                             │
         │                  │                  │                             │
    ┌────▼────┐      ┌──────▼──────┐     ┌────▼────┐                         │
    │ OpenAI  │      │  Pinecone   │     │ Eidetic │                         │
    │Perplexity│     │  (Vectors)  │     │(MandelDB)│                        │
    │ Gemini  │      └─────────────┘     └──────────┘                        │
    └─────────┘                                                               │
```

### 2.3 Directory Structure

```
ekkoscope/
├── main.py                    # FastAPI application entry point
├── services/
│   ├── database.py            # SQLAlchemy models & session management
│   ├── visibility_hub.py      # Multi-LLM API orchestration
│   ├── query_generator.py     # Intent-classified query generation
│   ├── report_generator.py    # PDF report creation
│   ├── site_inspector.py      # Website content scraping
│   ├── auto_configure.py      # GPT-powered business configuration
│   ├── genius.py              # AI insights generation
│   └── memory/
│       ├── eidetic_client.py  # MandelDB integration
│       └── ekkobrain.py       # Local memory patterns
├── templates/
│   ├── public/                # Public-facing pages
│   │   ├── landing_v2.html    # Main landing page
│   │   ├── squeeze_audit.html # Product squeeze page
│   │   ├── squeeze_book.html  # Agency squeeze page
│   │   └── teaser_dashboard.html
│   ├── user/                  # Authenticated user pages
│   │   └── dashboard.html
│   └── admin/                 # Admin portal pages
│       └── dashboard.html
├── static/                    # Static assets (CSS, JS, fonts)
├── reports/                   # Generated PDF reports
├── data/                      # Configuration & queue files
│   ├── tenants.json
│   └── pending_eidetic_queue.json
└── docs/                      # Technical documentation
```

### 2.4 UI/UX Design System

EkkoScope V2 implements a "Boardroom" aesthetic designed for premium agency clients:

| Element | Specification |
|---------|---------------|
| **Background** | Light Gray (#F9FAFB) |
| **Sidebar/Headers** | Deep Navy (#111827) |
| **Primary CTA** | Royal Blue (#2563EB) |
| **Typography** | Inter font family |
| **Icons** | Heroicons (outline style) |
| **Charts** | Chart.js with brand colors |

---

## 3. AI Visibility Engine

### 3.1 Multi-Provider Architecture

EkkoScope queries three major AI providers to ensure comprehensive visibility measurement:

| Provider | API Type | Capability | Behavior Pattern |
|----------|----------|------------|------------------|
| **OpenAI (GPT-4)** | Chat Completions | Knowledge-based recommendations | Favors well-known brands in training corpus |
| **Perplexity** | Sonar API | Real-time web search with citations | Higher visibility for strong web presence |
| **Google Gemini** | Generative AI | Hybrid knowledge + web | Balanced approach |

### 3.2 Query Generation System

#### 3.2.1 Intent Classification

Queries are classified into five intent categories with assigned business value:

| Intent Type | Description | Value Score (1-10) | Example |
|-------------|-------------|-------------------|---------|
| **Emergency** | Urgent, immediate-need | 10 | "emergency plumber near me" |
| **High Ticket** | Large purchases/contracts | 9 | "best commercial HVAC contractor" |
| **Transactional** | Ready-to-buy | 8 | "buy roofing materials wholesale" |
| **Replenishment** | Recurring purchases | 7 | "monthly office supply delivery" |
| **Informational** | Research/comparison | 5 | "how to choose a roofing company" |

#### 3.2.2 Query Template System

Templates are customized by:
- **Business Type**: E-commerce, Local Service, B2B Service
- **Category**: Industry-specific keywords
- **Region**: Geographic location

**Local Service Templates:**
```
"best {category} in {region}"
"emergency {category} near {region}"
"top rated {category} company in {region}"
"who should I call for {category} in {region}"
```

**E-commerce Templates:**
```
"best place to buy {category} online"
"bulk {category} supplier for businesses"
"{category} supplier with fast shipping"
```

### 3.3 Scoring Algorithm

#### 3.3.1 Visibility Score Calculation

EkkoScope uses **provider-response level** scoring:

```
Visibility Score = (Total Provider Hits / Total Provider Probes) × 100
```

**Where:**
- **Total Provider Probes** = Queries × Providers with successful responses
- **Total Provider Hits** = Responses where target business was mentioned

#### 3.3.2 Per-Query Scoring

| Score | Condition |
|-------|-----------|
| 2 | Target is primary recommendation |
| 1 | Target is mentioned (not primary) |
| 0 | Target not mentioned |

#### 3.3.3 Risk Level Classification

| Score Range | Risk Level | Implication |
|-------------|------------|-------------|
| 0% | CRITICAL | Complete AI invisibility |
| 1-19% | HIGH | Rarely recommended |
| 20-49% | MODERATE | Inconsistent presence |
| 50%+ | LOW | Strong AI presence |

### 3.4 Data Integrity Guardrails

The Report Integrity Guardrail System prevents hallucinated scores:

1. **Primary Calculation**: Uses raw probe data (Python math, not LLM estimation)
2. **Override Protection**: Rejects LLM narrative if it conflicts with calculated score
3. **Forced Correction**: Overwrites misleading positive language at critical scores
4. **Template-Based Narratives**: Deterministic text generation for 0% or CRITICAL cases

---

## 4. Lead Capture & Teaser Audit System

### 4.1 Overview

The lead capture system converts website visitors into qualified leads through a gated free audit workflow:

```
Landing Page → Lead Modal → Capture & Audit API → Auto User Creation → 
Teaser Dashboard → Upsell Flow
```

### 4.2 Lead Capture Modal

**Fields Captured:**
| Field | Required | Validation |
|-------|----------|------------|
| Name | Yes | Non-empty string |
| Email | Yes | Valid email format |
| Phone | No | Optional contact |
| Business Domain | Yes | Valid URL/domain |

### 4.3 Teaser Audit Specifications

| Specification | Value |
|---------------|-------|
| **Query Count** | 1 high-impact query |
| **Providers** | Perplexity + ChatGPT only |
| **Target Response Time** | < 15 seconds |
| **Output** | Visibility score + top competitor |

### 4.4 Teaser Dashboard

The teaser dashboard (`/teaser/{audit_id}`) displays:

| Section | State | Purpose |
|---------|-------|---------|
| Visibility Score | Unlocked | Hook with immediate value |
| Top Competitor | Unlocked | Create urgency |
| 30-Day Action Plan | Blurred/Locked | Upsell trigger |
| Query Logs | Blurred/Locked | Upsell trigger |
| Trend Analysis | Blurred/Locked | Upsell trigger |

**Upsell CTA:** "Unlock Full Report" → Continuous tier ($297/month)

### 4.5 Squeeze Pages

Two dedicated marketing pages with zero navigation for conversion focus:

#### `/audit` - Product Squeeze
- **Headline**: "Check Your AI Visibility Score in 15 Seconds"
- **Input**: URL field with domain pre-fill
- **CTA**: "Run Free Scan" → Lead Modal
- **Design**: Clean white background, minimal elements

#### `/book` - Agency Squeeze
- **Headline**: "Stop Guessing. Let Us Fix Your AI Reputation."
- **Video**: VSL placeholder for sales video
- **Widget**: Calendly booking embed
- **Design**: Dark navy background, premium feel

### 4.6 API Endpoint

**POST /api/leads/capture-and-audit**

```json
{
  "name": "John Smith",
  "email": "john@example.com",
  "phone": "(555) 123-4567",
  "domain": "example.com"
}
```

**Response:**
```json
{
  "success": true,
  "lead_id": 123,
  "audit_id": 456,
  "redirect_url": "/teaser/456"
}
```

---

## 5. User Management & Authentication

### 5.1 User Model

| Field | Type | Description |
|-------|------|-------------|
| id | Integer | Primary key |
| email | String | Unique login identifier |
| password_hash | String | Bcrypt-hashed password |
| name | String | Display name |
| company | String | Optional company name |
| tier | Enum | snapshot, continuous, autofix |
| is_admin | Boolean | Admin portal access |
| created_at | DateTime | Account creation |
| stripe_customer_id | String | Stripe customer reference |

### 5.2 Authentication Flow

1. **Login**: Email + password → Session token
2. **Session**: Secure HTTP-only cookie
3. **Logout**: Session invalidation
4. **Auto-Login**: Lead capture creates account with temp password

### 5.3 Authorization Levels

| Level | Capabilities |
|-------|--------------|
| **Public** | Landing page, squeeze pages, lead capture |
| **User** | Dashboard, reports, settings |
| **Admin** | Client management, onboarding, all users |

---

## 6. EkkoBrain Memory System

### 6.1 Two-Layer Architecture

EkkoBrain implements a dual-layer memory system for persistent pattern learning:

```
┌─────────────────────────────────────────────────────────┐
│                    EkkoBrain Memory                      │
├─────────────────────────────────────────────────────────┤
│                                                          │
│  Layer A: Relational Memory (SQLite)                    │
│  ┌─────────────────────────────────────────────────┐    │
│  │ • Audit results & raw data                      │    │
│  │ • Query responses (JSON)                        │    │
│  │ • User/business configurations                  │    │
│  │ • Report metadata                               │    │
│  └─────────────────────────────────────────────────┘    │
│                                                          │
│  Layer B: Vector Memory (Pinecone)                      │
│  ┌─────────────────────────────────────────────────┐    │
│  │ • Semantic embeddings (3072 dimensions)         │    │
│  │ • Pattern recognition across audits             │    │
│  │ • Similarity-based recommendations              │    │
│  │ • Gap analysis vectors                          │    │
│  └─────────────────────────────────────────────────┘    │
│                                                          │
└─────────────────────────────────────────────────────────┘
```

### 6.2 Pinecone Index Configuration

| Setting | Value |
|---------|-------|
| **Index Name** | `ekkobrain` |
| **Embedding Model** | `text-embedding-3-large` |
| **Dimensions** | 3072 |
| **Metric** | Cosine similarity |

### 6.3 Namespace Organization

| Namespace | Content | Purpose |
|-----------|---------|---------|
| `business-content` | Client website data | Source of truth |
| `competitor-content` | Competitor website data | Comparison baseline |
| `audit-patterns` | Historical audit patterns | Pattern learning |
| `gap-missions` | Sherlock gap analysis | Action items |
| `strategic-insights` | AI recommendations | Knowledge base |

---

## 7. Eidetic Integration (MandelDB 2.0)

### 7.1 Architecture Overview

Eidetic AI provides external cloud-based memory following the MandelDB 2.0 "Total Recall" architecture:

```
┌─────────────────────────────────────────────────────────────────┐
│                      MandelDB (Eidetic AI)                       │
│                                                                  │
│  ┌─────────────────────┐     ┌─────────────────────────────┐   │
│  │     Layer A          │     │        Layer B               │   │
│  │  (Hippocampal Archive)│    │     (Cortex Synthesis)       │   │
│  │                      │     │                              │   │
│  │  Supabase Storage    │     │  Pinecone Vectors            │   │
│  │  Complete JSON Blob  │     │  + Knowledge Graph           │   │
│  │  SHA-256 Verified    │     │  + Typed Edges               │   │
│  │  IMMUTABLE           │     │  + Decay Weights             │   │
│  └─────────────────────┘     └─────────────────────────────┘   │
│                                                                  │
│  ┌─────────────────────────────────────────────────────────┐    │
│  │              Synaptic Isolation (RLS)                    │    │
│  │  All data scoped to namespace: ekkoscope_v1              │    │
│  └─────────────────────────────────────────────────────────┘    │
└─────────────────────────────────────────────────────────────────┘
```

### 7.2 Connection Details

| Setting | Value |
|---------|-------|
| **Production URL** | `https://mandeldb.com` |
| **Namespace** | `ekkoscope_v1` |
| **Auth Header** | `X-API-Key` |
| **Data Isolation** | Namespace-scoped RLS |

### 7.3 Node Taxonomy

| Node Type | Source Data | Decay Rate (λ) | Description |
|-----------|-------------|----------------|-------------|
| `MEMORY` | Raw LLM responses | 0.01 | Permanent record |
| `INSIGHT` | Recommendations | 0.05 | Actionable advice |
| `VILLAIN` | Competitors | 0.03 | Competitor tracking |
| `SCORE_TREND` | Audit scores | 0.01 | Time series data |

### 7.4 Available Endpoints

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `/api/v1/ekkoscope/archive` | POST | Dual-write audit ingestion |
| `/api/v1/ekkoscope/time-travel` | POST | Semantic search across history |
| `/api/v1/ekkoscope/competitor-history` | POST | Track competitor appearances |
| `/api/v1/ekkoscope/compare-logs` | POST | Compare LLM responses over time |
| `/api/v1/ekkoscope/archives/{domain}` | GET | List stored audits |
| `/api/v1/ekkoscope/score-trend/{domain}` | GET | Score progression for charting |
| `/api/v1/ekkoscope/archive/{id}/raw` | GET | Complete original JSON blob |

### 7.5 Durable Retry Queue

Failed writes persist to `data/pending_eidetic_queue.json` and auto-retry every 60 seconds:

```python
class EideticRetryQueue:
    def __init__(self):
        self.queue_file = "data/pending_eidetic_queue.json"
    
    def enqueue(self, audit_data):
        # Persist to disk for durability
        # Retry every 60 seconds until success
    
    def on_startup(self):
        # Drain any pending items from previous session
```

---

## 8. Sherlock Semantic Intelligence Engine

### 8.1 Purpose

Sherlock identifies **semantic topics** (not keywords) that competitors cover but the client does not. Unlike traditional keyword tools, Sherlock understands meaning and context.

### 8.2 Core Capabilities

| Capability | Description |
|------------|-------------|
| **Content Ingestion** | Scrapes and embeds website content into vector space |
| **Topic Extraction** | GPT-powered semantic theme identification |
| **Gap Analysis** | Compares client vs competitor vector spaces |
| **Mission Generation** | Creates actionable tasks from gaps |
| **Strategic Consultant** | RAG-powered Q&A ("Interrogation Room") |
| **Fabricator** | Generates files from missions (Schema, HTML, FAQ) |

### 8.3 Content Ingestion Pipeline

```
URL → Web Scrape → Extract Text → GPT Topic Extraction → 
Vector Embedding → Pinecone Upsert
```

**Topic Extraction Prompt:**
```
Analyze this website content and extract the main TOPICS covered.
Not keywords - identify the semantic concepts, themes, and subject areas.

For each topic, provide:
1. topic: A clear topic name (2-5 words)
2. category: The broader category (e.g., "services", "problems", "solutions")
3. depth: How thoroughly covered (1-10)
4. example_phrases: 2-3 key phrases from the content
```

### 8.4 Gap Analysis Algorithm

1. Retrieve client topics from ingested content
2. Retrieve competitor topics from ingested content
3. Identify topics present in competitor data but absent/weak in client data
4. Rank gaps by potential business value

**Output:**
- Missing topics (competitor has, client lacks)
- Weak topics (client has but competitor covers more deeply)
- Coverage comparison scores

### 8.5 Interrogation Room (RAG Chat)

Users can ask strategic questions like:
- "Why is Coastal Roofing beating me?"
- "What topics should I cover to improve visibility?"
- "How does my service page compare to competitors?"

The system retrieves relevant Pinecone documents and provides evidence-based strategic advice.

### 8.6 Fabricator (Asset Generation)

Turns missions into downloadable files:

| Asset Type | Output |
|------------|--------|
| **Schema** | JSON-LD structured data |
| **Landing Page** | HTML template |
| **FAQ Content** | Formatted Q&A pairs |
| **Meta Descriptions** | SEO-optimized text |

### 8.7 API Endpoints

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `/api/sherlock/ingest` | POST | Ingest website content |
| `/api/sherlock/analyze` | POST | Run gap analysis |
| `/api/sherlock/consult` | POST | RAG-powered Q&A |
| `/api/sherlock/fabricate/{mission_id}` | GET | Generate assets |

---

## 9. FixEngine Core (Autonomous Remediation)

### 9.1 Overview

FixEngine Core is an autonomous system that parses GEO reports and generates fixes automatically using specialized AI agents.

### 9.2 Pipeline Architecture

```
PDF Report → Parser → AI Fix Planner (GPT-4o) → 
Agent Router → [Content | SEO | Deploy | Verification] → 
Fix Package Output
```

### 9.3 Agent Specifications

| Agent | Responsibility | Output |
|-------|---------------|--------|
| **Content Agent** | Generate optimized content | Meta descriptions, FAQs, page content |
| **SEO Agent** | Create structured data | JSON-LD schema markup |
| **Deploy Agent** | Generate deployment code | WordPress PHP, raw HTML, API payloads |
| **Verification Agent** | Measure improvement | Before/after metrics comparison |

### 9.4 Fix Package Structure

```json
{
  "fix_id": "fix_abc123",
  "business_id": 42,
  "created_at": "2026-01-12T10:00:00Z",
  "fixes": [
    {
      "type": "schema",
      "target": "LocalBusiness",
      "content": "{...json-ld...}",
      "deploy_instructions": "Add to <head> section"
    },
    {
      "type": "content",
      "target": "services-page",
      "content": "...",
      "deploy_instructions": "Replace existing content"
    }
  ],
  "verification": {
    "pre_score": 12,
    "projected_improvement": "+25%"
  }
}
```

---

## 10. PDF Report Generation

### 10.1 Report Types

| Report | Description | Trigger |
|--------|-------------|---------|
| **Standard GEO Report** | Comprehensive visibility analysis | Full audit |
| **Dossier Report** | Narrative-driven intelligence format | On-demand |

### 10.2 Standard GEO Report Sections

1. **Cover Page**: Business name, report date, market focus
2. **Executive Dashboard**: Key metrics (visibility %, recommendations, score)
3. **Query Analysis**: Per-query breakdown with provider results
4. **Competitor Matrix**: Top competitors by mention frequency
5. **Multi-Source Visibility**: Provider comparison chart
6. **Genius Insights**: AI-generated strategic recommendations
7. **Page Blueprints**: Content specifications for new pages
8. **30-Day Action Plan**: Phased implementation tasks
9. **Recommendations**: Prioritized optimization actions

### 10.3 Dossier Report Format

Narrative-driven "Intelligence Dossier" that transforms data into a compelling forensic-to-coaching story:

**Section A: "The Forensic Audit"**
- CLASSIFIED cover page with INVISIBLE/DETECTED verdict stamp
- Suspect Lineup (top 3 competitors)
- "Smoking Gun" evidence from gap analysis

**Section B: "The Coach's Playbook"**
- 4-week implementation sprint
  - Week 1: Triage & Patching
  - Week 2: Content Counter-Attack
  - Week 3: Authority & Signals
  - Week 4: Re-Scan
- Fabricator integration with downloadable tools

### 10.4 Technical Specifications

| Specification | Value |
|---------------|-------|
| **Library** | FPDF2 (Python) |
| **Typography** | JetBrains Mono |
| **Page Size** | Letter (8.5" x 11") |
| **Color Scheme** | Dark theme with cyan accents (#00F0FF) |

---

## 11. Sales Mode (Headless Prospecting)

### 11.1 Purpose

Automated cold outreach system for prospecting at scale.

### 11.2 Workflow

```
Domain URL → Auto-Configure → Teaser Audit (3 queries) → 
Early-Exit Detection → Sales Packet → Hook Message
```

### 11.3 Specifications

| Feature | Specification |
|---------|---------------|
| **Auto-Configuration** | GPT-4o-mini infers business name, industry, location from URL |
| **Query Count** | Exactly 3 high-impact queries (emergency, high_ticket, transactional) |
| **Early-Exit** | Stops on first 0% visibility finding |
| **Output** | JSON with hook_message for personalized outreach |

### 11.4 Security

| Protection | Implementation |
|------------|----------------|
| **SSRF Prevention** | IPv4/IPv6 validation via `ipaddress` module |
| **Rate Limiting** | 5 requests/minute/IP |
| **Input Validation** | Domain sanitization |

### 11.5 API Endpoints

| Endpoint | Method | Purpose |
|----------|--------|---------|
| `/api/sales/configure` | POST | Auto-configure from URL |
| `/api/sales/teaser` | POST | Run single teaser audit |
| `/api/sales/batch` | POST | Batch process multiple domains |

### 11.6 Error Codes

| Code | Meaning |
|------|---------|
| 400 | Invalid input |
| 422 | Operational failure |
| 429 | Rate limit exceeded |
| 500 | Server error |

---

## 12. Swarm Commander (Domain Provisioning)

### 12.1 Purpose

Infrastructure-as-Code module for automated domain procurement and configuration.

### 12.2 4-Step Handshake

```
BUY (Namecheap) → HANDOVER (Cloudflare zone) → 
LINK (update nameservers) → FORTIFY (SPF/DKIM/DMARC)
```

### 12.3 Capabilities

| Step | Service | Action |
|------|---------|--------|
| **Domain Check** | Namecheap API | Verify availability before purchase |
| **Purchase** | Namecheap API | Register domain |
| **Zone Creation** | Cloudflare API | Create DNS zone |
| **Nameserver Update** | Namecheap API | Point to Cloudflare |
| **Security Records** | Cloudflare API | Auto-inject SPF, DKIM, DMARC |
| **MX Records** | Cloudflare API | Optional email provider config |

### 12.4 API Endpoints

| Endpoint | Method | Auth | Purpose |
|----------|--------|------|---------|
| `/api/swarm/check` | GET | None | Check domain availability |
| `/api/swarm/provision` | POST | X-Admin-Password | Execute 4-step handshake |
| `/api/swarm/status/{domain}` | GET | None | Check provisioning status |

### 12.5 Dry Run Mode

Simulate purchase without charging for testing:
```json
{
  "domain": "example.com",
  "dry_run": true
}
```

---

## 13. Payment Processing & Billing

### 13.1 Pricing Tiers

| Tier | Price | Billing | Capabilities |
|------|-------|---------|--------------|
| **Snapshot** | FREE | One-time | Single teaser audit, limited results, lead capture |
| **Continuous** | $297/month | Subscription | Bi-weekly audits, full reports, trend tracking |
| **Auto-Fix** | $997/month | Subscription | All Continuous features + AI agents + remediation |

*Note: Pricing is configurable via Stripe Price IDs in environment variables.*

### 13.2 Stripe Integration

| Component | Purpose |
|-----------|---------|
| **Products** | Continuous Monitoring, Auto-Fix Agents |
| **Prices** | Recurring monthly billing |
| **Checkout Sessions** | One-click subscription signup |
| **Customer Portal** | Self-service billing management |
| **Webhooks** | Real-time subscription updates |

### 13.3 Webhook Events Handled

| Event | Action |
|-------|--------|
| `checkout.session.completed` | Activate subscription, update user tier |
| `customer.subscription.updated` | Sync tier changes |
| `customer.subscription.deleted` | Downgrade to snapshot |
| `invoice.payment_failed` | Flag account, notify user |

### 13.4 Environment Variables

| Variable | Purpose |
|----------|---------|
| `STRIPE_SECRET_KEY` | API authentication |
| `STRIPE_PUBLISHABLE_KEY` | Frontend Stripe.js |
| `STRIPE_WEBHOOK_SECRET` | Webhook signature verification |
| `STRIPE_PRICE_CONTINUOUS_290` | Continuous tier price ID |
| `STRIPE_PRICE_REPORT_490` | One-time report price ID |

---

## 14. Admin Portal

### 14.1 Access Control

- **URL**: `/admin/dashboard`
- **Authentication**: Admin-only session check
- **Authorized Users**: `is_admin = True`

### 14.2 Capabilities

| Feature | Description |
|---------|-------------|
| **Client Overview** | All businesses with recent audit status |
| **Onboarding** | Add new clients with auto-configuration |
| **Audit Management** | Trigger audits, view results, download reports |
| **User Management** | View/edit user accounts |
| **Subscription Status** | Monitor active subscriptions |

### 14.3 Auto-Configuration

Admin onboarding leverages `auto_configure.py`:

1. **Input**: Business domain URL
2. **Scrape**: Extract website content via `site_inspector.py`
3. **Inference**: GPT-4o-mini determines:
   - Business name
   - Industry
   - Business type (local service, e-commerce, B2B)
   - Categories
   - Location
4. **Output**: Fully configured business record

---

## 15. API Reference

### 15.1 Public Endpoints

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/` | GET | Landing page |
| `/audit` | GET | Product squeeze page |
| `/book` | GET | Agency squeeze page |
| `/api/leads/capture-and-audit` | POST | Lead capture + teaser audit |
| `/teaser/{audit_id}` | GET | Teaser dashboard |

### 15.2 Authenticated Endpoints

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/dashboard` | GET | User dashboard |
| `/api/audit/{business_id}` | POST | Trigger full audit |
| `/api/report/{audit_id}` | GET | Download PDF report |
| `/api/analytics/{business_id}` | GET | Visibility analytics data |

### 15.3 Admin Endpoints

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/admin/dashboard` | GET | Admin portal |
| `/admin/onboard` | POST | Add new client |
| `/admin/trigger-audit/{business_id}` | POST | Trigger client audit |

### 15.4 Sherlock Endpoints

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/api/sherlock/ingest` | POST | Ingest website content |
| `/api/sherlock/analyze` | POST | Run gap analysis |
| `/api/sherlock/consult` | POST | RAG-powered Q&A |
| `/api/sherlock/fabricate/{mission_id}` | GET | Generate assets |

### 15.5 Sales Endpoints

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/api/sales/configure` | POST | Auto-configure from URL |
| `/api/sales/teaser` | POST | Headless teaser audit |
| `/api/sales/batch` | POST | Batch processing |

### 15.6 Swarm Endpoints

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/api/swarm/check` | GET | Check domain availability |
| `/api/swarm/provision` | POST | Provision domain |
| `/api/swarm/status/{domain}` | GET | Check status |

---

## 16. Security & Compliance

### 16.1 Authentication Security

| Measure | Implementation |
|---------|----------------|
| **Password Hashing** | Bcrypt with salt |
| **Session Tokens** | Secure HTTP-only cookies |
| **CSRF Protection** | Token-based validation |
| **Rate Limiting** | Request throttling |

### 16.2 API Security

| Measure | Implementation |
|---------|----------------|
| **API Keys** | Environment secrets (never logged) |
| **Webhook Verification** | Stripe signature validation |
| **Input Validation** | Pydantic models |
| **SSRF Protection** | IP address validation |

### 16.3 Data Protection

| Data Type | Protection |
|-----------|------------|
| **Passwords** | Bcrypt hash (never stored plain) |
| **API Keys** | Environment secrets |
| **User Data** | SQLite with file-system permissions |
| **Audit Data** | Namespace-scoped isolation (Eidetic) |

### 16.4 Third-Party Security

| Service | Security Measure |
|---------|------------------|
| **Eidetic/MandelDB** | Namespace-scoped RLS (Synaptic Isolation) |
| **Pinecone** | API key authentication |
| **Stripe** | Webhook signature verification |
| **OpenAI/Perplexity/Gemini** | Secure API key handling |

---

## 17. Deployment & Infrastructure

### 17.1 Hosting Environment

| Component | Provider |
|-----------|----------|
| **Application** | Replit |
| **Database** | SQLite (local) |
| **Vector Database** | Pinecone (cloud) |
| **External Memory** | Eidetic/MandelDB (cloud) |
| **Payments** | Stripe (cloud) |

### 17.2 Environment Variables

| Variable | Purpose |
|----------|---------|
| `OPENAI_API_KEY` | OpenAI API access |
| `PERPLEXITY_API_KEY` | Perplexity API access |
| `GOOGLE_GEMINI_API_KEY` | Gemini API access |
| `PINECONE_API_KEY` | Pinecone vector database |
| `EIDETIC_API_KEY` | MandelDB memory service |
| `STRIPE_SECRET_KEY` | Stripe payments |
| `SESSION_SECRET` | Session encryption |
| `ADMIN_PASSWORD` | Swarm Commander auth |

### 17.3 Workflow Configuration

**Primary Workflow: EkkoScope Server**
```bash
uvicorn main:app --host 0.0.0.0 --port 5000
```

### 17.4 Scaling Considerations

| Concern | Mitigation |
|---------|------------|
| **Database Scale** | Migrate to PostgreSQL for production |
| **API Rate Limits** | Queue-based processing for batch audits |
| **Memory** | Async operations, connection pooling |
| **Cost** | Teaser audits minimize API calls |

---

## 18. Roadmap

### 18.1 Implementation Status Matrix

| Module | Status | Lines of Code | Notes |
|--------|--------|---------------|-------|
| **Core Visibility Engine** | Production | 800+ | Full multi-LLM analysis |
| **Lead Capture System** | Production | 400+ | Teaser audits, auto-login |
| **PDF Report Generator** | Production | 600+ | Standard + Dossier formats |
| **Stripe Integration** | Production | 263 | Subscriptions + webhooks |
| **Admin Portal** | Production | 1000+ | Client management |
| **User Dashboard** | Production | 800+ | Full analytics |
| **Sherlock Engine** | Production | 1539 | Gap analysis, RAG chat, Fabricator |
| **Swarm Commander** | Production | 641 | 4-step domain provisioning |
| **Sales Mode** | Production | 223 | Headless teaser audits |
| **Eidetic Integration** | Production | 300+ | MandelDB dual-write |
| **FixEngine Agents** | Beta | 500+ | Content, SEO, Deploy agents |
| **Squeeze Pages** | Production | N/A | /audit and /book routes |

### 18.2 Near-Term (Q1-Q2 2026)

| Feature | Status |
|---------|--------|
| Enhanced FixEngine agent capabilities | Planned |
| White-label agency portal | Planned |
| API access for enterprise clients | Planned |
| Mobile-responsive dashboard | In Progress |
| Multi-language support | Planned |

### 18.3 Long-Term (2026-2027)

| Feature | Description |
|---------|-------------|
| **Voice AI Integration** | Monitor Siri, Alexa, Google Assistant |
| **Predictive Analytics** | ML-based visibility forecasting |
| **Automated Content Publishing** | Direct CMS integration |
| **Competitive Intelligence Dashboard** | Industry-wide visibility benchmarks |
| **Enterprise SSO** | SAML/OAuth integration |

---

## Appendix A: Scoring Formula Reference

```
Overall Visibility = Σ(is_target_found) / Σ(successful_probes) × 100

Provider Visibility = Σ(provider_target_found) / Σ(provider_probes) × 100

Query Score = 
  2 if target is primary recommendation
  1 if target is mentioned (not primary)
  0 if target not mentioned
```

---

## Appendix B: Intent Template Count

| Intent Type | Template Count |
|-------------|----------------|
| Emergency | 4 |
| High Ticket | 6 |
| Replenishment | 5 |
| Informational | 6 |
| Transactional | 5 |

---

## Appendix C: Database Schema

### Users Table
```sql
CREATE TABLE users (
    id INTEGER PRIMARY KEY,
    email VARCHAR UNIQUE NOT NULL,
    password_hash VARCHAR NOT NULL,
    name VARCHAR,
    company VARCHAR,
    tier VARCHAR DEFAULT 'snapshot',
    is_admin BOOLEAN DEFAULT FALSE,
    stripe_customer_id VARCHAR,
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP
);
```

### Businesses Table
```sql
CREATE TABLE businesses (
    id INTEGER PRIMARY KEY,
    name VARCHAR NOT NULL,
    domain VARCHAR,
    business_type VARCHAR,
    industry VARCHAR,
    categories JSON,
    location VARCHAR,
    user_id INTEGER REFERENCES users(id),
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP
);
```

### Audits Table
```sql
CREATE TABLE audits (
    id INTEGER PRIMARY KEY,
    business_id INTEGER REFERENCES businesses(id),
    visibility_score FLOAT,
    risk_level VARCHAR,
    competitors JSON,
    query_results JSON,
    is_teaser BOOLEAN DEFAULT FALSE,
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP
);
```

### Leads Table
```sql
CREATE TABLE leads (
    id INTEGER PRIMARY KEY,
    name VARCHAR NOT NULL,
    email VARCHAR NOT NULL,
    phone VARCHAR,
    domain VARCHAR NOT NULL,
    teaser_audit_id INTEGER,
    converted BOOLEAN DEFAULT FALSE,
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP
);
```

---

## Appendix D: Glossary

| Term | Definition |
|------|------------|
| **GEO** | Generative Engine Optimization - optimizing for AI recommendations |
| **LLM** | Large Language Model (ChatGPT, Gemini, etc.) |
| **Visibility Score** | Percentage of AI queries where business is mentioned |
| **Probe** | Single query sent to a single AI provider |
| **Teaser Audit** | Limited free audit (1 query, 2 providers) |
| **EkkoBrain** | Local memory system (SQLite + Pinecone) |
| **Eidetic** | Cloud memory service (MandelDB 2.0) |
| **Sherlock** | Semantic gap analysis engine |
| **FixEngine** | Autonomous remediation system |
| **Fabricator** | Asset generation from Sherlock missions |
| **Swarm Commander** | Domain provisioning module |

---

*Document generated from EkkoScope V2 codebase analysis*
*All technical claims verified against implemented functionality*
*Last updated: January 12, 2026*
