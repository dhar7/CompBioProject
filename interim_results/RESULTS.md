# Interim results

Local run: 2,905 positive pairs, 83 peptides, five folds, three seeds, three epochs,
and five negatives per positive. Chance checks use 1,000 shuffles; bootstrap estimates use 200 samples.

## Negative construction

Frozen ESM-2 with an MLP. Scores are averaged over folds, then seeds. AP is average precision.

| Negatives | AUROC | AP |
|---|---|---|
| random pairing | 0.4999 | 0.1791 |
| background | 0.5608 | 0.2053 |
| p99 | 0.5613 | 0.2019 |
| p75 | 0.5541 | 0.2019 |
| p50 | 0.5394 | 0.1951 |
| p25 | 0.5224 | 0.1934 |
| p1 | 0.4981 | 0.1769 |

AUROC falls as negatives get harder. The 3-mer boosting check also falls: 0.5579 at p99 to 0.4691 at p1.
For random pairing and p1, peptide-only, MHC-only, and TCR-blind controls score 0.5000 AUROC.

## Shared benchmark

Released checkpoints on the same 16,192 supported pairs; mean scores over five folds.

| Predictor | AUROC | AP |
|---|---|---|
| epiTCR | 0.5048 | 0.1502 |
| TITAN | 0.5522 | 0.1907 |

The local negative-swap range is 0.0639 AUROC versus a predictor gap of 0.0473.
For AP, the range is 0.0221 versus a gap of 0.0404. This does not isolate an architecture effect.

## Notes

- Results are preliminary. GILGFVFTL is 73.4% of selected positives and the only peptide in one fold.
- The split holds out peptides; four positive TCRs cross folds. Negatives are assumed, and the background is one donor.
- Pretrained-model training overlap is not ruled out. Full settings and folding remain for Sol; 200 structural inputs are ready.

[Figures](figures/) · [Supporting files and original run](supporting/) · [Run settings](supporting/settings.txt)
