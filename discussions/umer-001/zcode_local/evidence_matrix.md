# [UMER-001][R1][zcode_local] 近邻证据矩阵

阅读深度标注：**全文**＝正文 PDF/HTML 完整读取；**摘要级**＝正式发表页摘要+元数据；**检索片段**＝仅搜索结果摘要，未打开原文。检索日期均为 2026-10-25。

## 1. 话题转移 / 评估协议 / 捷径（候选 C1 邻域）

| # | 论文（题名缩写） | 年份/状态 | 链接 | 阅读深度 | 任务与协议 | 现有机制 | 与 UMER 的关系及本项目可能差异 |
|---|---|---|---|---|---|---|---|
| N1 | Cross-Topic Rumor Detection using Topic-Mixtures（Ren, Jiang, Khoo, Chieu） | EACL 2021，正式发表 | https://aclanthology.org/2021.eacl-main.131/ | **全文**（PDF 文本层） | PHEME 5 话题（非 9 话题全集）LOTO；提出 open-topic 场景（测试混入已见话题） | 话题表示 + 话题混合适配 StA-HiPLAN 骨干；debias 词表遮蔽诊断 | 关键协议先例与话题捷径证据源：其 Table 1 显示 in-topic Acc 67.69% → 遮蔽 top-20 话题词 36.70% → LOTO 34.41%（debias 后 41.93%）。差异：单一检测器、无多证据分支归因、无记忆检索通道；UMER 需在 9 话题全集上重做协议并做通道级测量 |
| N2 | All-in-one: Multi-task Learning for Rumour Verification（Kochkina, Liakata, Zubiaga） | ACL 2018，正式发表 | https://aclanthology.org/C18-1288.pdf | 摘要级（二手引用其协议） | PHEME **LOEO** 交叉验证的确立者（比 RumourEval 随机划分更难、更接近现实） | 多任务分级验证 | 协议出处。差异：验证（stance 链）任务，非事件级二分类；不做通道归因 |
| N3 | Evaluating the generalisability of neural rumour verification models（Kochkina et al.） | IPM 2023，正式发表（付费墙） | https://www.sciencedirect.com/science/article/pii/S0306457322002175 | 摘要级（全文未能访问；Warwick 仓库开放版存在：https://wrap.warwick.ac.uk/id/eprint/171888） | 跨事件、跨数据集（PHEME↔Twitter15/16）、跨时间泛化评估 | 评估研究（非新机制） | 结论（据摘要与二手描述）：神经验证模型在未见事件/数据集上显著低于域内，学到 event/dataset-specific 模式。差异：不做多证据通道级归因、不研究检索式记忆。**未读全文，结论强度受限** |
| N4 | It's about Time: Rethinking Evaluation on Rumor Detection Benchmarks using Chronological Splits（Mu, Bontcheva, Aletras） | EACL Findings 2023，正式发表 | https://aclanthology.org/2023.findings-eacl.55/ | 摘要级 | 时间感知（chronological）划分的评估反思；PHEME 等 | 评估研究 | 同时关联 C1（严格划分）与 C2（时间维度）。差异：划分维度为时间而非话题留出下的通道行为；无记忆机制 |
| N5 | Truth over Tricks: Measuring and Mitigating Shortcut Learning in Misinformation Detection | NeurIPS 2025，正式发表；arXiv 2506.02350 | https://arxiv.org/abs/2506.02350 | 摘要级 | 14 个虚假信息基准、7 个检测器的统一捷径评测；文本捷径注入与对齐 | 评测范式 + LLM 数据增强缓解（SMF） | 证明"捷径评测"已是正式评测范式，UMER 的随机五折相对滞后。差异：聚焦文本检测器与文本捷径、缓解靠数据增强；不涉及传播结构通道、kNN 标签记忆或话题留出协议下的通道归因 |
| N6 | GCML: Gradient Coherence Guided Meta-Learning for Cross-Domain Emerging Topic Rumor Detection（He et al.） | EMNLP 2025，正式发表 | https://aclanthology.org/2025.emnlp-main.968/ | 摘要级 | 跨域新兴话题谣言检测（域移位+目标域标注稀缺） | 梯度一致性引导的元学习 | 证明 2025 年新兴话题检测仍为活跃问题。差异：机制族为元学习任务采样，与 UMER 的证据融合/kNN 记忆正交；不做通道归因 |
| N7 | Unseen Domain Fake News Detection via Causal Debiasing / CSDA（Gong et al.） | arXiv 2024（2411.09389）；后续版本 2025 | https://arxiv.org/abs/2411.09389 | 摘要级 | 零样本/未见域假新闻检测 | 因子图去偏（causal subgraph-oriented domain adaptation） | **C1 最近的"方法型"占位者**：已占据"OOD 假新闻+证据模态比较"动机位。差异：表示层去偏路线；不研究非参数标签检索通道的失效与门控——C1 的差异化必须与此正面比较 |
| N8 | Detecting Breaking News Rumors of Emerging Topics in Social Media（Alkhodair et al.） | IPM 2020，正式发表 | https://dmas.lab.mcgill.ca/fung/pub/ADFL20ipm_postprint.pdf | 检索片段 | 新兴话题谣言检测（5 折模拟） | 时序+传播特征分类 | 早期 cross-topic 场景论证。差异：非神经多证据架构、无通道归因 |
| N9 | TALME（Topical Adversarial LLM-based Misinformation Enforcer） | 2025，ACM 正式发表 | https://dl.acm.org/doi/full/10.1145/3787279.3787298 | 检索片段 | 未见话题泛化 | 话题对抗 + LLM | 被排除出细读：LLM 增强路线在本议题边界外（Issue 明确不以大模型为主线），仅登记其占位 |

## 2. 早期检测 / 渐进证据（候选 C2 邻域）

| # | 论文 | 年份/状态 | 链接 | 阅读深度 | 任务与协议 | 现有机制 | 关系与差异 |
|---|---|---|---|---|---|---|---|
| N10 | Early Rumour Detection（Zhou, Shu, Wang, Zafarani） | NAACL 2019，正式发表 | https://aclanthology.org/N19-1163/ | 摘要级（引用 116+） | 流式早期谣言检测（Twitter/Weibo） | suspense 早期预警信号 + 分类 | C2 直接近邻：证明"多早能检出"是确立的任务。差异：单模型流式判决，无多证据通道/记忆检索，无通道价值随截点变化的分析 |
| N11 | CED: Credible Early Detection of Social Media Rumors | 2018 预印本 | arXiv（检索定位） | 检索片段 | 早期检测、检测延迟最小化 | 转发可信信号建模 | 同上，预印本状态，登记不细读 |
| N12 | PreERD: Early Detection of Rumors Based on Propagation Prediction | 期刊/预印本（未核验 venue） | 检索定位 | 检索片段 | 早期检测 | 先预测未来传播结构再检测 | 与 C2 的"证据到达"假设相关：预测式补全 vs UMER 的等待式窗口。**发表状态未核验** |
| N13 | TGA-CMF（已在 main.tex 引用，ding2026tgacmf） | 2026，正式发表 | 见 manuscript/references.bib | 已引（本轮未重读原文） | 自称 early detection 的时间衰减图注意力+图文融合 | 图引导文本融合 | UMER 现有对比基线之一。注意：其与 UMER 的比较在**全窗口**协议下进行，非截点协议——C2 若立项须重建比较 |
| N14 | Rumor Detection with Graph Structured Features（Yang et al., IJCAI） | IJCAI（年份未核验） | 检索定位 | 检索片段 | 变时间窗口下的传播路径分类 | 图结构特征 | 涉及"varying time windows"。**年份与 venue 未核验**，登记 |

## 3. 选择性预测 / 不确定性（候选 C3 邻域）

