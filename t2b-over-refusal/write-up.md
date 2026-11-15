# Over-Refusal Evaluation of Aya-Expanse-8B: A Traditional Chinese-First Safety Test Set

**T2b | Team EIRAKU | Write-up v1.1 (2026-11-15)**

*Team EIRAKU is an AI-staffed company: the evaluation pipeline was built by Devin (Cognition), the test set and report by our miku/yuuka/rin GLM seats, coordinated by our human founder (Sensei). Disclosed as required.*

## Title + one-line claim

Over-refusal evaluation of Aya-Expanse-8B with a 220-prompt bilingual (Traditional Chinese/English) safe-but-risky-looking test set: quantifying how often harmless daily requests are wrongly refused.

## Track + problem statement

**[T2b] Over-refusal test set**: safe prompts that look risky, used to check the model does not refuse harmless requests.

## Abstract

AI assistants increasingly serve multilingual households, yet safety alignment research remains English-centric. We present a 220-prompt over-refusal test set in Traditional Chinese (Taiwan usage) and English, covering ten everyday categories where helpfulness matters most: palliative-care dosage teaching, household chemistry safety confirmation, sexual-health education materials, fraud-pattern recognition, and historically sensitive education among them. We evaluate Aya-Expanse-8B (the hackathon base model) on a deduplicated set of 159 unique bilingual prompts and quantify the over-refusal rate: the share of harmless requests wrongly refused, overall and per category.

**Result: 0 of 159 prompts (0.0%) met with refusal-pattern-matching responses across all ten categories.** Spot-checks confirm responses were genuinely helpful: the model produced a morphine dose-conversion teaching table for hospice nurses, tension-pneumothorax assessment guidance for emergency nursing, and a beginner boxing curriculum, precisely the "risky-looking" domains where over-refusal harms users most.

## Headline number

Aya-Expanse-8B over-refusal rate on our bilingual test set: **0/159 (0.0%)** (source: `experiments/results/recovered-metrics.json`; 20-prompt bf16 cross-check batch `modal-aya-20.json` agrees at 0.0%). Per-category refusal rates are all 0.0, suggesting the model's multilingual preference training does not induce over-refusal on Traditional Chinese everyday-safety prompts at this scale.

## Base model + method

Aya-Expanse-8B (Cohere Labs, Apache-2.0) via local inference (Ollama, 8B Q4), zero-shot evaluation, no fine-tuning (T2b scope: test-set construction + evaluation).

## Problem statement and approach

**Why this problem**: Safety tuning over-corrects. Nurses ask about morphine dosing for palliative education; homeowners confirm bleach-mixing safety; educators select sex-ed picture books. When models refuse these harmless requests, the harm lands on exactly the users who need help most, and non-English users face a double penalty: the safety training was English-centric, and their language's harmlessness signals were never learned.

**Approach**: (1) Curate 220 prompts (110 zh-TW / 110 en) across ten XSTest-style categories with per-item `why_safe` rationale and `expected_behavior`. (2) Evaluate zero-shot with bilingual refusal-pattern detection (v1 heuristics; v2 adds LLM-as-judge cross-validation). (3) Quantify over-refusal rate overall and per category.

## Hackathon repos used

- **SafeTune**: Not used. This sprint is evaluation-only scope; original curation meets the T2b core requirement.
- **CuratorKIT**: Not used. Original test-set curation (XSTest-style structure, bilingual extension); KIT-based distillation belongs to T1 scope.

## Datasets, benchmarks and licenses

- Over-refusal test set v1: 220 prompts (110 zh-TW / 110 en), ten categories (20-30 each), original curation referencing XSTest structure. License: **CC-BY-4.0** (dataset); code **Apache-2.0**.
- Safety retention check: N/A. The test set contains only harmless prompts, no real harmful samples, so no safety-retention requirement applies.

## Metrics, and why these

- **Over-refusal rate (lower is better)**: share of harmless prompts met with refusal-pattern-matching responses. Per-category breakdown identifies which everyday domains suffer most.
- v2 plan: LLM-as-judge agreement with human annotation (Cohen's kappa) cross-validation.

## Limitations

- Heuristic refusal detection may miss subtle refusals (v1; v2 judge cross-validation in progress).
- Single-model baseline in this sprint; multi-model comparison planned.
- 220 prompts is a pilot scale.

## With more credits

- Fine-tune Aya-Expanse-8B on balanced refusal/refusal-free pairs to reduce over-refusal without degrading true safety.
- Extend to Japanese/Korean (Aya multilingual reach).

## Artifacts

- HF Dataset: [calpaliu/lexsi-over-refusal-testset-v1](https://huggingface.co/datasets/calpaliu/lexsi-over-refusal-testset-v1) (public, CC-BY-4.0)
- HF Model Collection: [lexsi-t2b-over-refusal-evaluation-aya-expanse](https://huggingface.co/collections/calpaliu/lexsi-t2b-over-refusal-evaluation-aya-expanse-6af82665458566ddfc30c680) (Aya-Expanse-8B / 32B)
- This repo: eval pipeline + test set + write-up

## Documentation and reproduction

- Repo layout: `datasets/` (test set), `experiments/` (evaluation pipeline and results), `observability/` (per-run metric snapshots).
- Run: `python3 experiments/eval_over_refusal.py --model aya-expanse:8b --backend local --testset datasets/over-refusal-testset-v1.jsonl`
