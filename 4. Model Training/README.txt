Smart Tenant Profiling: AI-Driven Analysis for Commercial Real Estate

This repository supports the Named Entity Extraction (NEE) project, extracting tenant profiles from 200 synthetic email chains for CRE advising. Using DistilBERT and T5 models fine-tuned with W&B sweeps, T5's best model (macro F1 = 0.6035) outperforms DistilBERT's (0.4773). Parsing errors (e.g., lastname: "fosterchenorgan" in GreenWave) require post-processing.

Repository Structure

1. Data Generation

- data_generation.ipynb: Generates 200 email chains using GPT with prompt.txt.
- prompt.txt: CRE tenant scenario prompts.
- synthetic_email_data.json: Raw dataset of email chains.
- used_contexts.json: Tracks industry contexts for diversity.
- used_names.json: Logs tenant names to avoid duplication.

2. Data Cleaning

- clean_data.json: Standardized dataset (e.g., GrowthStage: early-stage, scaling, mature).
- data_diversity.ipynb: Analyzes diversity (e.g., skewed MovingTimeline) and applies CONSOLIDATION_MAPS.

3. Data Splitting

- data_split.ipynb: Splits dataset into 70% train (train.json), 15% validation (val.json), 15% test (test.json).
- train.json, val.json, test.json: Split datasets with profiles.

4. Model Training

- distilbert_outputs/: DistilBERT predictions/metrics (best: glorious-sweep-1, macro F1 = 0.4773).
- t5_outputs/: T5 predictions/metrics (best: toasty-sweep-4, macro F1 = 0.6035).
- sweepsDistilBert.ipynb: 25 W&B sweeps for DistilBERT (learning rate: 1e-5–5e-5).
- sweepst5.ipynb: 25 W&B sweeps for T5 (learning rate: 5e-5–3e-4).

Usage

- Run data_generation.ipynb to create emails.
- Use data_diversity.ipynb to clean data, producing clean_data.json.
- Execute data_split.ipynb for train/validation/test splits.
- Train models with sweepsDistilBert.ipynb and sweepst5.ipynb.

Requirements

- Python 3.8+
- Libraries: transformers, wandb, fuzzywuzzy, pandas, numpy
- Hardware: GPU

Future Work

- Augment dataset for sparse entities (PainPoints).
- Normalize T5 outputs with regex/spaCy.
- Integrate with tenant profiling and advising pipeline.

Contributors

- Julius Balbus
- Lidia Nehmad
