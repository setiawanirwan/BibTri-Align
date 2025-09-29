Example Workflows for BibTri-Align

This document provides example workflows for using the BibTri-Align v2 corpus. Each workflow demonstrates a typical use case, from basic filtering to weighted training and curriculum learning.

1. Filtering by Quality Flags

Researchers may want to exclude noisy alignments.

import pandas as pd

df = pd.read_csv("data/su_id_en_parallel.csv")

# Keep only High-confidence alignments
filtered = df[df['flag'] == '✓']

filtered.to_csv("data/su_id_en_high.csv", index=False)
print(f"Filtered size: {len(filtered)} sentences")


Result: A cleaner subset for MT training.

2. Weighted Training

Instead of discarding Medium alignments, we can assign weights.

def assign_weight(flag):
    if flag == '✓':
        return 1.0
    elif flag == '~':
        return 0.5
    else:
        return 0.0

df['weight'] = df['flag'].apply(assign_weight)

# Save weighted training file
df[['su_text','id_text','weight']].to_csv("data/su_id_weighted.csv", index=False)


Fairseq example (using weights):

fairseq-train data-bin \
  --task translation \
  --source-lang su --target-lang id \
  --criterion label_smoothed_cross_entropy \
  --sentence-avg --update-freq 2 \
  --train-subset train --valid-subset valid \
  --sample-break-mode none \
  --loss-weight-file data/su_id_weighted.csv

3. Curriculum Learning

Start training on High, then gradually include Medium.

# Phase 1: High only
bash scripts/evaluation/train_nmt.sh su en data/su_id_en_high.csv

# Phase 2: High + Medium
bash scripts/evaluation/train_nmt.sh su en data/su_id_en_high_medium.csv --restore-file checkpoint_phase1.pt


This strategy helps the model learn from clean data first, then adapt to noisier examples.

4. Error Analysis with Flags

Flags can also guide linguistic analysis.

low_cases = df[df['flag'] == '✗']

# Inspect problematic alignments
print(low_cases[['su_text','id_text','en_text']].head(10))


Applications:

Identify missing verses in Sundanese.

Examine morphological errors.

Study where cultural/lexical gaps appear.

5. Baseline MT Evaluation

Example script (already included in scripts/evaluation/):

bash scripts/evaluation/run_baseline.sh su id


This runs SMT and NMT on Sundanese→Indonesian with three settings:

Unfiltered

Filtered (High only)

Weighted (High + Medium)

Results (BLEU/ChrF/COMET) are saved in results/.

6. Extending to Other Domains

The pipeline is modular and can be applied to other parallel texts:

python scripts/preprocessing/normalize.py new_data/su.txt new_data/id.txt
python scripts/alignment/run_fastalign.py new_data/su.txt new_data/id.txt


This ensures the resource can grow beyond scripture in future releases.
