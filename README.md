# BibTri-Align
BibTri-Align: A Trilingual Bible Corpus for Low-Resource Machine Translation in Sundanese

This repository hosts BibTri-Align v2, a trilingual parallel corpus aligning Sundanese, Indonesian, and English Bible translations. To our knowledge, this is the first systematically aligned trilingual resource for these three languages that also includes metadata on alignment confidence.

The resource is introduced in our article, which was submitted to Language Resources and Evaluation.

Contents

data/ – Corpus files in CSV and JSONL formats, with alignment confidence metadata.
scripts/ – Preprocessing, alignment, heuristic scoring, and evaluation scripts.
docs/ – Documentation, including annotation guidelines, usage instructions, and workflows.


Features
Trilingual alignment: Sundanese ↔ Indonesian ↔ English at the verse and sentence levels.
Quality flags: High / Medium / Low reliability metadata for each aligned unit.
Preprocessing pipeline: Scripts for normalization, segmentation, and tokenization.
Reproducibility package: Example workflows for SMT (Moses) and NMT (Fairseq).

Getting Started

Clone the repository:
git clone https://github.com/setiawanirwan/BibTri-Align.git
cd BibTri-Align


Explore the corpus (CSV):
import pandas as pd
df = pd.read_csv("data/su_id_en_parallel.csv")
print(df.head())


Train a baseline MT system (example using Fairseq):
bash scripts/evaluation/train_nmt.sh


Detailed usage is provided in docs/GETTING_STARTED.md

Documentation
ANNOTATION_GUIDELINES.md
 – Alignment flagging scheme with examples.
GETTING_STARTED.md
 – Step-by-step usage guide.
WORKFLOWS.md
 – Example MT workflows (filtering, weighting).
CONTRIBUTING.md
 – How to report issues or suggest improvements.

License
Corpus: Released under CC BY-SA 4.0
Code: Released under the MIT License

Citation
If you use BibTri-Align v2 in your research, please cite:

