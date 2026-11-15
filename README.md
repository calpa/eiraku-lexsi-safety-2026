# EIRAKU × Lexsi AI Safety & Alignment Hackathon 2026

**Team EIRAKU** (Yongle), a 15-agent AI company. Every part of this work (test-set curation, evaluation pipeline, security review, trajectory generation, documentation) was produced by our AI agents under the direction of our founder. We declare the team as EIRAKU; agents collaborate as seats, not individuals.

## Two artifacts, one submission

### 1. T2b: Over-Refusal Test Set & Aya-Expanse-8B Evaluation (primary)
A 220-prompt bilingual (110 zh-TW / 110 en) "safe-but-risky-looking" test set across ten everyday categories: palliative-care dosage teaching, household chemistry, sexual-health education, fraud-pattern recognition, historically sensitive education, and a zero-shot over-refusal evaluation of Aya-Expanse-8B.

**Result: 0 / 159 unique prompts wrongly refused (0.0%)**, all ten categories, spot-checked genuinely helpful (morphine dose-teaching for hospice nurses, tension-pneumothorax guidance, beginner boxing curricula).

→ [`t2b-over-refusal/`](t2b-over-refusal/) · dataset on HF: [calpaliu/lexsi-over-refusal-testset-v1](https://huggingface.co/datasets/calpaliu/lexsi-over-refusal-testset-v1)

### 2. T3 artifacts: zh-Hant Agentic Trajectory Dataset & Evaluation Framework (additional)
A replayable Traditional Chinese (Taiwan) agentic tool-calling dataset: 22 trajectories from Taiwanese-scenario seed tasks, byte-reproducible via a deterministic stub environment; three-metric harness (task success / tool-call accuracy / latency) cross-checked against AuditKIT; judge rubric + independent safety gate. Data quality secured by six rounds of adversarial review (four sandbox-bypass classes found and fixed, each with a negative fixture) and dual-sign-off manual review; the full record is in the repo.

**Validator: PASS (errors=0, warnings=0) · 43 tests passing · byte-replay verified.**

→ [`t3-trajectories/`](t3-trajectories/)

## Reproduce
```bash
# T2b evaluation (local Ollama)
python3 t2b-over-refusal/experiments/eval_over_refusal.py \
  --model aya-expanse:8b --backend local \
  --testset t2b-over-refusal/datasets/over-refusal-testset-v1.jsonl

# T3 dataset validation + tests
python3 t3-trajectories/scripts/validate_trajectory_dataset.py t3-trajectories/data/trajectories/zh-Hant/
cd t3-trajectories && python3 -m pytest tests/ -q   # 43 passed
```

## Licenses
- Code: **Apache-2.0**
- Datasets (test set + trajectories): **CC-BY-4.0**
- Base model: Aya-Expanse-8B (Cohere Labs, Apache-2.0)
- No Lexsi kit source redistributed; kits used via public PyPI / adapters only.

## Honesty notes
T2b refusal detection is v1 heuristics (LLM-as-judge cross-validation planned). T3 contains no real-model trajectories (rule-based generation, provenance disclosed); its real-model experiment protocol is defined but not yet run. Both limitations are stated in the respective write-ups.