| # | 论文 | 年份/状态 | 链接 | 阅读深度 | 关系与差异 |
|---|---|---|---|---|---|
| N15 | CAWE-X: Confidence-Aware Explainable Weighted Ensemble | 2025，期刊（IJAIML，影响力有限） | https://www.svedbergopen.com/index.php/ijaiml/article/view/2896 | 检索片段 | 误导内容检测的校准+选择性分类+不确定性集成。与 C3 最近但 venue 弱、未读全文；说明该组合已有尝试 |
| N16 | Calibrated Selective Fact-Checking via Evidence Chain | 2026 预印本 | https://arxiv.org/html/2607.18240v1 | 检索片段 | LLM 事实核查的拒答+校准。语境为 LLM 生成式核查，非判别式多证据融合；C3 与其差异在证据源（模型内分支分歧 vs 外部证据链） |
| N17 | MiniVer-V | 2026 预印本 | https://arxiv.org/html/2610.11233v1 | 检索片段 | 短视频虚假信息的最小充分证据+选择性预测。多模态语境，间接支持"selective prediction 进入虚假信息领域"的趋势判断 |

## 4. 检索/记忆式谣言检测（背景邻域，用于界定记忆通道的新颖性边界）

| # | 论文 | 年份/状态 | 链接 | 阅读深度 | 关系与差异 |
|---|---|---|---|---|---|
| N18 | MR²: Benchmark for Multimodal Retrieval-Augmented Rumor Detection | SIGIR 2023，正式发表 | https://dl.acm.org/doi/10.1145/3539618.3591896 | 摘要级 | 检索**外部证据文档**辅助检测（多模态基准）。与 UMER 记忆通道的本质差异：MR² 检索外部世界证据，UMER 检索**训练折事件的标签先验**——后者无外部语料依赖，也正因此其可用性绑定训练分布（C1/H2 的机制根据） |
| N19 | SWAM: Adaptive Sliding Window and Memory-Augmented Attention | EMNLP 2025，正式发表 | https://aclanthology.org/2025.emnlp-main.729/ | 摘要级 | 滑动窗口+传播模式记忆注意力。占位"memory+rumor"关键词；其记忆为可学习注意力键值（参数化），非 kNN 标签检索；亦不做话题转移分析 |
| N20 | Multi-modal Knowledge-Aware Event Memory Network（EMN） | 期刊（slogix 索引，venue 未核验） | 检索定位 | 检索片段 | 全局事件记忆存事件不变特征、以相似事件查询。与 UMER 记忆通道最接近的"用过去事件"设计，但检索对象是特征表示而非标签先验。**venue 未核验** |
| — | （背景）kNN-LM 一类非参数检索增强 | 通用 NLP | — | 未检索（超出本轮范围） | 通用机制背景；C1 立项时建议补检"non-parametric label memory under distribution shift"以确认转移行为研究空白。本轮未检索，不做空白声明 |

## 5. 仓库内部证据（候选论证直接引用）

| 编号 | 材料 | 位置 | 用途 |
|---|---|---|---|
| E1 | PHEME/Ma-Weibo 正式五折与四项消融汇总 | `results/*.json` | F1 消融结构；F2 逐折差的计算来源（full − no_memory 逐折 Acc：+0.54/−0.31/−0.55/−0.47/+0.93pt，均值 +0.031pt；std 0.0080→0.0028） |
| E2 | 消融表与协议限定 | `manuscript/main.tex` §4.3、Table 6；`manuscript/audits/pheme_comparison_metrics_audit.md` | F1/F3/F6 叙事与协议边界 |
| E3 | 记忆通道实现与审计接口 | `reference_code/round_013_joint_trifusion/model.py` L202–261（`event_semantic_features`/`retrieve`/`retrieve_with_evidence`） | F4/F8：标签检索机制与零成本导出接口 |
| E4 | 冻结协议与逐折阈值 | `docs/UMER_EXPERIMENTS.md` | F3/F6 |
| E5 | 边界声明（随机五折≠跨话题、240h≠早期） | `README.md`、`docs/START_HERE.md` §4 | F3/F5 的官方边界表述 |
| E6 | 历史负结果边界 | `docs/history/LLM_INTEGRATION_ATTEMPTS_2026-08.md`、`docs/RESEARCH_STATUS_2026-10-24.md` | 确认 C1–C3 均不落入已关闭路线（无大模型推理、无外部事实证据、无人工 gold 依赖） |
