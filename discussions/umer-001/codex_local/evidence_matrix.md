# 文献与本地证据矩阵

参与者：`codex_local`；检索与核对日期：2026-10-25；背景 commit：`d71e5b7595deba3a6e7cbc53e8cc98d1b6944334`。这是第一轮独立材料，没有阅读另外两方交付。

“方法已读”指实际打开并阅读下面列出的原文段落，不代表整篇复现。只依赖原始论文、正式出版页与论文指向的作者仓库；搜索结果中的聚合站、综述或二手解读不作为技术判断证据。

## 1. 首选 A 的关键近邻

| ID / 来源 | 身份、实际阅读 | 已有机制与本项目边界 | 资源和协议核查 |
| --- | --- | --- | --- |
| A1 [R-Drop: Regularized Dropout for Neural Networks](https://papers.neurips.cc/paper_files/paper/2021/file/5a66b9200f29ac3fa0ae244cc2a51b39-Paper.pdf) | NeurIPS 2021；§2.1–2.2、公式(1)–(4)；非全篇逐段精读 | 相同输入双 dropout 的监督与双向 KL 已有；A 必须区别信息可见性变化，不能将双前向一致性当贡献 | [作者仓库](https://github.com/dropreg/R-Drop)元数据及 README 已读（README blob `054fb72b`），含通用 KL 示例；未运行 |
| A2 [What Makes for Good Views for Contrastive Learning?](https://proceedings.neurips.cc/paper/2020/file/4c2e5eaae9152079b9e95845750bb9ab-Paper.pdf) | NeurIPS 2020；§3.1–3.3、Proposition 3.1 前后；未审计附录证明 | 保留任务信息与减少无关信息的视图原则已有；论文的对比学习条件不能直接证明监督 JSD 在 UMER 有害 | 视觉任务为主，与会话二分类不同；本轮未核验其完整代码/数据入口 |
| A3 [Propagation Tree Is Not Deep: Adaptive Graph Contrastive Learning Approach for Rumor Detection](https://ojs.aaai.org/index.php/AAAI/article/view/27757)；[已读方法正文](https://arxiv.org/html/2508.07201) | 正式 AAAI 2024，出版页核验；arXiv 上载为 2025，不能误写成新 2025 方法；读 Analysis、Method、增强与对比目标、实验设置 | 已有传播树中心性指导的视图增强；A 不是“首次保护关键回复”，需比较不同的预测一致性条件 | [RAGCL](https://github.com/CcQunResearch/RAGCL) README 已读（`e030965f`）：需先算中心性，数据为外部链接，未下载/核完整性；原文实验协议不能直接与 UMER 同等比较 |
| A4 [Rumor Detection with Diverse Counterfactual Evidence](https://arxiv.org/html/2307.09296) | KDD 2023 元数据见原文页；§3.2–3.4、Algorithm 1–2、损失与实验设置已读 | GATv2、Top-K 子图、补图、多样性及聚合已有；补图目标与标签翻转假设不等于实际世界干预后的真值 | [DCE-RD](https://github.com/Vicinity111/DCE-RD) README 实际仅一句数据发布限制（`3258751f`）；未审计实现树，不能宣称仓库就是可运行复现包 |
| A5 [Focusing on Relevant Responses for Multi-modal Rumor Detection](https://arxiv.org/html/2306.11746) | 已读 arXiv 2023 v1：§IV-B–D、V-A；作者终版 PDF 请求超时，正式 DOI 打开失败，故不声称读过 TKDE 终版 | 标签监督的粗筛 top-k 与细粒度关系推理已有；直接换成“重要回复选择”不足。A 当前关注截断后观察条件，而非相关性排序 | 原文是含图像的 Twitter15/16 四分类并过滤重复转发；不可与 PHEME 6,425 事件直接比表。数据引用入口已定位，未读完整数据；模型代码入口未独立确认 |

A1/A2/A3 是理论/目标/视图构造的核心比较；A4/A5 防止把“多样性、证据选择”换名包装。它们并不共同证明 A 已经新颖或有效。

## 2. 备选 B 的直接约束

| ID / 来源 | 身份、实际阅读 | 已有内容与边界 | 资源/可比性 |
| --- | --- | --- | --- |
| B1 [Examining the Limitations of Computational Rumor Detection Models Trained on Static Datasets](https://aclanthology.org/2024.lrec-main.595.pdf) | LREC-COLING 2024；§4.1、5.1–5.4，重点 source removal 与相似度分析 | 数据切分、源帖依赖与时间变化已有系统分析。为诊断提供动机，不能把其结论数值直接搬到 UMER | 包含其他版本数据和模型；本轮没有核验其完整代码入口或重复运行 |
| B2 [Equal Truth: Rumor Detection with Invariant Group Fairness](https://aclanthology.org/2025.findings-emnlp.584.pdf) | Findings EMNLP 2025；§2.1–2.2、§3.1 数据/评估范围 | FIRM 已学习动态困难分组并做不变学习；加 group loss 不构成新空白。分组公平也不能自动等同于因果正确 | FineFake/Weibo21/MCFEND 等语料与当前事件图不相同；正文检索未见直接 GitHub 链接，不断言不存在代码 |
| B3 [GCML: Gradient Coherence Guided Meta-Learning for Cross-Domain Emerging Topic Rumor Detection](https://aclanthology.org/2025.emnlp-main.968.pdf) | EMNLP 2025；§3、§4.1–4.2，并阅读概要中 meta-update 说明；§4.3 未逐式核完 | 已使用目标少量标签、任务梯度一般化分数和元更新；不是无目标样本的域泛化，不可混作公平对照 | 是否能在现有事件图设置直接重现尚未核验；本轮未核完整代码/数据 |
| B4 [Don’t Take the Easy Way Out: Ensemble Based Methods for Avoiding Known Dataset Biases](https://aclanthology.org/D19-1418/) | EMNLP-IJCNLP 2019；正式页面与摘要已读，**方法全文未精读** | 偏置专家与稳健专家组合的基本思想已有；仅提出 source-only 专家不能称新颖 | 不是谣言专用方法。若 B 被选，需补读公式及公平移植条件 |
| B5 [Learning Beyond Domains: Misleading Prompts and Pseudo-Label Contrast for Text Domain Generalization](https://ojs.aaai.org/index.php/AAAI/article/view/40436) | AAAI 2026，正式出版页核验；**本轮仅读摘要** | 域误导 prompt 与伪标签对比已用于含谣言任务的文本泛化；这里只用于确认相关空间拥挤，不宣称公式等价 | 原文/作者 PDF 与代码检索入口定位到，未进一步读取、安装或运行 |
| B6 [Yesterday’s News: Benchmarking Multi-Dimensional Out-of-Distribution Generalization of Misinformation Detection Models](https://aclanthology.org/2026.cl-2.6/) | Computational Linguistics 52(2), June 2026；**正式页面摘要与元数据** | 已区分时间、事件、话题、发布者等多种泛化轴；不能把“多轴 OOD 评估”本身当新任务 | distant labeling 的新闻基准；不是现有社交会话数据的替代物，未下载 |

## 3. 暂缓 C 的直接约束

| ID / 来源 | 身份、实际阅读 | 已有内容与边界 | 资源/可比性 |
| --- | --- | --- | --- |
| C1 [Early Rumor Detection Using Neural Hawkes Process with a New Benchmark Dataset](https://aclanthology.org/2022.naacl-main.302.pdf) | NAACL 2022；§2、4–5.2 关键段落、§6 指标及 source bias 讨论；未逐式审计全部 Hawkes 推导 | 预测翻转建模与自动停止已存在；先验数据的早期覆盖也已受质疑，不能只裁历史数据即宣称真实早期有效 | [HEARD](https://github.com/znhy1024/HEARD) README 已读（`6ea24b72`）；列树/时间补充，但 embedding 标记不再直接下载。PHEME 版本 5,802 条，非当前 6,425；未核数据实际可得性 |
| C2 [Early detection of online public opinion rumors for cross-event generalization](https://link.springer.com/article/10.1007/s44163-026-02227-7) | Discover AI，2026-09-18；SCSNet §3.1–3.3、§4.3 说明与 Data availability 已读；非完整复现实验 | 回复贡献、stage 组织、线性状态与更新门，以及稳定性/新信息权衡已有。不能把“状态随新证据更新”概括成空白 | 数据声明 upon request，页内未检出 code 链接；未联系作者/下载。论文结果不与 UMER 随机五折直接比数值 |
| C3 [Structure-Aware Propagation Graph Learning for Platform-Side Rumor Risk Screening Under Limited Observation](https://www.mdpi.com/2079-9292/15/15/3330) | Electronics，检索预览给出 2026-07-28；**打开全文 429，未读方法全文** | 预览涉及多节点观察规模、重复评分和单检查点。只作为必须补查的潜在重合，不据预览评价其正确性或等价性 | 代码与数据未核验；不复述其指标作为比较依据 |

## 4. 额外筛查而未纳入主机制判断

- [EASE: Towards Real-Time Fake News Detection under Evidence Scarcity](https://arxiv.org/html/2510.11277)：打开 arXiv 2025 v1，阅读摘要和目录；依赖多类评价与 LLM 知识，超出本轮主线。页面还保留模板会议占位，不据此声称正式发表。
- KPG（WWW 2025）作者机构页面显示图生成与关键子结构选择；本轮仅筛查摘要，未将其方法公式作为结论依据。若发展回复选择机制需补读。
- 2026 的 SAFE-MR、若干多模态外部证据/LLM 方法只作为检索线索，未据摘要宣布与 A 重合或无关；本轮没有完整覆盖这批新工作。

## 5. 源码定位补充

背景 commit 下的公开文件链接：
- [JointEventDataset.encode / __getitem__](../../../reference_code/round_013_joint_trifusion/run_fold.py#L127)：分别截断和取视图。
- [训练正则](../../../reference_code/round_013_joint_trifusion/run_fold.py#L981)与[JSD](../../../reference_code/regularization.py#L6)：无观察重叠条件。
- [门控/残差变体](../../../reference_code/round_013_joint_trifusion/model.py#L30)：已存在。
- [参数互斥](../../../reference_code/round_013_joint_trifusion/run_fold.py#L504)：SAM、R-Drop、Group DRO 的组合有禁止条件；代码钩子不是新方案也不是运行结果。
- [正式消融](../../../docs/UMER_EXPERIMENTS.md#L39)：原一致性总体有益，是 A 必须面对的反证约束。

本轮没有把第三方论文中的真假标签、stance、证据充分性和本项目 rumor/non-rumor 当同一个 contract。
