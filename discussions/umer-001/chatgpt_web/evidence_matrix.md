# UMER-001 / R1 证据矩阵（chatgpt_web）

> 证据截止：2026-10-25。基准 commit：`d71e5b7595deba3a6e7cbc53e8cc98d1b6944334`。原始第一轮判断独立形成，未阅读其他参与者交付、PR 或 Issue 评论。本矩阵区分仓库事实、论文原文事实、推断、尚待检验假设；不包含新的实验或模型运行。候选代号：**A** 可观测覆盖条件化文本视图一致性（首选）；**B** 跨话题训练记忆适用域拒绝（唯一备选）；**C** 早期分阶段检测（暂缓）。分数不可跨不同测试协议直接比较。

## A. 共同材料：现有 UMER 实证与代码事实

| ID | 可复核事实 / 数值 | 定位（基准 commit 相对路径） | 对候选的含义 | 证据层级 / 不能推出 |
| --- | --- | --- | --- | --- |
| U01 | 输入是源帖+240h 回复；输出事件级 rumor/non-rumor，并不核查陈述真伪，也不是早期检测 | `docs/START_HERE.md` §§1–4；`manuscript/main.tex` §3.1、§4.1（约 310–388、666–740 行） | A/B 保留现有任务，C 要重设观测时段 | **确认的任务定义**；不能以 240h 结果证明早期效果 |
| U02 | PHEME 6,425 事件、2,402 rumor/4,023 non-rumor，105,238 个保留帖，source-only 677 (10.54%)；中位 12 帖/事件 | `docs/UMER_EXPERIMENTS.md` §1；`manuscript/main.tex` §4.1，Table 2 | A 的稀疏负对照与长度分层；B 的话题相关性需另查 | **汇总确认**；source-only 存在不是条件化 JSD 必要性的证明 |
| U03 | Ma-Weibo 4,664 事件、2,313/2,351，1,771,329 保留帖，source-only 6 (0.13%)；中位 236 帖/事件 | `docs/UMER_EXPERIMENTS.md` §2；`manuscript/main.tex` §4.1，Table 2 | A 有长对话观测预算的合理研究动机 | **数据分布确认**；中位回复数量不代表已进入 tokenizer 的帖子数 |
| U04 | 四个源帖固定首位文本视图 full/reversed/even/odd，train 随机抽 2，val/test 取 4 logits 均值，DeBERTa-v3-large 的 tokenizer `max_length=256` | `docs/UMER_MODEL_ARCHITECTURE.md` §2.2、§4、§9；`reference_code/round_013_joint_trifusion/run_fold.py` 第 104–165 行（`JointEventDataset.encode`）| A 的**已存在观测预算和视图变换**；可提出覆盖重合度诊断 | **源码/架构确认**；视图 token 交集、冲突/伤害尚未测量。该归档未含 `round_009` 构造函数正文 |
| U05 | `sample_view_subset` 从视图 logits 中均匀无放回抽不同视图；文本概率一致性用每事件视图的无条件广义 JSD | `reference_code/round_013_joint_trifusion/model.py` 第 10–27、325–334、393–418 行；`reference_code/regularization.py` 第 6–16 行；`manuscript/main.tex` §3.3 | A 正面面对“任意视图无条件拉齐”的现状 | **确认为实现的目标形式**；还未确定该目标在哪类事件失败 |
| U06 | 三路分别是图节点 Set/Transformer、DeBERTa 文本与训练折内 31 近邻标签 log-odds（T=.05）；Linear(5,2) | `docs/UMER_MODEL_ARCHITECTURE.md` §§3–6；`reference_code/round_013_joint_trifusion/model.py` 第 202–232、343–353 行；`reference_code/original_model.py` 第 35–69、113–204 行 | A 修改视图机制时保持其余三路与融合不变；B 必须与现有库对照 | **源码阅读确认**；不能把邻近 rumor 标签当事实证据 |
| U07 | 记忆仅来自训练分区；训练查询排除自己，val/test 不加入库；outer stratified 5-fold seed 3090，inner validation 选 checkpoint/threshold，train seed 2000 | `docs/UMER_MODEL_ARCHITECTURE.md` §§5、8；`docs/UMER_EXPERIMENTS.md` §4；`reference_code/round_013_joint_trifusion/model.py` 第 218–232 行；`run_fold.py` 第 735–775 行 | B 分析话题支持域，但不得使用外层 test 标签；A 以同样选择边界检验 | **协议确认为已有记载**；事件互斥不等于话题独立 |
| U08 | SAM effective event batch=64（4×16），rho=.05；图/文本辅助 CE 各 .15、JSD 权重 .5；验证/测试 4 文本视图 | `docs/UMER_MODEL_ARCHITECTURE.md` §§6–9；`reference_code/sam.py` 第 7–24、58–105 行；`manuscript/main.tex` §3.5 | 首选最小验证保持训练目标/计算预算可比 | **冻结协议**；在本轮未训练、未复现 |
| U09 | PHEME 完整 Accuracy / Macro-F1 / Rumor-F1 = 0.8988327 / 0.8925436 / 0.8666235；Ma-Weibo 对应 0.9689094 / 0.9689014 / 0.9693597 | `results/pheme_summary.json`、`results/maweibo_summary.json` 的 `mean` | 既有质量基线，不能用不同划分的前作分数直接排位 | **官方聚合 JSON**；没有重新计算逐事件指标 |
| U10 | PHEME no_text 0.8600778、no_consistency 0.8894942、no_graph 0.8940078、no_memory 0.8985214 Accuracy；相对完整为 -3.88/-0.93/-0.48/-0.03 pt | `results/pheme_ablation/{no_text,no_consistency,no_graph,no_memory}_summary.json` 的 `mean.accuracy` | A 值得诊断但**不可**先宣布改进；B 现有收益上限警示 | **五折聚合消融**；消融仅证明相应配置下的平均差异，非归因给覆盖/话题污染 |
| U11 | 文稿文本辅助 CE 公式与源码“每个受监督视图 CE”不一致；Set 结构描述与节点维度内 MLP/pooling 有差别 | `docs/KNOWN_DIFFERENCES.md` §1–3；`reference_code/round_013_joint_trifusion/model.py` 第 405–415 行；`reference_code/original_model.py` 第 35–69 行 | 应修正论文准确性，**不算**新研究贡献 | **已登记差异**，禁止擅改原稿 |
| U12 | PHEME MST 0.8691 排除了 source-only；Bi-GCN/RAGCL/RRD-N 采用含测试折访问的作者协议；Ma-Weibo RRD-N 仅三折 | `manuscript/audits/pheme_comparison_metrics_audit.md` Protocol qualifications；`manuscript/audits/maweibo_macro_metrics_audit.md` Reporting rule | 首选验证基线必须可比，完整评估总体和验证选择须对齐 | **历史审计事实**；“同一个外层折”不足以证明所有基线无泄漏 |
| U13 | `ReliabilityGatedFusion` 和 `ConditionalResidualFusion` 已写入阅读快照，正式使用 linear | `reference_code/round_013_joint_trifusion/model.py` 第 30–114、179–200、349–361 行；`docs/UMER_MODEL_ARCHITECTURE.md` §6 | A/B 若只换门控，可能是已有代码重试，需作为对照 | **代码存在**；不能说这两变体已是最终已验证配置 |

