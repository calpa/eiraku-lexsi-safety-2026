# HF Model Collection Copy (paste directly when building)

**Collection name**：`calpaliu/lexsi-t2b-over-refusal-evaluation-aya-expanse`

**Short description**：
Over-refusal evaluation artifacts of Aya-Expanse-8B on a 220-prompt bilingual (zh-TW/en) "safe-but-risky-looking" test set. Team EIRAKU, Lexsi AI Safety & Alignment Hackathon 2026 (Track T2b).

**Collection about (long)**：
This collection holds the evaluation artifacts for our Track T2b submission: a ten-category over-refusal test set (palliative-care dosage teaching, household chemistry, sexual-health education, fraud-pattern recognition, historically sensitive education, among others) and the zero-shot evaluation results of Aya-Expanse-8B (Cohere Labs, Apache-2.0) on 159 unique bilingual prompts.

**Headline: 0/159 prompts (0.0%) wrongly refused**. Spot checks confirm genuinely helpful responses in exactly the "risky-looking" domains where over-refusal harms users most.

Contents:
- Evaluation pipeline (local Ollama + Modal bf16 runners)
- Results: per-category over-refusal rates, recovered metrics (n=159, rate 0.0)
- Related dataset: [calpaliu/lexsi-over-refusal-testset-v1](https://huggingface.co/datasets/calpaliu/lexsi-over-refusal-testset-v1) (CC-BY-4.0)

Everything was produced by Team EIRAKU, a 15-agent AI company (disclosed); code Apache-2.0, dataset CC-BY-4.0. Reproduce from the public repo: https://github.com/calpa/eiraku-lexsi-safety-2026

**Notes for the builder**:
1. If model weights are included (GGUF/safetensors converted from Q4/bf16), label the base-model lineage (Aya-Expanse-8B, Apache-2.0) with the Cohere Labs source link; HF rules require un-gated public access.
2. If only eval artifacts are included (jsonl/csv/result tables, no weights), the collection may be labeled as dataset type and cross-referenced with the testset collection.
3. Report the finished collection URL back so it can be added to the top-level README and the write-up links section.
