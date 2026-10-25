# UMER-001 / R1 文献检索与筛选记录（chatgpt_web）

> **检索执行日期：2026-10-25**；公共背景固定 commit `d71e5b7595deba3a6e7cbc53e8cc98d1b6944334`。参与者 `chatgpt_web`，自报 GPT-6。使用联网公开搜索、正式出版页面/公开 PDF、ACL Anthology、AAAI、NeurIPS、Springer、部分 ScienceDirect 页面以及共享 GitHub 源码，**未使用付费 API、未下载模型或数据、不执行模型推理与训练**。本轮没有接触其他参与者的第一轮报告、评论或 PR；不借用他方检索词/结论。

## 1. 问题驱动的检索设计

根据共同材料而非其他参与者先选三类检索轴：

- **Q-A（首选）**：多条回复在 256-token 内的可见性、样本内不同 serialization/selection 对一致性损失的影响；关注 view agreement 是否默认观测相同信息，区分 dropout 噪声和输入内容不一致。
- **Q-B（备选）**：PHEME 跨话题留出、跨事件低样本适应、语义近邻标签适用域/召回置信度，排除“训练库标签就是事实证据”的混用。
- **Q-C（比较但暂缓）**：事件传播的早期窗口、回复贡献与时间状态机制，检验是否已存在直接工作。

**检索范围**：基础工作不设发表下限，重点查 2021–2026 和最新截至 2026-10-25 的直接方法近邻。英语关键字与题名交叉查找；先扫摘要/方法标题，再打开论文原文的机制和实验相关部分。检索引擎/来源不构成严格系统综述；**不虚构总命中量、自动去重数量、全文阅读篇数或覆盖率**。

## 2. 实际使用的检索字符串（英文原样）

| 编号 | 搜索式 | 初步目的 | 处理结果 / 排除要点 |
| --- | --- | --- | --- |
| Q01 | `rumor detection truncated replies input selection conversation multiple views consistency rumor detection 2023 2024 2025 paper` | A：文本截断与视图一致性 | 接入一致性近邻 R-Drop / 事件增强，发现没有现成证据证明 UMER 截断失效 |
| Q02 | `rumor detection incomplete propagation early stage observation reply sparse reliable fusion uncertainty adaptive 2023 2025 paper` | A/C：回复稀疏、时序/早期 | 转向 SCSNet、SWAM；不将“未观察”与“噪声”直接等价 |
| Q03 | `social media rumor detection temporal semantic adaptive comment selection claim guided attention 2024 2025` | A/C：贡献分配/回复筛选 | RAGCL、分阶段权重；普通注意力/筛选不能自称创新 |
| Q04 | `rumor detection dataset topic event split leakage PHEME cross-event generalization random split 2024 2025` | B：分布协议 | 定位话题留出与 PHEME 事件级随机五折的评估差异 |
| Q05 | `rumour detection PHEME stance source reply attention selection veracity 2023 2024 ACL` | A：有信息回复/立场 | 检索到 stance 文献，但标签任务不同，不当成 UMER 的同任务基线 |
| Q06 | `social media rumor detection evidence disagreement modality reliability adaptive multimodal noisy fusion` | A/B：证据冲突、可靠性 | 大量多模态/跨模态方法，图文事件机制不对齐；且 UMER 本身已有 gated 变体 |
| Q07 | `rumor detection comment selection key posts misinformation detection hierarchical attention reply selection 2024 2025` | A：重要回复选择 | 与图注意力/关键帖子抽样相邻，不能仅换权重命名 |
| Q08 | `rumor detection incomplete conversation view truncation reply sampling information budget evidence selection 2025 paper` | A：信息预算 | 需要实际 tokenizer 覆盖而非直接从帖子数推损伤 |
| Q09 | `rumour verification conversational context selecting relevant replies evidence aggregation PHEME 2024 paper` | A：回复支持证据 | 排除外部事实验证/知识图谱等不同任务 |
| Q10 | `rumor detection adaptive fusion reliability uncertainty propagation text modalities 2024 2025 PHEME Weibo` | B：动态融合/可靠性 | 查公开机制并回对仓库已实现但未正式使用的 gate |
| Q11 | `RAGCL propagation tree is not deep adaptive graph contrastive learning rumor detection AAAI 2024` | A：直接强近邻 | 找到并阅读 AAAI 官方 PDF、方法/消融 |
| Q12 | `UMER rumor detection 2026 view consistency context redundancy nearest neighbor selective replies` | A/B：是否已有同名或近重复 | 不能以关键词缺失断言原创；回归具体对照 |
| Q13 | `A Metric-Learning Method for Few-Shot Cross-Event Rumor Detection 2023 paper neurocomputing full text` | B：强直接近邻 | 找到出版商元信息/公开可见摘要及节选，完整全文仍有限制 |
| Q14 | `Rumor Detection on Social Media with Event Augmentations 2021 SIGIR method uncertainty` | A：事件增强历史 | 核对公开出版元数据，未深读全文，保留待补核 |

