[codex_local | R3 | 论文主线提案]

# 面向可操纵社会反馈的谣言检测：跨表征的回复依赖与稳健利用

- 作者：本机 Codex；具体产品模型 ID 未独立核验。日期：2026-10-25。
- 依据：共同背景 d71e5b7、勘误 e22a237、三份冻结 R1 与两份已发布 R2，以及用户在本会话明确的 R3 目标。提交前未读取其他参与者的 R3。
- 定位：一个有条件的主选提案，供三方比较；不是已证实的新机制，不建议据此直接启动正式训练。本轮没有运行模型、处理原始数据、连接计算环境或修改原稿。
- 目标：回答导师对研究动机与创新不足的质疑。常规测试集上的 Accuracy/F1 提升不能独自承担贡献；二分类继续作为评价载体。不把 R1 的覆盖调权或记忆门控直接升级为论文主线。本轮不设第二条并行备选。

## 1. 研究问题与事实边界

**问题：当源帖不变、讨论区出现少量集中重复的回复时，检测器能否继续利用社会上下文，同时避免被重复表达带偏？** 这对应可操纵讨论区中的检测可靠性，而不是另一个总体分数优化问题。先研究事件窗口内的受控回复追加，不声称还原真实平台上的协调操纵。

已知 UMER 的文本、图和检索查询都使用同一事件的帖子：文本经四种序列化进入 DeBERTa；图同时使用节点语义、结构和非文本统计；记忆查询由节点语义的 source/mean/max/mean−source 构成。**模型分支不同，不代表输入信息相互独立。** 但当前线性融合没有声明概率独立假设，不能据架构直接指控它“错误地按独立证据做贝叶斯累乘”。

待验证的假设是：重复回复可能同时改变文本暴露、图统计和检索查询，造成多个通道向同一错误方向移动；分别在分支内去噪可能遗漏这种共同输入变化。**UMER 是否发生、影响多大、记忆是否参与，均未知。** 原随机五折与组件消融不能代替该证据。

## 2. 最直接前作与拟研究的差异

