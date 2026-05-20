# INSES: Intelligent Navigation & Similarity-Enhanced Search

**INSES** is an advanced multi-hop reasoning framework designed for complex Question Answering (QA) over incomplete, noisy, or sparse knowledge structures. By integrating a lightweight QA complexity router with an LLM-driven graph navigation loop, INSES dynamically balances computational efficiency, latency, and reasoning precision.

---

## ✨ Key Features

* **LLM-guided Navigation and similarity expansion:**  INSES couples LLM-guided navigation, which prunes noise and steers exploration, with embedding-based similarity expansion to recover
hidden links and bridge semantic gaps.
* **Dynamic QA Routing:** Features a strict binary complexity classifier that dynamically intercepts user queries. Simple questions (1–2 hops) are routed directly to a Naive RAG pipeline, while complex queries (≥ 3 hops) escalate to the Graph Search loop, significantly cutting down API latency and token expenditure.
* **Hybrid Storage Architecture:** Seamlessly unifies high-performance vector similarity search (via Qdrant) with relational graph topology (via Neo4j) to maximize retrieval contextual integrity.

---

## Installation
```bash
# Python 3.10+ recommended
pip install -r requirements.txt
```

### Optional services via Docker
```bash
# install Docker, Qdrant, Neo4j
# Start Qdrant & Neo4j
docker compose up -d
```

## Configure API keys & endpoints
Edit `.env`:
```
ZHIPUAI_API_KEY=...
DEEPSEEK_API_KEY=...
OPENAI_API_KEY=sk-...
QDRANT_URL=http://localhost:6333
QDRANT_API_KEY=             # if you enabled auth
NEO4J_URI=bolt://localhost:7687
NEO4J_USERNAME=neo4j
NEO4J_PASSWORD=your_password
```

Most classes accept params directly; environment variables are a convenient default.

## Quickstart
Run the demo router over a small sample:
```bash
# End-to-end run
python rag_router.py --dataset 2wiki --sample_size 1000 --llm_provider zhipuai --model glm-4
```

## Datasets
`data/` includes JSON files such as `2wiki.json`, `hotpotqa.json`, `musique.json`.
Each item typically contains fields like `question`, `answer`, and rich context (entities, supporting_facts, evidences).

## Project Layout
```
inses/
  data/
  inses/
    data_loader.py
    evaluator.py
    inses_retriever.py
    llmer.py
    llm_factory.py
    neo4j_graphdb.py
    neo4j_manager.py
    qdrant_vectordb.py
    rag_router.py
  results/
  graphdb_backups/
  graph_mine/
    kg_loader.py
    kg_search.py
```
