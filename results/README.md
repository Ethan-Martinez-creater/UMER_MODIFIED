# 正式结果的聚合证据

这里保存六份原有 summary JSON 的数值副本：PHEME、Ma-Weibo 正式模型，以及 PHEME no_text/no_graph/no_memory/no_consistency 四项消融。保留逐折聚合指标、五折均值、标准差和原有字段；只规范文本换行。

没有逐事件预测、帖子、事件标识、标签清单、文件系统定位信息或模型文件。本次没有重新训练、推理或重算全部指标。可以用这些文件核对报告数字，不能据此宣称已经复现整个实验。

- [PHEME](pheme_summary.json)
- [Ma-Weibo](maweibo_summary.json)
- [PHEME 四项消融](pheme_ablation/)

文稿中 no-SAM 的 0.8951 Accuracy 来自既有文稿/实验记录，本次没有另导入其独立 summary 文件。
Ma-Weibo Macro-P/R 看 [配套审计](../manuscript/audits/maweibo_macro_metrics_audit.md)，不在上述 summary 字段中。

`target_strictly_greater_than` 和 `all_mean_metrics_strictly_exceed_target` 是原文件保留的历史筛查字段，不是这次讨论新设的接受门槛，也不代表对 UMER 工作整体作 GO/NO_GO 判决。

来源、导入处理与 SHA256 见 [SOURCE_MANIFEST.json](../SOURCE_MANIFEST.json)。模型对比的协议限定另见 [原稿审计](../manuscript/audits/)。
