1. Download and Install

Clone the repository:

git clone https://github.com/setiawanirwan/BibTri-Align.git
cd BibTri-Align


Dependencies (Python 3.8+):

pip install -r requirements.txt


Main packages used:

pandas (data handling)

regex (normalization and entity checks)

fairseq (neural MT training)

mosesdecoder + kenlm (phrase-based SMT)

2. Explore the Data

The main corpus is stored in CSV and JSONL formats. Each row contains aligned text in Sundanese (su), Indonesian (id), and English (en), with a quality flag.

import pandas as pd

df = pd.read_csv("data/su_id_en_parallel.csv")
print(df.head())


Sample output:

su_text	id_text	en_text	flag
"gusti teh pangpangna asih ..."	"tuhan itu penuh kasih ..."	"the lord is merciful ..."	✓

Flags:

✓ = High confidence

~ = Medium confidence

✗ = Low confidence

3. Filtering by Quality Flags

Example: keep only High and Medium alignments.

filtered = df[df['flag'].isin(['✓', '~'])]
print(len(filtered))


Save to a new file:

filtered.to_csv("data/su_id_en_filtered.csv", index=False)

4. Training Baseline SMT (Moses)

Example workflow (scripts provided in scripts/evaluation/).

bash scripts/evaluation/train_smt.sh su id data/su_id_en_filtered.csv


Outputs:

Phrase tables

Language model

BLEU scores on dev/test sets

5. Training Baseline NMT (Fairseq)

Preprocess and train:

bash scripts/evaluation/train_nmt.sh su en data/su_id_en_filtered.csv


Evaluate with BLEU and ChrF:

bash scripts/evaluation/eval_nmt.sh su en

6. Example Jupyter Demo

Open the demo notebook:

jupyter notebook examples/notebook_demo.ipynb


The notebook shows how to:

Load the dataset

Filter by flags

Visualize length ratios

Run a quick MT baseline

7. Next Steps

See docs/WORKFLOWS.md
 for example pipelines (filtering, weighting).

See docs/ANNOTATION_GUIDELINES.md
 for details on alignment flags.

Contributions welcome – see docs/CONTRIBUTING.md
.
