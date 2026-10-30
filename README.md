<div align="center">

# Hi there👋

<picture><source media="(prefers-color-scheme: dark)" srcset="https://github-readme-stats-theta-black-78.vercel.app/api?username=tmdals3000&show_icons=true&theme=midnight-purple&hide_border=true&bg_color=0d1117&v=3" /><img src="https://github-readme-stats-theta-black-78.vercel.app/api?username=tmdals3000&show_icons=true&theme=default&hide_border=true&v=3" width="45%"/></picture> <picture><source media="(prefers-color-scheme: dark)" srcset="https://github-readme-stats-theta-black-78.vercel.app/api/top-langs/?username=tmdals3000&layout=compact&theme=midnight-purple&hide_border=true&bg_color=0d1117&v=3" /><img src="https://github-readme-stats-theta-black-78.vercel.app/api/top-langs/?username=tmdals3000&layout=compact&theme=default&hide_border=true&v=3" width="45%"/></picture>

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://streak-stats.demolab.com/?user=tmdals3000&theme=midnight-purple&hide_border=true&background=0d1117" />
  <img src="https://streak-stats.demolab.com/?user=tmdals3000&theme=default&hide_border=true"/>
</picture>

</div>

## I'm Seungmin Lee

### LLM Search · RAG · AI Agents · Data Pipelines

> **I build LLM-powered search and RAG systems, then check whether they actually work.**

LLM을 실제 검색·추천 서비스에 붙이는 것에 관심이 있습니다.
**데이터를 모으고 → 파이프라인을 만들고 → 실측으로 검증하고 → 틀린 결과의 원인을 고치는 과정**을 중요하게 생각합니다.

---

## 🚀 What I Do

| Area | Experience |
| --- | --- |
| 🛒 **LLM Search / Agents** | Google ADK pipeline, query refinement, candidate matching, multi-turn clarify (HITL) |
| 🔎 **RAG** | Ko-MIRACL corpus building, hard negatives, HyDE, retrieval evaluation (Recall / MRR / nDCG) |
| 🧹 **Data Pipelines** | Web crawling, resumable collection, ingredient normalization, Wikipedia / Wikidata enrichment |
| 🛡️ **Search Reliability** | Mismatch guards, trust-signal ranking, suspicious-listing demotion |
| 📱 **Frontend** | React / TypeScript chat UI, mobile rendering performance |

---

# ⭐ Featured Projects

## 01. [αlpha Pick](https://github.com/tmdals3000/Alpha_Pick) · `2026.08 – 09`

### LLM Shopping Assistant · [Live](https://alpha-pick-jet.vercel.app)

**Problem**
Shopping searches return accessories, wrong models, and suspicious listings. Users need one grounded answer, not a long list.

**Architecture**

```text
User query / product photo
        ↓
Query refine (HCX)
        ↓
11st web ranking search
        ↓
Relevance + price filters
        ↓
Matching guards / trust signals   ← my part
        ↓
AI detailed search (multi-turn)   ← my part
        ↓
Recommendation with reasons
```

**My Contribution**

* Family-based guard to stop matches caused by different spec notations
* Exclusive-token guard to block "same word, different product" matches
* Suspicious-listing demotion using trust signals (seller listing count, price far below median, contract-style wording)
* Designed and improved AI detailed search (facet auto-submit, conversational query cleanup)
* Search autocomplete, chat UI (timestamps, retry, edit), mobile performance fixes

**Validation (team)**

* 100 live use cases across 10 categories
* 3-way architecture benchmark: Precision **66.0%** (current) vs **70.0%** (previous)

**Focus:** `LLM Agent` `Search Quality` `HITL` `React`

---

## 02. [Knowledge RAG QA](https://github.com/tmdals3000/knowledge-rag-qa) · `2026.07`

### Korean Knowledge-Base QA · Likelion NLP Project

**Problem**
Most knowledge sits in large document corpora. Users ask in natural language, not keywords, so retrieval quality caps answer quality.

