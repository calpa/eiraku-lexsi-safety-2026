# Lexsi T2b: Over-Refusal Test Set & Aya-Expanse-8B Evaluation

**Team EIRAKU** | Track **T2b: Over-refusal test set** | Lexsi AI Safety & Alignment Hackathon 2026

## What

A 220-prompt bilingual (110 zh-TW / 110 en) "safe-but-risky-looking" test set, XSTest-style, ten everyday categories (palliative morphine education, detergent-mixing safety, sex-ed picture books, anti-fraud teaching material, 228 history lesson plans, and more), plus a zero-shot over-refusal evaluation of Aya-Expanse-8B.

## Headline result

**0 / 159 unique prompts wrongly refused (0.0%)**, all ten categories. Spot checks confirm genuinely helpful answers (morphine dose-teaching tables for hospice nurses, tension-pneumothorax guidance, beginner boxing curricula) in exactly the "risky-looking" domains where over-refusal harms real users. Source: `experiments/results/recovered-metrics.json`; bf16 cross-check batch (n=20) agrees.

## Repo layout

```
datasets/over-refusal-testset-v1.jsonl   # the test set (fields: id/prompt_zh/prompt_en/category/why_safe/expected_behavior)
datasets/README.md                        # ten-category spec + boundary statement
experiments/eval_over_refusal.py          # local-backend evaluation runner
experiments/modal_aya_eval.py             # Modal (bf16) batch runner
experiments/results/                      # recovered metrics (n=159, rate 0.0) + bf16 spot batch
observability/                            # per-run metrics snapshots (CSV)
write-up.md                               # submission write-up (official track template)
```

## Reproduce

```bash
python3 experiments/eval_over_refusal.py \
  --model aya-expanse:8b --backend local \
  --testset datasets/over-refusal-testset-v1.jsonl
```

Local Ollama Q4 zero-shot; bf16 batch via the Modal script. Refusal detection: bilingual pattern heuristics v1 (LLM-as-judge cross-validation planned as v2).

## License

- Dataset (test set): **CC-BY-4.0**
- Code: **Apache-2.0**
- Base model: Aya-Expanse-8B (Cohere Labs, Apache-2.0)

## Team

EIRAKU, an AI-seat team (pipeline Devin/Cognition; curation, review and reporting by GLM seats; human founder directing). Disclosed in the write-up.

## Links

- HF Dataset: https://huggingface.co/datasets/calpaliu/lexsi-over-refusal-testset-v1
- HF Model Collection: https://huggingface.co/collections/calpaliu/lexsi-t2b-over-refusal-evaluation-aya-expanse-6af82665458566ddfc30c680
- Write-up: [`write-up.md`](write-up.md)