## B. 公开文献：逐项核查方法、协议与可能差异

“阅读范围”只说明本轮实际能读到的部分；**摘要/页面不能冒充全文阅读**。正式发表年份按出版来源登记，部分论文在预印本先行时不重复算新工作。以下主要站点为官方论文页/PDF；作者代码只在确已打开时才可称核验，本轮未审任何外部完整代码。

| ID | 题名、年份、发表状态与原始链接 | 实际阅读范围、任务/评估协议 | **实际方法**及与 UMER 的关键比较 | 关联 / 可证伪风险 |
| --- | --- | --- | --- | --- |
| L01 | Liang et al. **R-Drop: Regularized Dropout for Neural Networks**，**NeurIPS 2021 正式发表**。[官方 PDF](https://proceedings.neurips.cc/paper_files/paper/2021/file/5a66b9200f29ac3fa0ae244cc2a51b39-Paper.pdf) | 原文 §2.1–2.2、§3，尤其两次随机前向/监督及 KL 公式、任务表；多个分类及语言任务，**非**事件级 PHEME 协议 | 对**同一输入**的独立 dropout 子模型输出施加双向 KL；UMER 已具针对两个不同回复序列化的 JSD。**本提案**仅可能区别在截断后实际“输入证据不等价”时要不要拉齐 | A：若只重用 R-Drop/JSD 而无观测差异解释，则**无新颖性** |
| L02 | Cui & Jia **Propagation Tree Is Not Deep: Adaptive Graph Contrastive Learning Approach for Rumor Detection**（RAGCL），**AAAI 2024 正式发表**。[官方 PDF](https://ojs.aaai.org/index.php/AAAI/article/download/27757/27555)；[论文链接作者代码](https://github.com/CcQunResearch/RAGCL) | 官方原文方法部分（约 pp.75–77），实验/消融（约 pp.77–79）；Weibo、DRWeibo 二分类，Twitter15/16 四类，作者采用随机切分重复；**不能与 UMER 固定 PHEME 五折直接比**；作者仓库链接发现但**代码未审** | 根据 graph degree / betweenness / PageRank 优先级构建节点/边/特征增强（保护 root），对比学习。UMER 四个文本序列化+JSD 而非同样的图增强。若仅用“选关键回复、做自适应图增强”，已被直接覆盖；只有“tokenizer 实际可见内容与一致性适用条件”的机制需进一步验证 | A/C：近邻**强**，不许称首次自适应回复筛选 |
| L03 | Kang & Yuan **Early detection of online public opinion rumors for cross-event generalization**（SCSNet），**Discover Artificial Intelligence 2026-09-18 正式发表**。[Springer 开放全文](https://link.springer.com/article/10.1007/s44163-026-02227-7) | 全文 §§3.1–3.4、§4.1–4.3，检视传播阶段/贡献公式/模型对照；PHEME 跨事件/话题评估（公开文稿列 Macro-F1 82.74%），**非 UMER 随机五折协议** | 用回复相对源/父的差异、时间与深度估计信息贡献；软阶段动态划分并门控更新预测状态。它已覆盖“新回复有无信息”“分阶段预测是否更新”；UMER 无该状态机；A 必须限于**同一固定任务的被观察文本视图是否信息可比** | A/C：相邻机制**非常强**；简单“有信息更新、无信息保持”不能单独成原创 |
| L04 | Guo et al. **SWAM: Adaptive Sliding Window and Memory-Augmented Attention Model for Rumor Detection**，**EMNLP 2025 正式发表**。[ACL Anthology PDF](https://aclanthology.org/2025.emnlp-main.729.pdf) | 原文方法 §§3.3–3.5、实验 §§4.1–4.4 与早期检测段落；Twitter/DRWeibo 传播图基准（论文具体划分与复现须独立核准），并非 UMER 五折 | 按传播速率自适应时间窗口，前窗隐藏状态作为**事件内** memory，结合深度编码/attention 演化；与 UMER **跨事件训练标签近邻库**不是同一种 memory | C：早期状态学习已有充分直接近邻，暂缓；B 不得将 SWAM 冒充跨事件标签检索 |
| L05 | Ren et al. **Cross-Topic Rumor Detection using Topic-Mixtures**，**EACL 2021 正式发表**。[ACL Anthology PDF](https://aclanthology.org/2021.eacl-main.131.pdf) | 官方原文方法/实验 §§3–4，包括话题混合构造、跨话题 PHEME 划分；与固定事件随机五折不同 | 表示训练话题分布与目标实例混合，意图处理未见话题；UMER 的 top-31 是余弦近邻**标签**加权的同训练折证据，缺少显式支持域诊断，但“跨话题”动机并不新 | B：若只是 topic mixture，直接撞前作 |
| L06 | Ran et al. **A metric-learning method for few-shot cross-event rumor detection**，**Neurocomputing 2023 正式发表**。[DOI/出版商](https://doi.org/10.1016/j.neucom.2023.02.044) | 出版页面 abstract 与可访问 Methodology/Datasets 预览；**出版商全文部分受限**、未核验完整方法/消融/作者代码；PHEME5/PHEME9 few-shot cross-event protocol（具体采样需全文复核） | episodic metric learning、原型/关系度量，以少量新事件监督做迁移；UMER 训练折近邻是固定无梯度的标签支持，**没有**few-shot 适应。不可用不同数据/监督下的准确率比较 | B：强调近邻度量与跨事件迁移已非新；待全文复核后才可作更细粒度“新方法不重合”断言 |
| L07 | Ding et al. **Interpretable Temporal Graph Attention Network and Cross-Modal Fusion for Early Rumor Detection**（TGA-CMF），**Information Fusion 2026 正式发表**。[DOI](https://doi.org/10.1016/j.inffus.2026.104486) | 本轮仅核对共有稿 §2.1、参考文献/引用和公开出版元信息；**未精读全文**，不作为排他性创新性判断主依据 | 时间衰减图 attention 和图引导文本融合的近邻；UMER 本身没有已验证 early-window 协议 | C：进一步降低单纯“时间图+文本融合”新颖性，证据深度较浅 |
| L08 | He et al. **Rumor Detection on Social Media with Event Augmentations**，**SIGIR 2021 正式发表**。[DOI](https://doi.org/10.1145/3404835.3463001) | 公开论文元数据/摘要；**未读全部正文**，不能推断具体增强公式或协议 | 事件增强既有方法；UMER 四种确定性视图与原文增强应在正式创新主张前逐一核验 | A：广义“事件级数据增强”不能独占为新贡献 |
| L09 | Li & Scarton **Can We Identify Stance without Target Arguments? A Study for Rumour Stance Classification**，**LREC-COLING 2024 正式发表**。[ACL Anthology](https://aclanthology.org/2024.lrec-main.253/) | 页面摘要/任务定义；rumour **stance** 分类，不是事件 rumor/non-rumor | 判别回复立场的任务与 UMER 事件二分类不同；可辅助理解立场信息，不能用 stance 标签替代事件标签 | A/C：**范围排除**，不作为直接机制第一近邻 |
| L10 | Dougrez-Lewis et al. **Knowledge Graphs for Real-World Rumour Verification**，**LREC-COLING 2024 正式发表**。[ACL Anthology](https://aclanthology.org/2024.lrec-main.860/) | 论文页与摘要/任务；涉及外部 KG 信息验证 | 显式事实验证超出本轮维持事件二分类的范围 | **排除外部事实核查主线**，不作为近邻机制 |
| L11 | Yang et al. **Large Language Models for Rumour Stance Classification**（或文献同类 LLM 立场研究），**Findings of ACL 2024 正式**。[ACL Anthology](https://aclanthology.org/2024.findings-acl.796/) | 仅查询命中与摘要，**没有**全文分析 | LLM 生成/立场推理不是用户本轮研究方向 | **范围排除**，不能由不成功的历史 LLM 推出所有 LLM 不可用 |

## C. 证据链判定与优先验证的反例

| 待判断命题 | 当前直接证据 | 仍缺的关键事实 | 如果发现……则如何改变判断 |
| --- | --- | --- | --- |
| A1：固定文本视图的有效观察覆盖常不同 | U03–U05：长会话分布 + 四视图 + 256-token | tokenizer 后哪几条回复实际可见、两视图交集（尤其源帖截断） | 若大量视图有效 token 完全一致或差异少，A **停止** |
| A2：这种不等价会使无条件一致性失当 | U10 的 JSD 整体**正效应**，反而要求谨慎 | 原内层验证视图分歧、覆盖相异、错误/校准关系，按事先冻结分组 | 若覆盖相异与预测错误/过置信无关系，或 JSD 对该组仍显著更稳，A **停止** |
| A3：条件化一致性优于普通工程控制 | L01、L02、L03 暗示大量先验机制 | 同资源下随机回复、普通长度权重、无 JSD、视图选取、原内置门控等强控制 | 若简单控制完全解释差别，**只能算工程优化，不宣称机制研究** |
| B1：近邻库有适用域外高置信支持错误 | U06–U07、U10（记忆总体贡献仅 ~0.03pt）；L05–L06 | 训练折合法话题 ID，预定义 out-of-topic 与高风险子群的错误分析 | 若 memory/no_memory 难分或分歧无跨话题结构，B **停止** |
| B2：记忆域拒绝有新贡献 | U13 内置门控，L05/L06 直接近邻 | 超过已有 gate、缩小 k、标签熵拒绝及简单不使用记忆的可比验证 | 未超越即**停止** |
| C1：新早期机制有值得改变协议的创新性 | U01、L03/L04/L07 | 时间戳可信度、严格到达时序、优于 SWAM/SCSNet 的独立机制 | 若只是“先截窗口+自适应注意力”，C **不立项** |

## D. 阅读与证据完整性声明

- 公开学术“方法接近”只说明**已搜索到的特定方法**，不能推断“首次”、未有某机制或已覆盖全部截至 2026-10-25 文献；未访问与出版付费壁垒分别记录于 [search_log.md](search_log.md)。
- 报告中的外部结果不作为和 UMER 的直接数值比较；标签空间、PHEME 5/9-event 组成、话题隔离、early-stage 时间条件及 test-selection 有实质差别。
- 冻结汇总仅能说明**已保存的结果**，不能描述为在本轮“重新复现”；文件中没有逐事件帖子、概率、梯度或真实 tokenizer 覆盖统计。
- 这份独立矩阵只供 Issue #1 三方提交齐备后的交叉讨论使用。本轮不读取其他方报告，不启动实验。
