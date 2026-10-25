# 英文论文文本快照

导入日期：2026-10-25。该目录提供现有英文稿的完整文本，以便网页智能体阅读；本次没有改进、审稿或编译论文。

- [main.tex](main.tex)：既有全文，含引言、相关工作、方法、实验、结论与伦理。
- [references.bib](references.bib)：既有参考文献；没有在此次上传中重新查证全部文献。
- [参考资料审计](audits/reference_audit.md)：历史查阅记录，可能含过时的写作状态或会议信息。
- [PHEME 对比审计](audits/pheme_comparison_metrics_audit.md)：指标构造及基线协议限定。
- [Ma-Weibo 指标审计](audits/maweibo_macro_metrics_audit.md)：宏平均恢复与不完整折说明。

## 阅读注意

原稿正文和 bibliography 只规范文本换行；审计副本移除了私有来源位置和部署措辞，并增加历史范围标记。具体处理与校验值见 [来源清单](../SOURCE_MANIFEST.json)。

此处不包含编译后的 PDF、图片、模板类文件或参考论文 PDF，因此不是独立可编译的 LaTeX 工程。main.tex 中的相对图文件与模板引用保留原样供理解，不能据此认定附件已上传。当前模型图解可先依据 [架构说明](../docs/UMER_MODEL_ARCHITECTURE.md) 理解。

原目录名和 TeX 会议元数据仅反映历史写作模板，不代表已决定投稿场所或确认当前会议日期、格式要求、截止时间。背景阅读中已发现的表述差异见 [KNOWN_DIFFERENCES](../docs/KNOWN_DIFFERENCES.md)。
