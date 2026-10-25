> 公开阅读副本：仅用于理解原稿的历史来源与协议差异；相关私有定位信息已移除。文中“本次”“已核验”“计划”等均指原文记录时点，不代表本次上传或新的工作授权。出现状态冲突时先对照 ../main.tex 与 ../../docs/KNOWN_DIFFERENCES.md。

# PHEME Comparison Metrics Audit

This file records the provenance and aggregation rules for the PHEME comparison
table in `main.tex`. It is an internal reproducibility note and is not part of
the submitted paper.

## Archived result sources (logical identifiers)

- Author-protocol comparison runs:
  `PRIVATE_PHEME_BASELINE_ARCHIVE`
- UMER (the finalized model) five-fold run:
  `PRIVATE_UMER_PHEME_ARCHIVE`
- Fixed test-fold class supports:
  - folds 1--3: 805 non-rumor and 480 rumor events;
  - folds 4--5: 804 non-rumor and 481 rumor events.
- Label mapping: `0 = non-rumor`, `1 = rumor`.

All nine comparison methods have five completed fold result files: SVM-TS,
DLSTM, Bi-GCN, RAGCL, PAGCN, TGA-CMF, ADAAT-FGM, RRD-N, and MST.

## Metric construction

For each class, the paper reports Precision, Recall, and F1. It also reports one
overall Accuracy column. A separate class-specific Accuracy column is omitted
because it is redundant for binary one-versus-rest evaluation: its usual
definition equals overall Accuracy, while accuracy restricted to examples of
one class equals that class's Recall.

Metrics are computed on each fixed test fold first and then averaged
arithmetically over the five folds. The stored result JSON files provide
Accuracy and rumor F1 but do not retain full confusion matrices. For each fold,
the integer binary confusion matrix was recovered exactly from:

1. the known rumor and non-rumor supports;
2. the stored overall Accuracy; and
3. the stored rumor F1.

The recovered integer counts reproduce the stored metrics at their full saved
precision. RAGCL is a special case: its released protocol reports the average
of the last ten test epochs. Therefore, the confusion matrix was recovered for
each of those ten epochs from `history.json`; class metrics were averaged
across those epochs within a fold and then across folds.

## Five-fold means used in the paper

| Method | Rumor P | Rumor R | Rumor F1 | Non-rumor P | Non-rumor R | Non-rumor F1 | Accuracy |
|---|---:|---:|---:|---:|---:|---:|---:|
| SVM-TS | 0.4829 | 0.4430 | 0.4620 | 0.6830 | 0.7166 | 0.6994 | 0.6143 |
| DLSTM | 0.4147 | 0.4218 | 0.3870 | 0.6636 | 0.6557 | 0.6450 | 0.5682 |
| Bi-GCN | 0.8390 | 0.7589 | 0.7961 | 0.8642 | 0.9122 | 0.8873 | 0.8549 |
| RAGCL | 0.7291 | 0.7276 | 0.7272 | 0.8380 | 0.8371 | 0.8370 | 0.7961 |
| PAGCN | 0.7734 | 0.6173 | 0.6528 | 0.8053 | 0.8832 | 0.8383 | 0.7838 |
| TGA-CMF | 0.6840 | 0.6653 | 0.6727 | 0.8039 | 0.8146 | 0.8085 | 0.7588 |
| ADAAT-FGM | 0.7742 | 0.7090 | 0.7371 | 0.8357 | 0.8730 | 0.8528 | 0.8117 |
| RRD-N | 0.8357 | 0.7919 | 0.8119 | 0.8803 | 0.9061 | 0.8926 | 0.8633 |
| MST | 0.8620 | 0.7760 | 0.8161 | 0.8738 | 0.9247 | 0.8983 | 0.8691 |
| UMER | 0.8560 | 0.8784 | 0.8666 | 0.9264 | 0.9110 | 0.9185 | 0.8988 |

## Protocol qualifications

- Bi-GCN, RAGCL, and RRD-N follow released author protocols that inspect the
  held-out test fold during training or model selection. Their table rows are
  marked with a dagger and must not be described as leakage-free estimates.
- The released MST preprocessing excludes source-only events because it cannot
  construct their propagation graphs. Its row is marked with a double dagger
  and is evaluated on the eligible subset of each fixed test fold.
- All other reproduced systems retain the complete fixed test folds.

The strongest reproduced baseline by overall Accuracy is MST (0.8691). UMER
reaches 0.8988, an absolute gain of 0.0297, i.e., 2.97 percentage points.
