# 检索与阅读记录：codex_local / R1

日期：2026-10-25。背景 commit：`d71e5b7595deba3a6e7cbc53e8cc98d1b6944334`。本记录是实际查询和阅读范围的人工整理，不是原始工具日志，也不包含凭据、原始帖子或私有定位信息。

## 1. 检索策略与独立性

先从共享源码中的截断、多视图 JSD、融合和随机五折出发，检索观察预算、source 依赖、泛化和早期决策。候选在检索中收敛为报告的 A/B/C，没有预选论文后倒造 UMER 的失败现象。

使用当前会话的网页搜索/打开/文本定位工具，以及 GitHub 连接器对作者仓库的只读查询。没有安装检索工具、使用额外推理 API、运行模型、下载数据/权重或联系作者。未调用子代理；未读取另外两位参与者的报告、PR 或讨论意见。没有列举目标仓库的其他 PR 来寻找候选。

检索结果出现的综述、ResearchGate、聚合站和无关网页不作为方法判断来源。关键论断以已经打开的原始论文/正式出版页为据。全文读取失败的资料仅记作待核线索。

## 2. 实际搜索词

下表按发起批次记录原始查询；不是声称检索穷尽。域限制只在注明的一批使用。

| 批次 | 查询 | 主要作用 |
| --- | --- | --- |
| S1 | `rumor detection source bias shortcut topic generalization graph text debiasing 2024 2025 2026` | 初筛泛化与 source 依赖 |
| S1 | `early rumor detection evidence sufficiency adaptive stopping uncertainty 2024 2025 2026` | 初筛早期判断已有机制 |
| S1 | `rumor detection reply redundancy noise counterfactual graph text 2025 2026` | 初筛回复噪声、选择和反事实已有机制 |
| S2 | `rumor detection debiasing source text bias domain generalization` | 限 ACL/arXiv/AAAI，定位原始论文 |
| S2 | `rumor detection early stopping uncertainty evidence sufficiency` | 同上，定位 HEARD 等 |
| S2 | `rumor detection cross view consistency information loss reply selection long conversation` | 同上，定位直接视图近邻 |
| S3 | `rumor detection "consistency" "views" evidence information` | 区分图对比、文本一致性和多模态核验 |
| S3 | `rumor detection informative replies selection token budget conversation text` | 定位 FoRM 与相关筛选工作 |
| S3 | `rumor detection "source" "bias" "debias" 2025 2026` | 补新近泛化方法 |
| S3 | `rumor detection early detection 2026 non LLM adaptive stopping` | 补新近早期方法；没有将排除 LLM 当成新颖性 |
| S4 | `rumor detection multi view consistency incomplete views selection RAGCL Focal Reasoning DCE` | 找强直接比较对象 |
| S4 | `rumor detection "source post" "bias" disentangle 2024 2025` | 查 source/上下文分工近邻 |
| S4 | `rumor detection "information loss" "truncation"` | 查截断条件已有表述 |
| S4 | `rumor detection "consistency" "complementary" 2025 2026` | 查一致性与互补性结合 |
| S5 | `"Propagation Tree Is Not Deep" arxiv code` | 查 RAGCL 正文与作者实现 |
| S5 | `"R-Drop" "Regularized Dropout" arxiv` | 查原目标与对照 |
| S5 | `"What Makes for Good Views" contrastive learning NeurIPS 2020` | 核视图信息保留原则 |
| S5 | `"multi-view" "rumor" "consistency" -multimodal -image -LLM` | 尝试收紧文本会话对象；未据少结果宣称空白 |
| S6 | `"rumor detection" "consistency regularization" 2025 2026` | 补最新一致性相关 |
| S6 | `"rumor detection" "partial" "view" consistency` | 查部分观察邻近 |
| S6 | `"rumor detection" "truncation" "consistency"` | 查 token 截断与一致性重合 |
| S6 | `"rumor detection" "observation" "consistency"` | 找到 limited-observation screening 和 SCSNet 等线索 |
| S7 | `"Focusing on Relevant Responses for Multi-modal Rumor Detection" TKDE 2024 DOI` | 追查版本与正式发表信息；访问受限详见下表 |
| S7 | `"observation" "consistency" "rumor" 2026 token serialization` | 进一步收紧 A 的对象，未据结果断言首次 |
| S8 | `"Don’t Take the Easy Way Out" "Ensemble" ACL` | 查偏置专家思想的直接前作 |
| S8 | `"Learning Beyond Domains" "GenPromptCL" AAAI 2026` | 核新近文本域泛化正式来源 |

