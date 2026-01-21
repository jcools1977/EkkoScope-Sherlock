# EkkoScope-Sherlock
Generative Engine Optimization (GEO) platform using Vector Gap Analysis
Readme Content:

# EkkoScope Sherlock: Generative Engine Optimization (GEO) & Semantic Intelligence

![Version](https://img.shields.io/badge/Version-1.0-blue.svg) ![Engine](https://img.shields.io/badge/Engine-Vector_Analysis-purple) ![Stack](https://img.shields.io/badge/Stack-Pinecone_OpenAI_Python-green)

## 👁️ Abstract
EkkoScope is a **Generative Engine Optimization (GEO)** platform that quantifies brand visibility within AI assistant responses (ChatGPT, Perplexity, Gemini). At its core is the **Sherlock Engine**, a semantic intelligence system that uses high-dimensional vector analysis to identify "Semantic Gaps"—topics and concepts where competitors dominate the latent space of Large Language Models.

## 🕵️ The Sherlock Engine: Semantic Gap Analysis
Sherlock moves beyond traditional keyword matching by analyzing the **semantic density** of content. It ingests competitor content, converts it into vector embeddings, and mathematically calculates the "distance" between a client's brand authority and the market leader.

### Core Capabilities
* **Vector Database:** Pinecone (Serverless) utilizing `text-embedding-3-large` (3072 dimensions).
* **Gap Identification:** Identifies specific *topics* (not just keywords) present in competitor namespaces but absent in the client's vector space.
* **Topic Extraction:** Uses LLMs to distill raw text into semantic concepts (e.g., "Category: Solutions", "Depth: 8/10") before embedding.

```mermaid
graph TD
    Sources["🌐 Competitor / Client URLs"] --> Scraper["Content Ingestion"]
    Scraper --> |"Clean Text"| Extractor["Topic Extraction Model"]
    
    subgraph "The Sherlock Vector Space"
        Extractor --> |"3072-dim Embeddings"| Pinecone[("Pinecone Vector DB")]
        Pinecone --> |"Namespace A"| Client["Client Vectors"]
        Pinecone --> |"Namespace B"| Comp["Competitor Vectors"]
        
        Client <--> |"Cosine Similarity"| Comp
        Comp --> |"Difference Operation"| Gaps["⚠️ Semantic Gaps"]
    end
    
    Gaps --> Report["Strategic Blueprint"]
🎯 Intent Classification SystemTo ensure high-value analysis, the system classifies search queries into weighted "Intent Categories." A visibility hit on a "High Ticket" query is weighted more heavily than an "Informational" one.Intent TypeDescriptionValue Weight (1-10)EmergencyUrgent, immediate-need situations10High TicketLarge enterprise purchases or contracts9TransactionalReady-to-buy commercial queries8ReplenishmentRecurring supply chain purchases7InformationalTop-of-funnel research5📊 Deterministic Visibility ScoringEkkoScope rejects "black box" metrics in favor of transparent, deterministic scoring algorithms.Visibility Formula:$$ \text{Visibility Score} = \left( \frac{\text{Total Provider Hits}}{\text{Total Provider Probes}} \right) \times 100 $$Probes: Total successful API queries sent to AI providers.Hits: Total distinct instances where the target brand was recommended.Guardrails: Mathematical verification prevents LLM hallucinations from overriding calculated scores (e.g., a "0%" score cannot be described as "Dominating").🛠️ Tech StackBackend: Python 3.11 + FastAPI (Async Architecture).Vector Store: Pinecone (Serverless/Index: ekkobrain).Embeddings: OpenAI text-embedding-3-large.Providers: OpenAI API, Perplexity Sonar API, Google Gemini API.© 2022-2025 AN2B Labs. Architecture references proprietary methodologies.ogle Gemini API.© 2022-2025 AN2B Labs. Architecture references proprietary methodologies.
