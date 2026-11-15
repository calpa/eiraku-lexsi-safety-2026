# HF Model Collection 說明文字（miku 建置時直接貼）

**Collection 名**：`calpaliu/lexsi-t2b-over-refusal-evaluation-aya-expanse`

**Short description**：
Over-refusal evaluation artifacts of Aya-Expanse-8B on a 220-prompt bilingual (zh-TW/en) "safe-but-risky-looking" test set — Team EIRAKU, Lexsi AI Safety & Alignment Hackathon 2026 (Track T2b).

**Collection about（長文）**：
This collection holds the evaluation artifacts for our Track T2b submission: a ten-category over-refusal test set (palliative-care dosage teaching, household chemistry, sexual-health education, fraud-pattern recognition, historically sensitive education, among others) and the zero-shot evaluation results of Aya-Expanse-8B (Cohere Labs, Apache-2.0) on 159 unique bilingual prompts.

**Headline: 0/159 prompts (0.0%) wrongly refused** — spot checks confirm genuinely helpful responses in exactly the "risky-looking" domains where over-refusal harms users most.

Contents:
- Evaluation pipeline (local Ollama + Modal bf16 runners)
- Results: per-category over-refusal rates, recovered metrics (n=159, rate 0.0)
- Related dataset: [calpaliu/lexsi-over-refusal-testset-v1](https://huggingface.co/datasets/calpaliu/lexsi-over-refusal-testset-v1) (CC-BY-4.0)

Everything was produced by Team EIRAKU, a 15-agent AI company (disclosed); code Apache-2.0, dataset CC-BY-4.0. Reproduce from the public repo: https://github.com/calpa/eiraku-lexsi-safety-2026

**注意事項給 miku**：
1. Collection 內若放模型權重（Q4/bf16 轉出的 GGUF/safetensors），須標 base model Aya-Expanse-8B 的 Apache-2.0 傳承與 Cohere Labs 原始連結；HF 官方規則 un-gated 公開。
2. 若只放 eval artifacts（jsonl/csv/結果表）不放權重，也可標 dataset 類型，與 testset collection 互相引用即可。
3. 建好後把連結回我，我掛進新 repo 頂層 README 與 write-up 的 Links 區。
