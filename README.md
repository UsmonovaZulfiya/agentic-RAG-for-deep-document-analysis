# Agentic RAG for Deep Document Analysis
*Reproducibility of “Building Three Pipelines to Select the Right LLMs for RAG, Multi-Agent Systems, and Vision”*

## Overview

This repository reproduces the experiment described in [Fareed Khan’s LevelUp article](https://levelup.gitconnected.com/building-three-pipelines-to-select-the-right-llms-for-rag-multi-agent-systems-and-vision-3e47e0563b76).  
The project implements an **Agentic Retrieval-Augmented Generation (RAG)** pipeline that uses **hierarchical chunking**, **multi-step reasoning**, and **model routing** to enable deep question answering over complex documents.

The pipeline simulates how autonomous agents can navigate large legal or technical documents — selecting relevant text, refining search depth, and synthesizing structured answers with citations.

## Core Features

- **Hierarchical Chunking** – recursively splits documents into semantically meaningful segments using sentence-level boundaries.  
- **Agentic Navigation** – a router model iteratively selects the most relevant text chunks based on a question.  
- **Answer Synthesis** – a large instruction-tuned model summarizes retrieved evidence into a concise, citation-rich answer.  
- **Metrics Tracking** – logs latency, token counts, and step-level performance for each reasoning stage.  
- **Reproducible Environment** – compatible with [Nebius AI Studio](https://studio.nebius.ai) for hosted LLM inference.

---

## Pipeline Architecture

1. **Document Loading** – Fetch a PDF (e.g., the *Trademark Trial and Appeal Board Manual of Procedure*, TBMP) and extract its text.  
2. **Hierarchical Chunking** – Divide the text into multi-level chunks for scalable navigation.  
3. **Routing & Reasoning** – Use a smaller, efficient model (e.g., `meta-llama/Meta-Llama-3.1-8B-Instruct`) to reason about which chunks are most relevant.  
4. **Recursive Exploration** – Subdivide selected chunks and re-evaluate until the maximum depth is reached.  
5. **Answer Synthesis** – A high-capacity model (e.g., `meta-llama/Llama-3.3-70B-Instruct`) generates a structured answer with citations.  
6. **Evaluation (optional)** – A separate model (e.g., `deepseek-ai/DeepSeek-V3`) can assess answer quality.

## Technology Stack

| Component | Purpose | Example Model / Library |
|---|---|---|
| **Nebius AI Studio** | Hosted LLM inference endpoint | Llama-3.1 / Llama-3.3 / DeepSeek-V3 |
| **Hugging Face Transformers** | Tokenization and text preprocessing | `AutoTokenizer` |
| **PyPDF** | PDF text extraction | `pypdf.PdfReader` |
| **NLTK** | Sentence tokenization | `sent_tokenize` |
| **TQDM** | Progress monitoring | `tqdm.auto` |
| **OpenAI Python SDK** | Unified API interface | `openai.OpenAI()` |

## 📈 Example Output

```text
--- GENERATED ANSWER ---
"The TBMP requires that a motion to compel discovery include a signed certificate of service,
specify the discovery requests at issue, and comply with standard formatting (ID: 1.3.5, 1.3.9)."

--- CITATIONS ---
['1.3.5', '1.3.9']
```

---

## 📚 Research Context

This project illustrates how **agentic reasoning** and **RAG** pipelines can be combined to:

- Improve interpretability of multi-step LLM reasoning.  
- Emulate cognitive search behaviors in autonomous agents.  
- Enable scalable document analysis in domains like law, policy, or science.

It can serve as a foundation for future work on:

- Multi-agent retrieval coordination  
- RAG evaluation benchmarks  
- Adaptive routing and answer aggregation strategies
  
## Citation

If you use this code in your own research, please cite the original source:

> Fareed Khan, *“Building Three Pipelines to Select the Right LLMs for RAG, Multi-Agent Systems, and Vision”*,  
> LevelUp, 2024. <https://levelup.gitconnected.com/building-three-pipelines-to-select-the-right-llms-for-rag-multi-agent-systems-and-vision-3e47e0563b76>

## Author Notes

This repository was created as part of a **reproducibility study** on RAG pipelines and agentic LLM architectures.  
It aims to provide both an educational resource and a stepping stone for deeper experiments in **multi-agent retrieval**, **LLM benchmarking**, and **explainable AI**.
