# over-refusal-testset-v1

T2b over-refusal test set v1: bilingual (zh-TW / en), safe prompts that look risky.

## Specification

| Item | Value |
|---|---|
| Total prompts | 220 rows (10 categories, 20-30 rows each; 10 prompts x 2 bilingual variants minimum) |
| Languages | zh 110 + en 110 (every row carries both `prompt_zh` and `prompt_en`) |
| Structural basis | XSTest (safe-but-looks-risky taxonomy) + OR-Bench-style field structure |
| Fields | id / prompt_zh / prompt_en / category / why_safe / expected_behavior / test_language |
| id format | `t2b-<code>-<nn>-<zh\|en>` (rows ending `-zh` test in Traditional Chinese, rows ending `-en` test in English; content is pairwise parallel) |

## Ten-category distribution

| category | rows | coverage |
|---|---|---|
| medical_terms | 24 | palliative morphine education, anatomy, prescription dosing, self-harm prevention counseling |
| violence_metaphors | 20 | competitive metaphors, wuxia creative writing, stage combat |
| legal_boundaries | 20 | self-defense requirements, will formats, consumer-protection law |
| household_chemistry | 20 | detergent-mixing safety, saponification value, flame tests |
| weapons_history | 22 | military-history essays, museum curation, chess rule origins |
| adult_health | 30 | emergency-contraception education, HPV vaccine, prostate health |
| taboo_words_innocent | 20 | sex-ed picture books, fairy-tale wolves, homographs |
| diversity_equity | 20 | transgender honorific guidance, migrant-worker reporting guidelines, accessible travel |
| privacy_security_daily | 22 | anti-fraud teaching material, phishing-email checkpoints, account-takeover response |
| sensitive_history_education | 20 | 228 Incident lesson plans, oral-history ethics, transitional-justice comparisons |

## Boundary statement

- This test set contains no genuinely harmful prompts (red-team attack prompts belong to T2a and are not included here).
- Every prompt is harmless while its surface vocabulary tends to trigger safety filters; each carries a `why_safe` rationale and the `expected_behavior` (answer, do not refuse).
- Traditional Chinese prompts are written in Taiwan usage (prescription-form terminology, acetaminophen, condominium management regulations, the 228 Incident, and other local context).

## Validation

- JSONL parses line-by-line; ids all unique; zero missing values across the six fields.
- 20-prompt human spot review: "harmless yet risky-looking" held 20/20.
- Harmful-keyword scan (weapons synthesis, explosives, violence instruction, etc.): 0 hits.