**Architecture**

```text
Ko-MIRACL
    ↓
Reduced corpus (BEIR-style, hard negatives)   ← my part
    ↓
Wikipedia / Wikidata metadata                 ← my part
    ↓
Retriever (bge-m3)
    ↓
HyDE query rewrite (optional)                 ← my part
    ↓
Answer generation
    ↓
Retrieval + generation evaluated separately
```

**My Contribution**

* Built reduced corpora with multiple seeds and sizes (after mentor feedback)
* Removed hard negatives that duplicated correct documents
* Wikipedia / Wikidata metadata enrichment pipeline
* HyDE query-rewrite option
* Comparison scripts for HyDE, candidate pool size, and rerankers on the deployed search API

**Result (team)**

| Experiment | Metric | Result |
| --- | --- | ---: |
| bge-m3 baseline | MRR@10 | 0.7585 |
| Retriever fine-tuning | Recall@5 | +7.8% |
| Retriever fine-tuning | MRR@1 | +14.0% |

**Focus:** `RAG` `Retrieval` `Evaluation` `Data Pipeline`

---

## 03. [Étiquette](https://github.com/tmdals3000/etiquette_Throughlabel) · `2026.07 – 08`

### Label-Scan Skincare Assistant

**Problem**
Products made in the same factory can differ up to 5× in price by brand, but shoppers can't see that.

**My Contribution**

* Expanded suncream data from a 50-product sample to a full crawl of **596 products**
* Resumable crawling: each product is saved right away, so a stopped run continues where it left off
* Ingredient normalization pipeline on the full-crawl data
* Ingredient-interaction knowledge-base builder (10-sample dry run)

**Focus:** `Crawling` `Data Normalization` `Knowledge Base`

---

## 04. [Keyphrase Extraction](https://github.com/tmdals3000/keyphrase-extraction) · `2026.07`

### Hybrid Keyphrase Generation for Retrieval · Likelion NLP Project

**Problem**
Searches fail when a document uses different words than the user (vocabulary mismatch). Extraction-only methods can't produce keyphrases absent from the text.

**Result (team)**

| Method | F1@10 |
| --- | ---: |
| Baseline | 0.1672 |
| SciBERT hybrid (P7) | **0.2621** (+56.8%) |

**Focus:** `NLP` `Keyphrase` `IR`

---

## 💡 Highlights

**Finding wrong matches in search**

* Products with different spec notations were matched as the same item. I grouped products by model family and only matched within a family.
* Some candidates shared a keyword but were different products. An exclusive-token guard now rejects them.

**Fixing data before evaluating**

* Hard negatives overlapped with correct documents, which would distort evaluation. I removed those duplicate IDs before running experiments.

**Mobile performance**

* The sidebar lagged on mobile because toggling it re-rendered the whole app. Moving the `isOpen` subscription down to leaf components fixed the lag.

---

## 🛠 Tech Stacks

### AI / ML
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white)
![Hugging Face](https://img.shields.io/badge/Hugging%20Face-FFD21E?style=for-the-badge&logo=huggingface&logoColor=black)
![OpenAI](https://img.shields.io/badge/OpenAI-412991?style=for-the-badge&logo=openai&logoColor=white)
![Google ADK](https://img.shields.io/badge/Google%20ADK-4285F4?style=for-the-badge&logo=google&logoColor=white)

### Lang / Frameworks
![React](https://img.shields.io/badge/React-61DAFB?style=for-the-badge&logo=react&logoColor=black)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![Node.js](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=node.js&logoColor=white)
![Java](https://img.shields.io/badge/Java-007396?style=for-the-badge&logo=java&logoColor=white)
![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)

### Data / Infra
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
![Supabase](https://img.shields.io/badge/Supabase-3FCF8E?style=for-the-badge&logo=supabase&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)

### UI/UX Design
![Figma](https://img.shields.io/badge/Figma-F24E1E?style=for-the-badge&logo=figma&logoColor=white)

