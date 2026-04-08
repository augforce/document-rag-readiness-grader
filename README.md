# 🎯 Document RAG Readiness Grader

> **Pre-ingestion quality assurance tool for RAG systems** - Validates documentation structure before it enters your knowledge base to prevent retrieval errors and hallucinations.

[![Vertex AI](https://img.shields.io/badge/Vertex_AI-4285F4?logo=google-cloud&logoColor=white)](https://cloud.google.com/vertex-ai)
[![Gemini 3.1 Flash](https://img.shields.io/badge/Gemini_3.1-Flash-blue)](https://cloud.google.com/vertex-ai/docs/generative-ai/model-reference/gemini)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

<img width="844" height="874" alt="Screenshot 2026-04-08 at 6 03 59 AM" src="https://github.com/user-attachments/assets/5b6af61a-8c21-4126-9891-ba7432967e96" />


---

## 📋 The Problem

While building **[SuccessorAgent](https://github.com/augforce/Successor-Agent)** (my hybrid RAG agent for IT operations), I noticed some of my documentation was formatted in a way that prevented it from being RAG-ready. These poorly structured documents caused:

- ❌ Low-quality vector embeddings (bad chunking)
- ❌ Reduced retrieval precision (missing metadata)  
- ❌ Hallucinations in production (semantic fragmentation)

**Initial testing revealed 20% of ingested documents degraded SuccessorAgent's performance.**

---

## 💡 The Solution

An AI-powered **quality gate** that evaluates documents before they enter the RAG pipeline. This tool acts as a document reviewer, analyzing three critical dimensions:

### Evaluation Framework

**1. Chunking Suitability (35%)**  
Can this document be split into clean, semantically coherent chunks for vector embeddings?
- Checks for clear headers, paragraph structure, code block formatting

**2. Metadata Clarity (30%)**  
Does it have searchable metadata for hybrid search retrieval?
- Validates title, version, keywords, dates, ownership

**3. Semantic Density (35%)**  
Is the content information-rich enough for accurate retrieval?
- Measures lexical diversity, technical term frequency, sentence complexity

Documents scoring **≥70/100** are approved for ingestion. Lower scores receive specific fix recommendations.

---

## 🏗️ Technical Stack

| Component | Technology | Justification |
|-----------|-----------|---------------|
| **LLM** | Gemini 3.1 Flash | 10x cheaper than Pro, optimized for analysis tasks |
| **Platform** | Google Vertex AI Studio | Serverless, pay-per-use pricing |
| **Temperature** | 0.2 | Ensures consistent, deterministic scoring |
| **Cost** | ~$0.05-0.10/document | Prevents costly re-indexing of poor documents |

---

## 📊 Real-World Results

**Testing on IT Documentation Library (47 documents):**

| Document Type | Avg Score | Action Taken | Impact on SuccessorAgent |
|---------------|-----------|--------------|--------------------------|
| Troubleshooting Guides | 82/100 | Added metadata headers | High retrieval accuracy |
| Policy Documents | 76/100 | Converted tables to lists | Improved chunking quality |
| Tutorials | 78/100 | Removed redundant sections | Better semantic coherence |
| Tabular Data | 35/100 | Excluded from ingestion | Prevented embedding errors |

### Measured Impact on SuccessorAgent Performance:
- ✅ **Retrieval accuracy:** +23% (68% → 91%)
- ✅ **Hallucination incidents:** Reduced from 20% to 5%
- ✅ **Re-indexing cycles:** Reduced from 4 to 1 (-75% rework)
- ✅ **Engineer time saved:** 6 hours/week (15% capacity increase)


---

## 🚀 How It Works
<img width="1408" height="768" alt="Gemini_Generated_Image_qkd4x0qkd4x0qkd4" src="https://github.com/user-attachments/assets/58294ebb-9ce6-449c-9186-24d9d9472577" />

**Example Output:**
🎯 OVERALL SCORE: 82/100

⚠️ TOP 3 FIXES:

1. **Add Explicit Metadata**: The document lacks a formal header block containing the document title, version, last updated date, and author. While the content is clear, RAG systems benefit significantly from explicit metadata fields to improve retrieval relevance.

2. **Hyperlink Context**: The document contains "here" as a hyperlink anchor. In a RAG context, the URL destination is often lost or stripped. Replace these with descriptive text (e.g., "Check the status of Apple services at [URL]").

3. **Standardize List Formatting**: The document uses inconsistent numbering (e.g., "1-", "a-", "1-"). While readable by humans, standardizing to a consistent Markdown hierarchy (H1, H2, H3, bullet points) will ensure the RAG parser correctly maintains the parent-child relationship between troubleshooting steps.

✅ STATUS: Ready for Production (minor revisions)

---

## 🔗 Integration with SuccessorAgent

This tool serves as the **QA layer** for my production RAG system:

**SuccessorAgent** → IT operations assistant built on Microsoft Foundry (GPT-4.1-mini + Azure AI Search)  
**RAG Readiness Grader** → Pre-ingestion validator ensuring only high-quality docs enter the knowledge base

**Workflow:**  
<img width="1686" height="738" alt="Screenshot 2026-04-08 at 6 25 11 AM" src="https://github.com/user-attachments/assets/acf3eed2-9241-4c60-a4fe-390c4fb5e047" />

---

## 📁 Repository Contents

- **`agent-instructions.txt`** - Complete prompt used in Vertex AI
- **`examples/`** - Real grading results from production docs

---

## 🎯 Key Takeaway

Quality documentation is the foundation of reliable RAG systems. This tool transforms document review from a manual, subjective process into an automated, consistent quality gate—directly improving the accuracy and reliability of production AI agents.

---

## 👨‍💻 About

Built by **Michael Augustine** as part of a portfolio demonstrating end-to-end RAG system development.

**Related Project:** [SuccessorAgent](https://github.com/augforce/Successor-Agent)  
**Contact:** [Linktree](https://linktr.ee/MichaelAugustine) | [Email](maugustine78@gmail.com)

---

## 📜 License

MIT License - See [LICENSE](LICENSE)

**If this tool helped your RAG implementation, please ⭐ star the repo!**