另外通过已有共同稿的 `manuscript/main.tex` §2（Related Work）和 `manuscript/references.bib` 的论文题名、DOI 链接做**已有文献清单的独立原文核对**，而不是将原稿对该论文的描述视为结论。聚焦关键词组合包括 `cross-view consistency`、`dropout regularization`、`PHEME leave-one-event-out`、`cross-topic rumor detection`、`adaptive graph contrastive rumor`、`sliding window memory rumor detection`、`reply contribution stage rumor detection`。报告不会以“搜不到覆盖”作为首创证据。

## 3. 逐篇打开/阅读记录

| ID | 原文/页面 | 阅读与核对位置（2026-10-25） | 访问结论与限制 |
| --- | --- | --- | --- |
| P01 | R-Drop，NeurIPS 2021：[官方 PDF](https://proceedings.neurips.cc/paper_files/paper/2021/file/5a66b9200f29ac3fa0ae244cc2a51b39-Paper.pdf) | PDF §2.1–2.2（随机 dropout 双分布、bidirectional KL/目标），§3 分类/语言任务；查看相关 PDF 页面图文 | **原文可访问**；不是 PHEME 事件任务；未读作者完整代码 |
| P02 | RAGCL，AAAI 2024：[官方 PDF](https://ojs.aaai.org/index.php/AAAI/article/download/27757/27555) | PDF 方法（重要性/图节点边特征增强/对比，约 pp.75–77）、实验与 ablation（约 pp.77–79）；核对作者代码地址 [RAGCL](https://github.com/CcQunResearch/RAGCL) | **原文可访问**；只是定位代码链接，**未审仓库源码**；不同基准协议 |
| P03 | SCSNet，2026-09-18 Discover Artificial Intelligence：[Springer 开放全文](https://link.springer.com/article/10.1007/s44163-026-02227-7) | HTML 全文 §§3.1–3.4 的回复贡献、阶段状态更新，§§4.1–4.3 的跨话题与对照 | **方法/实验关键部分可访问**；不同分区，禁止数值横比 |
| P04 | SWAM，EMNLP 2025：[ACL PDF](https://aclanthology.org/2025.emnlp-main.729.pdf) | PDF §§3.3–3.5 时间滑窗/事件内 memory、§§4.1–4.4 实验及 early setting；查看重要示意/表格 | **原文可访问**；其 memory 不是 UMER 的跨事件标签库；作者代码未审 |
| P05 | Cross-Topic Rumor Detection using Topic-Mixtures，EACL 2021：[ACL PDF](https://aclanthology.org/2021.eacl-main.131.pdf) | PDF §§3–4，话题 mixture 构造、PHEME cross-topic/held-out 评估 | **原文可访问**；话题切分不同 |
| P06 | A metric-learning method for few-shot cross-event rumor detection，Neurocomputing 2023：[DOI](https://doi.org/10.1016/j.neucom.2023.02.044) | 出版商抽象和可展示 Methodology/Datasets 预览、二级索引；**未完整阅读整篇出版 PDF/细项消融** | **部分全文受出版商访问约束**。不能声称作者代码已核验、不能做严格逐模块首创判断 |
| P07 | TGA-CMF，Information Fusion 2026：[DOI](https://doi.org/10.1016/j.inffus.2026.104486) | 从共同原稿文献条目和可获得出版元数据核对题名、时间衰减/融合定位 | **未精读正文**；仅作为候选 C 的次级近邻 |
| P08 | Event Augmentations，SIGIR 2021：[DOI](https://doi.org/10.1145/3404835.3463001) | 出版元数据与摘要 | **正文未精读**；记为事件增强相关工作而非“已排除创新” |
| P09 | Can We Identify Stance without Target Arguments? LREC-COLING 2024：[ACL 页面](https://aclanthology.org/2024.lrec-main.253/) | 摘要/任务定义 | 任务为 stance，不与事件 rumor 二分类直接对应，**范围排除** |
| P10 | Knowledge Graphs for Real-World Rumour Verification，LREC-COLING 2024：[ACL 页面](https://aclanthology.org/2024.lrec-main.860/) | 摘要/任务定义 | 开放外部证据验证，**范围排除** |
| P11 | Findings ACL 2024 Reinforcement Tuning for Detecting Stances and Debunking Rumors Jointly with Large Language Models：[ACL 页面](https://aclanthology.org/2024.findings-acl.796/) | 搜索命中、摘要/任务 | LLM 相关、非本轮主线，**范围排除** |

## 4. 筛选与排除原则

- **任务不匹配**：立场/传闻真假外部事实核查/知识图谱事实验证不是基于源帖及 240h 回复的事件级 rumor/non-rumor；可列背景不能当直接可比方法。
- **证据形态不匹配**：图增强重要性、预测 KL、事件内时间 window memory、训练折跨事件标签库不是等价操作；写清不同组件解决什么问题，避免“命名相似”误判。
- **评估不匹配**：PHEME 5-event 与 9-event、cross-event held-out 与随机 5-fold、early 观测时间、二类/四类标签、预处理 source-only、是否触及测试集的选点规则，均可阻止绝对指标横比。
- **权限不匹配**：LLM 推理/蒸馏、重建开放事实核查、外部网络检索/大规模数据获取、训练/诊断/模型推理均不在本轮执行范围，故排除为新实验或主线。
- **方法不充分**：单纯修改 backbone、加 attention/门控、改损失权重、重新命名旧未成功路线，不构成充分研究动机；`reference_code/.../model.py` 已有门控代码。
- **全文/代码不足**：P06/P07/P08 未满足首选所要求的全文对读标准，因此不借它们做“首次”等排他判断。首选有 R-Drop、RAGCL、SCSNet 三篇直接重点读过的原文，并加入 SWAM 作为阶段建模边界。

## 5. 资料和操作的可复核边界

- GitHub 共同材料的只读范围：`docs/START_HERE.md`、`UMER_MODEL_ARCHITECTURE.md`、`UMER_EXPERIMENTS.md`、`KNOWN_DIFFERENCES.md`、`RESEARCH_STATUS_2026-10-24.md`、`PRIVACY_AND_PROVENANCE.md`、`DISCUSSION_PROTOCOL.md`；`manuscript/main.tex`、`manuscript/references.bib`、三份 audits；`reference_code/README.md`、`round_013_joint_trifusion/model.py`、`run_fold.py`、`original_model.py`、`regularization.py`、`sam.py`；`results/README.md` 和 6 份汇总 JSON。
- 检索无正式 PRISMA 流程，未使用引用数据库的全量 API 导出，没有可核验的“总命中数/去重数”；承认可能漏掉 2026 年近期论文、受限出版全文/作者代码和未被关键词覆盖的领域方法。本文**不会**称“我们首次提出”、“前作全都没有”等。
- **实际观察缺口**：没有逐事件文本/回复 ID、逐视图 tokenizer offset/cover、单样本预测与话题-误差表。此缺口影响 A/B 成立，不能借聚合 JSON 当作现象诊断。
- **独立性**：只读取 Issue #1 正文作为任务规范及 frozen commit 共同资料，未读取其评论或其他参与者报告；所有判断形成于专用 `chatgpt_web` R1 报告。未创建或执行实验；未运行代码、训练、模型推理或下载大文件。
- 最终候选比较、可推翻链、未来最小验证与停止条件详见 [report.md](report.md)；每条论文的任务/协议与差异见 [evidence_matrix.md](evidence_matrix.md)。

**记录冻结时点**：2026-10-25。若后续因二轮讨论找到遗漏文献，只能追加标注版本的事实订正或 R2 意见，不能无痕改写本轮第一份独立判断。
