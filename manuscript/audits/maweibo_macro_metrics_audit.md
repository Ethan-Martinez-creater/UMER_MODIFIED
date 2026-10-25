> 公开阅读副本：仅用于理解原稿的历史来源与协议差异；相关私有定位信息已移除。文中“本次”“已核验”“计划”等均指原文记录时点，不代表本次上传或新的工作授权。出现状态冲突时先对照 ../main.tex 与 ../../docs/KNOWN_DIFFERENCES.md。

# Ma-Weibo macro-metric audit

## Reporting rule

- Accuracy is reported once for binary classification.
- Precision, Recall, and F1 are computed for rumor and non-rumor separately,
  then macro-averaged across the two labels within each test fold.
- The reported number is the arithmetic mean of the five fixed outer folds.
- RRD-N uses the three completed folds and is excluded from five-fold rankings.

## Recovery from archived results

The archived result JSON files contain Accuracy, Macro-F1, and Rumor-F1 but do
not directly contain Macro-Precision or Macro-Recall. The fixed Ma-Weibo folds
have label-0/label-1 supports `(471,462)`, `(470,463)`, `(470,463)`,
`(470,463)`, and `(470,462)`. For each fold, Accuracy fixes the total number of
errors and Rumor-F1 fixes the rumor true-positive count, which uniquely
recovers the binary confusion matrix. The reproducible implementation is:

`original_model_optimization/analysis/recompute_maweibo_macro_pr.py`

RAGCL follows its archived author protocol: each of the final ten epoch-level
test metric records is recovered first, and the resulting macro metrics are
then averaged in the same order. This avoids treating a nonlinear metric of
averaged values as an averaged metric.

## Values used in Table 5

| Method | Accuracy | Macro-P | Macro-R | Macro-F1 | Folds |
|---|---:|---:|---:|---:|---:|
| SVM-TS | 0.7706 | 0.7714 | 0.7704 | 0.7703 | 5 |
| DLSTM | 0.5967 | 0.5984 | 0.5969 | 0.5950 | 5 |
| Bi-GCN | 0.8986 | 0.8989 | 0.8985 | 0.8985 | 5 |
| RAGCL | 0.9117 | 0.9195 | 0.9116 | 0.9109 | 5 |
| PAGCN | 0.9569 | 0.9570 | 0.9570 | 0.9569 | 5 |
| TGA-CMF | 0.9031 | 0.9062 | 0.9034 | 0.9029 | 5 |
| ADAAT-FGM | 0.9443 | 0.9448 | 0.9444 | 0.9442 | 5 |
| RRD-N | 0.9093 | 0.9094 | 0.9093 | 0.9092 | 3 |
| MST | 0.9325 | 0.9345 | 0.9327 | 0.9324 | 5 |
| UMER | 0.9689 | 0.9698 | 0.9691 | 0.9689 | 5 |

Archived result source (logical identifier):

`PRIVATE_MAWEIBO_BASELINE_ARCHIVE`

RRD-N Fold 1--3 recovered confusion matrices are respectively
`TP/FN/FP/TN = 425/37/48/423`, `424/39/37/433`, and
`424/39/54/416`. Their unrounded three-fold means are Accuracy
`0.9092533`, Macro-P `0.9094188`, Macro-R `0.9093198`, and Macro-F1
`0.9092482`.