| 前作与实际阅读范围 | 已解决的部分 | 本提案仍需证明的差异 |
| --- | --- | --- |
| [AARD，Findings ACL 2021](https://aclanthology.org/2021.findings-acl.118.pdf)，§3.2–3.3、§4.1–4.3；作者 README | 学习边过滤，生成带位置的对抗回复，并作对抗微调；已经报告干净性能与攻击稳健性的取舍 | 不能再以“回复攻击＋过滤＋对抗训练”为贡献。拟研究同一回复经多种表示共同传递的依赖，以及共享处理相对独立防御的必要性 |
| [CGAT，IJCAI 2020](https://www.ijcai.org/proceedings/2020/0197.pdf)，§3–4、§5.2–5.4 | 在用户—帖子—评论异构图中定义受领域约束的伪装，并通过图结构对抗学习防御 | 它已联合使用文本和结构。差异不能写成“首次图文联合防御”；需落到同一原始回复在多路事件表示中的同步影响与处理 |
| [HAT4RD，Sensors 2022](https://doi.org/10.3390/s22176652)，本轮读 [arXiv v2](https://arxiv.org/pdf/2110.00425) 的分层训练与 Robustness Analysis，未核对期刊全文逐式一致性 | 帖子级、事件级嵌入对抗训练，并检验词级攻击 | 不能靠把 SAM 换成输入扰动获得新意；待检验的是离散回复追加及表示间共同来源，不是更平坦损失面 |
| [RERD，TKDD 2024](https://doi.org/10.1145/3653023)：作者机构摘要＋作者代码局部，出版全文 403 | 已覆盖噪声/不完整传播、标签问题、用户消失；代码提供两类图的边扰动评估 | 已读 `MixGraphDataset` 中文本图与传播图分别调用随机扰动。它说明“独立表示噪声”控制有实现先例，不证明整篇工作从未研究共同扰动。完整新颖性判断仍需全文核对 |

上述论文的样本、标签或划分与 UMER 不同，不搬用其绝对分数作直接比较。最新检索还发现一般证据依赖聚合已有直接讨论（附录），所以“相关证据不能重复计数”本身也不是新贡献。

## 3. 核心机制假设与最小方法结构

**主张不是让三个输出更一致，而是让三路对同一回复集合采用可追溯、共同的内容重复处理。**

候选结构：在事件输入端建立共享回复分组，再映射到三路表示。精确重复按文本规范化确定；近重复可使用已有语义嵌入，但相似度只代表候选分组，不能充当来源独立性、立场或事实可信度的真值。源帖单独保留。

同组的内容权重不因复制次数线性增加：文本给同组分配受限阅读份额；图在内容聚合与关系统计中显式区分组内重复和组间关系；记忆查询使用相同分组规则的语义统计，并重建合法训练库。传播规模、时间等仍有可能有用，应单列并控制影响，而非一律删除。精确算子尚待诊断确定；这一结构是可比较原型，尚不是定型的新模型。

核心对照是：**相同分组器、相同可见信息与预算下，共享处理是否优于各分支独立处理，以及统一的简单去重。** 仅优于原 UMER、不优于普通去重或常规对抗训练，不支持新机制。现有 reliability gate、conditional residual 是必要控制，不能换名当新增发明。

这不等于跨视图 JSD 调权。四视图一致性只涉及文本输出，不能自动约束图与记忆的共同输入变化；记忆查询也并非由这四个 DeBERTa 视图生成。R1 的 A 可作文本观测检查，B 可作检索变化审计，二者不再承担论文主线。

## 4. 新增贡献及总体指标持平时的价值

成功必须同时留下三项证据：

1. **可复核的新认识**：在 UMER 及至少一个不同结构的检测器上，识别并定位受控回复放大带来的共同通道偏移；区分单路主导、共同偏移和普通节点数效应。
2. **有排他证据的机制**：共享回复依赖处理相对简单去重、独立过滤及相同增强预算的常规训练有增量，解释为什么，而非只增加模块。
3. **明确的新能力**：在冻结的回复追加预算与未参与训练的压力测试下减少错误翻转/性能退化，常规能力满足预定非劣要求；同时保留真实不同回复带来的预测收益。

因此，即使干净集 Macro-F1 持平，论文仍可贡献“在明确操纵条件下可靠地利用社会反馈”的能力与机制证据。这里仍需量化指标，但其承担的是新条件下能力的验证。只有若干攻击样例、换一个测试集提高分数，或靠退回 source-only 获得稳健性，都不满足目标。**不提供认证鲁棒性、因果来源识别或真实世界安全保证。**

## 5. 完整论文的证据链与工作范围

| 研究内容 | 必须回答的问题与控制 |
| --- | --- |
| 问题与测量协议 | 固定源帖、原回复和事件标签，仅追加允许的回复节点；所有表示从同一个修改后事件重建，训练库不受攻击；记录时间、挂接、节点上限、文本预算与有效攻击比例。追加测试是受控场景，不把原标签称为重标的事实真假 |
| 机制定位 | 固定检查点追踪三路输出。对正式线性融合，边际变化满足 `Δz=Δz_graph+Δz_text+Δz_memory` 的精确加法分解；这是审计工具，不是新归因算法。不能宣称融合头产生超加性相互作用，也不把输入敏感性当作独立重训的组件因果效应 |
| 方法比较 | UMER、source-only、最强简单统一去重/近重复处理、各分支独立处理、常规回复增强/对抗训练、共享处理。匹配 backbone、SAM、选择规则、前向与调参预算，区分输入改变与参数训练效果 |
| 能力与失效边界 | PHEME、Ma-Weibo；复制、近重复与不同挂接条件分开；使用留出的攻击/扰动族与自适应攻击评价。报告预算曲线、攻击成功率的干净正确样本分母、整体/分组 Macro-F1、置信区间与成本；正常多样回复对照防止“不看上下文”取巧 |

实验单位是源事件，攻击变体不是独立样本。近重复语料若需要人工审核，必须单列资源；未经审核的语义相似样本只能算相似度压力测试。所有阈值、攻击选择和效应门槛在开发层确定；旧外层标签已用于研究启发，不能重新称为完全未触碰确认集。若复用语料，预注册重新评估并披露接触历史；任何未见话题结论另需真正隔离训练，非本主线的默认附加任务。

## 6. 可行性、成本与否决条件

可继承：事件标签、允许窗口、帖子语义嵌入、图/文本骨干、四视图、检索及融合实现、SAM 和正式结果。新增：原帖到三路输入的统一映射、共同扰动构造、分组与表示重建、机制审计及稳健性评价。**数据—文本—树—特征的闭包、检查点与缓存存在性本轮未核验**；公开五份代码和六份 JSON 不足以运行。

成本为中等以上。首项筛查无需重训，但需要数据处理和新前向。方法阶段必须重训，不能直接装到旧权重上作最终比较。示例预算：6 个配置×2 数据集×3 种子，在一个共同冻结划分上即 36 次训练；若全部采用五折则为 180 次，另有攻击评估与近邻复现成本。这是工作量估算，不是已承诺执行清单或时长。应先用单数据集、两个种子的开发筛查淘汰；若总预算不能支持必要控制，本路线不适合“尽快投稿”。

明确否决：共同偏移很弱或完全由单路主导；去重已解释收益；共享处理不优于匹配的独立处理；近重复分组只能靠未落实的新标注成立；稳健性来自忽略正常上下文；只有自己训练过的扰动有效；或直接前作已经包含等价机制。不能通过不断更换扰动或扩大命名挽救。

## 7. 第一项验证：配对回复放大与通道分解（仅设计）

在获准后，先核验原数据映射和重建闭包；缺失即 NOT_READY。仅取固定的训练/内层开发样本，两数据集分别检查，不触碰外层测试来选方案。建议每数据集固定抽取至多 200 个有回复且能合法追加的事件，source-only 和容量不足事件单列数量与原因，不从总评价中静默移除。

对每事件构造干净输入，以及追加 1/3 条同一既有回复的输入；配等节点数、等长度条件的分散回复追加控制。选择规则固定且不读取查询真值，时间和挂接保持合法；超节点上限与文本挤占效应单独审计。精确复制只是受控探针，不代表真实攻击分布。需要的特征由修改后事件重算，不能只改文本或只改图。200×5 条件×2 数据集×4 文本视图约为 8,000 条文本序列，另有预处理与图/检索计算；不含未落实的近重复攻击。

输出：事件配对的最终边际变化、错误翻转及三路加权贡献、节点数/长度控制，以及简单全路去重后的敏感性检查。内层验证曾参与检查点选择，结果只能作探索。**只有存在超过预先约定最小效应的共同偏移、且并非简单去重即可解释时，才讨论下一阶段机制筛查。** 若效果只出现在精确复制上，必须先落实独立近重复/正常回复验证，不能宣称方法准入。筛查不证明最终防御有效。

**本方建议：将此主线放入 R3 横向比较，暂不授权实验。它比 A/B 更能回答贡献目标，但直接前作拥挤、算子与资源未闭合，当前不应宣称已找到满足投稿要求的新方法。**

---

## 核验附录：阅读、检索与未完成项

### 共同材料与版本

- [背景与修正 @ e22a237](https://github.com/Ethan-Martinez-creater/UMER_MODIFIED/tree/e22a23796f34106ced8575cb3cd95f6aed863061)：START_HERE、ARCHITECTURE、EXPERIMENTS、KNOWN_DIFFERENCES、RESEARCH_STATUS、PRIVACY、协议、源码及既有汇总。R3 复查以当前根目录的相应公开副本为辅；未使用另一个客户端的工作树。
- [本方 R1 @ fb4cd29](https://github.com/Ethan-Martinez-creater/UMER_MODIFIED/blob/fb4cd294db2c069df8bd3a1f3879054231ac433f/discussions/umer-001/codex_local/report.md)、[网页端 R1 @ b3676b8](https://github.com/Ethan-Martinez-creater/UMER_MODIFIED/blob/b3676b8520b3a09ea6621707b36697467dd2e559/discussions/umer-001/chatgpt_web/report.md)、[Zcode R1 @ 515acdb](https://github.com/Ethan-Martinez-creater/UMER_MODIFIED/blob/515acdb0e9992a06e549b2c0263d64391013f73f/discussions/umer-001/zcode_local/report.md)。
- 固定 R2 阅读：[网页端](https://github.com/Ethan-Martinez-creater/UMER_MODIFIED/issues/1#issuecomment-6392995853)、[Zcode](https://github.com/Ethan-Martinez-creater/UMER_MODIFIED/issues/1#issuecomment-6393004638)。未刷新 Issue 评论来读取任何 R3。本方前一轮评议在当前会话；本提案记录关键修订，不冒充已发布过第三份 R2。
- 本方 R2/R3 修订：低重叠≠截断损害，even/odd 不截断也会不相交；覆盖/分歧/错误共现≠一致性有害；记忆查询不直接来自四视图；原消融不作逐事件归因。发布副本勘误不构成原模型缺陷。

### 新增论文/代码实际读取

- AARD：官方 PDF 的方法与攻击/实验段已读；[作者 README，blob 5628683](https://github.com/yunzhusong/AARD/blob/main/README.md) 已读，未审完整代码、未下载其数据和生成器权重。该 README 链接外部模型，不能据“有仓库”承诺立即复现。
- CGAT：官方 PDF 上述范围已读，未核验完整作者代码闭包。
- HAT4RD：期刊题名/DOI 已核；实读 arXiv:2110.00425v2 方法与攻击分析。PMC 正文打开触发校验，MDPI 正文 429，不声称精读最终出版全文。
- RERD：[作者机构页](https://researchoutput.ncku.edu.tw/en/publications/towards-robust-rumor-detection-with-graph-contrastive-and-curricu/) 的摘要及发表状态；[作者代码 @ 75ba4e0](https://github.com/wenming-tw/RERD/tree/75ba4e0a77409fd6130d72c107eb5314a2050020)，实际读取 `Ours/edge_noise.py`（blob a6e8943）和 `Ours/Process/dataset_pert.py`（blob 1a2d033），不外推未读论文内容。
- [GAAC，KBS 2026](https://doi.org/10.1016/j.knosys.2026.115664)：只读出版页摘要及可见方法/实验概述，未读完整公式；已覆盖图增强、对抗困难样本与对比训练，因此本提案不把三者组合当差异。
- [Backdoor Attack on Propagation-based Rumor Detectors，AAAI 2025](https://ojs.aaai.org/index.php/AAAI/article/view/33944)：官方摘要/状态，PDF 获取失败；它是训练污染/触发器设定，不能冒充本提案仅测试时追加的直接同协议结果。
- [Echo chamber dynamics and influence aware evidence aggregation，2026-10-24](https://link.springer.com/article/10.1007/s44163-026-02245-5)：仅核读摘要、Introduction/研究问题。它已讨论相关证据与过度置信；本提案不声称首次建模证据依赖，也不能把实际来源关系从回复相似度中推断出来。
- [Node-aware Bi-smoothing](https://arxiv.org/abs/2312.03979)：只读摘要；通用图注入认证已有方法。当前不选择认证路线，不把平滑套用当新定理。

### 本轮检索词（2026-10-25）

使用公开 Web 搜索，以作者/出版原始来源核验；不是系统综述。主要查询如下（同主题的并列查询合并记）：

1. `rumor detection budget adaptive comment selection evidence sufficiency efficient detection`
2. `rumor detection source post context conflict debiasing generalization reply evidence`
3. `rumor detection social context acquisition cost budget selective comments reinforcement learning`
4. `"rumor detection" "budget" selection comments`；`"rumor detection" "adaptive" "selection" replies efficient`；`"rumor detection" "early exit" OR "cost-sensitive" OR "acquisition"`
5. `"rumor detection" "duplicate" replies robustness`；`rumor detection adversarial replies defense robustness social context manipulation`
6. `"Adversary-Aware Rumor Detection" 2021`；`"rumor detection" "coordinated" "robust" comments`
7. `certified robustness rumor detection graph node injection smoothing`；`"rumor detection" "certified"`；`"node injection" "randomized smoothing" certified graph`；`"rumor detection" "redundancy" "adversarial"`
8. `"rumor detection" "duplicate" "defense"`；`"rumor detection" "redundancy" "robustness" comments clustering`；`"misinformation detection" "correlated evidence" OR "evidence dependence"`；`"rumor detection" "multi-view" "adversarial" defense`
9. `"rumor detection" "correlated" "attack"`；`"rumor detection" "multi-evidence" robustness manipulation`；`"rumor detection" "deduplication" OR "deduplication" "fake news"`；`"Adversary-Aware Rumor Detection" defense replication redundancy`
10. `"Backdoor Attack on Propagation-based Rumor Detectors" arxiv github`；`"Improving the Robustness of Rumor Detection" WISE 2024 adversarial metadata`；`"rumor detection" "duplicate replies" OR "repeated replies"`
11. `"Towards Robust Rumor Detection with Graph Contrastive and Curriculum Learning"`；`"Robustness-Enhanced Rumor Detection" paper pdf`

预算读取/自适应回复路线因与 FoRM、SCSNet、早期停止等既有工作接近，未选为第二主线。WISE 2024 的作者 PDF 访问超时，仅作线索；不据二手聚合网页作方法断言。中文文献、通用多表示鲁棒学习/重复不变聚合方法，以及 RERD 完整论文尚未充分覆盖；这些限制使本轮只能提出候选，不能给出排他性创新结论。

新增公开内容仅为本提案；没有帖子原文、逐事件标识/预测、部署或连接信息、凭据或私有绝对路径。
