# [UMER-001][R1][zcode_local] 检索记录

- 检索日期：2026-10-25（全部检索在本日完成）
- 工具：WebSearch（后端 Z.ai web_search_prime，美区）；定向阅读用 webReader / WebFetch
- 说明：以下逐条记录检索词、主要命中、采纳与排除。排除标准：(a) 与候选方向无机制关联；(b) 大模型推理/蒸馏主线（Issue 边界排除，仅登记占位）；(c) 无法核实发表状态的零散预印本（登记但不细读）。
- 通用局限：未使用学术数据库 API（如 Semantic Scholar API）；检索覆盖以搜索引擎可达为限，"未命中"不等于文献不存在。

## 检索序列

| # | 时间段 | 检索词（原文） | 主要命中（采纳→编号） | 主要排除项与原因 |
|---|---|---|---|---|
| S1 | 10-25 | `cross-topic rumor detection generalization unseen topics` | Ren 2021（→N1）、Alkhodair IPM（→N8）、Ran 2023 Neurocomputing（few-shot cross-event，登记未细读：检索片段级）、GCML（→N6）、TALME（→N9，LLM 增强仅登记）、Ran & Jia 无监督跨域（排除：仅 Semantic Scholar 条目，无正文可达）、Lang 2026 多模态跨域（排除：多模态路线） | 无监督跨域条目无法读到正文；多模态方向与现有资产不符 |
| S2 | 10-25 | `topic bias shortcut learning misinformation fake news detection` | Truth over Tricks NeurIPS 2025（→N5）、SIGIR 2022 Bias Mitigation for Evidence-aware FND（登记：表示去偏证据类，未细读）、Source Bias MDPI（排除：fact-check 语料偏置，非话题协议）、SSRN source confounds（排除：同上）、TruthLens GitHub 项目（排除：工程项目） | — |
| S3 | 10-25 | `leave-one-topic-out PHEME rumor detection topic split evaluation` | Mu 2023（→N4）、Wu 2025 PLOS Temporal Tree（登记：LOEO 协议使用者之一，未细读）、Kochkina IPM 2023（→N3）、Ren 2021 SMU 版（同 N1）、Li et al. survey（排除：综述，无新增近邻）、Kaggle PHEME 页（排除：数据镜像页） | — |
| S4 | 10-25 | `early rumor detection social media time window delay detection performance` | CED 2018（→N11）、Zhou 2019（→N10，经 S8 确认 NAACL）、PreERD（→N12）、Yang IJCAI graph structured features（→N14）、Askarizade 2026 survey（排除：综述）、Shu 2025 unverified（排除：任务定义类） | 多数命中无直达链接（引擎返回正文片段），仅能以片段级登记 |
| S5 | 10-25 | `selective prediction uncertainty abstention fake news misinformation detection` | MiniVer-V（→N17）、CAWE-X（→N15）、Calibrated Selective Fact-Checking（→N16）、Nature SRep Dunning-Kruger LLM（排除：LLM 元认知，非检测机制）、Grounding Information Disorder（排除：理论批评）、Uncertainty-aware Web-Conditioned（排除：科学事实核查语境） | 该方向近邻分散且多为 LLM 语境，支持把 C3 降级为伴生分析的判断 |
| S6 | 10-25 | `retrieval augmented rumor detection memory similar events` | MR² SIGIR 2023（→N18）、SWAM EMNLP 2025（→N19）、EMN（→N20）、Metadata-Free LLM-augmented（排除：LLM 路线）、KBS 2024 memory-augmented transformer（排除：传播记忆注意力变体，venue 可达性未核验） | 用于确认"用过去事件辅助检测"已有多种占位，UMER 记忆通道的新颖性只能在转移行为/条件可靠性上建立 |
| S7 | 10-25 | `Kochkina "generalisability" rumour verification leave-one-event-out PHEME findings` | All-in-one ACL 2018（→N2）、Kochkina IPM 2023（→N3 补充：Warwick 开放版定位）、PHEMEPlus（排除：数据增强论文） | ScienceDirect 付费墙；未读 IPM 2023 全文，已在矩阵标注 |
| S8 | 10-25 | `Zhou "early rumour detection" 2019 ACL anthology suspense early warning` | 确认 N10 = Zhou, Shu, Wang, Zafarani, NAACL-HLT 2019（N19-1163，116+ 引） | — |
| S9 | 10-25 | `propagation structure versus text features out-of-distribution generalization fake news degradation`（引擎两次细化：`... OOD generalization ... performance degradation`、`"fake news" out-of-distribution ... social graph propagation vs textual content paper`） | CSDA/Gong 2024-2025（→N7）、Propagation Structure-Semantic Transfer Learning arXiv 2026（登记：转移学习桥接路线，摘要级，未编入矩阵细读——与 C7/N7 同族占位）、UPSAR COLING 2022（登记：不确定性传播结构重构，鲁棒性路线）、PSALLM Neural Networks 2026（排除：LLM 传播感知） | 首次查询返回教育类无关结果（引擎未锁定学术语料），已通过加引号与限定词细化；此为引擎质量问题，记录在案 |

## 定向阅读记录（非检索，逐篇打开）

| # | 对象 | 读取方式 | 实际读取范围 | 备注 |
|---|---|---|---|---|
| R1 | Ren et al. EACL 2021 全文 PDF | webReader | 全文文本层：任务设定、Table 1（in-topic 67.69 / topic-mask 36.70 / LOTO 34.41 / debias 41.93）、方法与实验段 | 本轮唯一全文级近邻；数字已用于报告 F/S1 论证 |
| R2 | Mu et al. EACL Findings 2023 | webReader（ACL landing） | 标题+摘要+元数据 | 标题全称含 "using Chronological Splits" |
| R3 | Truth over Tricks | WebFetch（arXiv abs） | 摘要 | 7 检测器×14 基准、SMF 缓解 |
| R4 | GCML EMNLP 2025 | webReader（ACL landing） | 标题+摘要 | 元学习机制确认 |
| R5 | Kochkina IPM 2023 | 检索综合（S3/S7） | 摘要+二手描述 | 全文付费墙；开放版已定位未读 |
| R6 | Zhou et al. NAACL 2019 | 检索综合（S4/S8） | 摘要 | — |

## 检索中明确记录的访问失败/受限

1. Kochkina IPM 2023（ScienceDirect）：付费墙，全文未读。
2. WebFetch 对 `aclanthology.org/*.pdf` 返回 "Unsupported content type: application/pdf"，改用 webReader 成功读取 Ren 2021；其余 PDF 未逐一尝试 webReader。
3. S4 命中的多数条目（CED、PreERD、Yang IJCAI）无引擎直达链接，仅片段级信息；PreERD 与 Yang 的 venue/年份未核验。
4. ACD-RAG（ScienceDirect 403）等在八月旧审计中已登记的线索，本轮未重复检索（与 UMER-001 候选无关）。

## 未执行的检索（明确记录，供 R2 或后续轮补做）

- "non-parametric / kNN label memory under distribution shift"（通用 ML 文献）：用于确认 C1/H2 的机制层空白，本轮因时间预算未做，报告 F.4 已相应不做空白声明。
- Ma-Weibo 是否存在话题/领域标注的官方说明：影响 C1 的跨数据集扩展论证，未检索。
- 中文文献（CNKI 等）：本轮检索均为英文源，中文近邻覆盖为零，记录为已知盲区。
