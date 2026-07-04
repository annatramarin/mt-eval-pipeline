# MT Evaluation Pipeline

A practical evaluation of Machine Translation quality using automatic metrics and human error analysis.

## What this does

1. Loads a sample of the [FLORES-200](https://huggingface.co/datasets/facebook/flores) benchmark (English source + Italian reference translations)
2. Translates the source sentences using the **DeepL API**
3. Adds a second language pair (**English → Japanese**) where native-speaker judgement isn't available — and discusses what that means for evaluation at scale
4. Scores translations with two complementary metrics:
   - **BLEU** (sacrebleu) — fast, interpretable, widely cited
   - **COMET** (unbabel-comet) — neural, reference-based, much closer to human judgement
5. Performs a **manual error analysis** on a 30-sentence sample, tagging errors as fluency / adequacy / terminology
6. Discusses where the metrics agree, where they diverge, and what that tells us about their limits

## Setup

```bash
git clone https://github.com/YOUR_USERNAME/mt-eval-pipeline.git
cd mt-eval-pipeline

python -m venv .venv
source .venv/bin/activate      # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

Create a `.env` file in the root:
```
DEEPL_API_KEY=your_free_tier_key_here
```

Then open the notebook:
```bash
jupyter notebook notebooks/mt_evaluation.ipynb
```

## Key findings

*(Filled in after running the notebook)*

## Structure

```
mt-eval-pipeline/
├── notebooks/
│   └── mt_evaluation.ipynb   ← main analysis
├── data/                      ← gitignored; populated at runtime
├── results/                   ← saved CSVs and plots
├── requirements.txt
└── README.md
```

## Metrics used

| Metric | Type | Range | Notes |
|--------|------|--------|-------|
| BLEU | n-gram overlap | 0–100 | Fast; penalises paraphrase |
| COMET (wmt22-comet-da) | Neural (DA) | ~0–1 | Correlates better with human judgement |

## Why two metrics?

BLEU and COMET frequently disagree. A sentence can score low on BLEU (different word choices from the reference) but high on COMET (semantically accurate, fluent). Understanding *when* they diverge — and why — is the core analytical question of this project.
