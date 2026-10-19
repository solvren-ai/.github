# Solvren AI

AI forward deployment for mid-market regulated teams. One production AI workflow per engagement, built inside your own cloud.

## What we do

- Our engineers embed with your team and build one production AI workflow per engagement.
- The build runs inside your own AWS, Azure or GCP account, on models you already approved.
- You keep the code, the infrastructure and the runbooks.
- Systems we have built: an AI skills registry with security scanning, agentic payments on Amazon Bedrock AgentCore, and Class 1 Decider, a small routing layer in front of LLM calls.

We work with biotech, healthcare, defense, legal and fintech teams. Founded in 2026, based in San Diego.

## Open models & datasets

| Artifact | What it is | Result |
|---|---|---|
| [class1-router-qwen3-0.6b-mlx](https://huggingface.co/SolvrenAI/class1-router-qwen3-0.6b-mlx) | Qwen3-0.6B LoRA request router, MLX | 0.88 accuracy on 50 hand-written requests (untuned Qwen3-4B: 0.90), a third to half the p50 latency |
| [class1-router-synthetic](https://huggingface.co/datasets/SolvrenAI/class1-router-synthetic) | Router training data, no real PII or PHI | 1,536 template rows + 50 hand-written test rows |
| [bge-base-en-v1.5-hipaa](https://huggingface.co/SolvrenAI/bge-base-en-v1.5-hipaa) | HIPAA retrieval embeddings | NDCG@10 0.907 vs 0.834 for the base model, 99 held-out queries |
| [hipaa-retrieval-pairs](https://huggingface.co/datasets/SolvrenAI/hipaa-retrieval-pairs) | Query-passage pairs over 45 CFR Parts 160 and 164 | 912 pairs over 304 regulation chunks |
| [hipaa-fda-rag-eval](https://huggingface.co/datasets/SolvrenAI/hipaa-fda-rag-eval) | Synthetic RAG eval QA over HIPAA 45 CFR 164 and FDA device-cybersecurity guidance, plus a 345-chunk corpus | 162 QA rows; reference answers are noisy (see below) |

Read the numbers with care:

- These are demos trained on synthetic or LLM-generated data.
- The test sets are small (n=50 and n=99), so one error moves the router's accuracy by 2 points.
- Router latency was measured on one shared laptop that was running other jobs, so it is approximate.
- In the RAG eval set, about 28% of spot-checked reference answers are partial or wrong, and two-thirds of questions are yes/no with answers skewed heavily to "Yes". Use it mainly for retrieval recall; the card has details.
- On the HIPAA eval the fine-tuned embedding model also scores ahead of bge-large-en-v1.5 (0.864) and snowflake-arctic-embed-m-v1.5 (0.865), with no meaningful change on BEIR SciFact.

Each model card covers the eval setup and its limitations.

## Code

- [solvren-ai/class1-router](https://github.com/solvren-ai/class1-router): data generation, LoRA training and evaluation for the router
- [solvren-ai/domain-embedding-finetune](https://github.com/solvren-ai/domain-embedding-finetune): local embedding fine-tuning pipeline
- [solvren-ai/rag-eval-generator](https://github.com/solvren-ai/rag-eval-generator): synthetic RAG evaluation set generation

## Compliance and partners

We build for teams working under HIPAA, SOC 2, ITAR and CMMC. Compliance and any certification or authorization stay with your organization and your auditors.

Solvren AI is an OpenAI Select Partner and an AWS Partner Network member.

## Citing our work

Each model and dataset card has a Citation section with a BibTeX entry and upstream credits. Please cite the specific artifact you use.

## Contact

[solvren.ai](https://solvren.ai) · [Contact](https://solvren.ai/contact/) · [nitya@solvren.ai](mailto:nitya@solvren.ai)