## 3. 阅读深度与访问限制

具体链接和已读节号见 [evidence_matrix.md](evidence_matrix.md)。

- 方法段落实际阅读：R-Drop、InfoMin、RAGCL、DCE-RD、FoRM（arXiv版）、Mu 等静态数据分析、FIRM、GCML（范围有限）、HEARD、SCSNet。
- 正式页面/摘要筛查：Clark 2019、GenPromptCL 2026、Yesterday’s News 2026；EASE 的 arXiv 摘要与目录。
- 没有将“打开 PDF”一概标成精读整篇；部分页有复杂公式和图，未完成逐式/视觉审计。没有把阅读与复现混写。

| 访问项 | 实际结果 | 处理 |
| --- | --- | --- |
| FoRM 作者终版 PDF | 打开超时；搜索索引可见 TKDE DOI | 使用实际可读 arXiv 方法段，标明版本限制 |
| FoRM DOI `10.1109/TKDE.2024.3389694` | 工具返回不可访问 | 不据此声称核完正式终版 |
| Electronics 15(15),3330 limited-observation 2026 | 搜索预览可读，全文打开 429 | 只列潜在重合，不据摘要推断公式 |
| RAGCL 年份 | 正式 AAAI 页面为 2024，arXiv 上载时间为 2025 | 按正式发表年份记录，避免误作新方法 |
| EASE 论文页 | arXiv v1 页仍有模板会议/DOI 占位 | 只按已读预印本处理 |
| SCSNet 公开可复现材料 | Data availability 为向作者索取；本页未检出 code | 不联系作者，不声称立即可复现 |
| BEARD 补充材料 | HEARD README 列树与时间入口；embedding 标记不再直接下载 | 未下载，不能保证文本/embedding 或完整数据即刻可用 |

## 4. 作者实现的定向核查

只读以下四个论文指向的仓库元数据与 README，不克隆、不读取 Issue/PR 或第三方讨论：
- [dropreg/R-Drop](https://github.com/dropreg/R-Drop)：README blob `054fb72bcfe1e65155389b2bb7b8a13924407c23`。
- [CcQunResearch/RAGCL](https://github.com/CcQunResearch/RAGCL)：README blob `e030965fc0be3685a7d993aa463478c7f7a0d899`。
- [Vicinity111/DCE-RD](https://github.com/Vicinity111/DCE-RD)：README blob `3258751f984674628acf07d1b9c0b197bdfb6387`。
- [znhy1024/HEARD](https://github.com/znhy1024/HEARD)：README blob `6ea24b72941b131ab6af08ea15031b09e0094fa9`。

上述 blob 用于定位此次实际读取的版本，不代表锁定了第三方完整实验。README 出现的安装与训练命令没有执行，外部数据链接没有下载。

## 5. 共享材料复查与未做事项

本会话已完整读过现稿并读过架构、实验、六份聚合 JSON 与配套审计；本轮定向复查编码/视图、JSD、门控/残差和参数互斥逻辑。只使用共同背景可定位事实。没有从旧研究目录新增读取动态产物来猜测进展。

没有：
- 检查新的帖子、事件级错误、模型权重或预测；
- 执行 P0/P1、Tokenizer 审计、梯度分析、早期切片或跨话题划分；
- 读取、评论或评判另两份独立报告；
- 将旧 baseline 数值与新近论文表格直接排列后宣称超越；
- 更改科学实现、论文、历史结果或 SOURCE_MANIFEST 的背景快照。

## 6. 尚缺的信息

A 尚缺实际 tokenizer 暴露映射和错误/训练信号；B 尚缺 UMER 的独立新话题诊断与可靠主题/主张分组；C 尚缺全部分支的历史可见性审计与可用早期数据。所有候选都缺新实验验证。

自适应一致性、部分视图学习及相关多模态工作没有完全穷尽。如果第二轮支持 A，需进一步精查其机制等价性；不能用本轮没有搜到完全同名方法来代替新颖性评估。

本轮文档发布前只进行隐私、链接与范围检查，不进行模型测试。发布后以 PR head commit 固定 R1 版本；后续更正和回应另行保留，不覆盖独立判断。
