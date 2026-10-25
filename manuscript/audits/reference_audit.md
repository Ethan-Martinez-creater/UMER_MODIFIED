> 公开阅读副本：仅用于理解原稿的历史来源与协议差异；相关私有定位信息已移除。文中“本次”“已核验”“计划”等均指原文记录时点，不代表本次上传或新的工作授权。出现状态冲突时先对照 ../main.tex 与 ../../docs/KNOWN_DIFFERENCES.md。

# WSDM 2027 稿件参考资料审计

本文件记录本次写稿实际查阅或引用的资料，防止后续重复检索、误引或把不同版本
PHEME 的结果混在一起。正文引用条目以 `references.bib` 为准。

## 会议信息与写作风格

| 资料 | 本次用途 | 核验状态 |
|---|---|---|
| [WSDM 2027 CFP](https://wsdm-conference.org/2027/cffp.html) | 匿名审稿类、9 页主文限制、独立 Ethical Considerations、字体嵌入、截止时间 | 已核验 |
| [WSDM 2027 主页](https://www.wsdm-conference.org/2027/) | 会议日期与地点：2027-02-15 至 19，Hong Kong | 已核验 |
| `template/reference.pdf` | WSDM 2026 双栏结构、方法章导读、3.1 问题定义、符号表和公式组织 | 已读取并逐页渲染检查 |
| `template/reference2.pdf` | WSDM 2026 论文叙事，以及 Figure 1 的黑白线框科研流程图风格 | 已读取并逐页渲染检查 |

## 正文已引用论文

| BibTeX key | 论文与链接 | 引用目的 | 核验状态 |
|---|---|---|---|
| `zubiaga2016pheme` | [Analysing How People Orient to and Spread Rumours in Social Media by Looking at Conversational Threads](https://doi.org/10.1371/journal.pone.0150989) | PHEME 来源、会话线程与未决谣言动机 | PLOS 页面核验 |
| `ma2016rnn` | [Detecting Rumors from Microblogs with Recurrent Neural Networks](https://www.ijcai.org/Proceedings/16/Papers/537.pdf) | 序列式谣言检测先行工作 | IJCAI 官方 PDF |
| `bian2020bigcn` | [Rumor Detection on Social Media with Bi-Directional Graph Convolutional Networks](https://doi.org/10.1609/aaai.v34i01.5393) | 双向传播图建模 | AAAI 官方页面核验 |
| `cui2024ragcl` | [Propagation Tree Is Not Deep](https://doi.org/10.1609/aaai.v38i1.27757) | 宽而浅传播树与自适应图对比学习 | AAAI 官方页面核验 |
| `peng2025temporal` | [Rumor Detection on Social Media with Temporal Propagation Structure Optimization](https://aclanthology.org/2025.coling-main.261/) | 时间间隔加权传播树、结构熵编码树与传播噪声背景 | ACL Anthology 正式论文页与 PDF |
| `guo2025fgdgnn` | [FGDGNN: Fine-Grained Dynamic Graph Neural Network for Rumor Detection on Social Media](https://aclanthology.org/2025.findings-acl.296/) | 图快照内与跨快照的细粒度动态传播建模 | ACL Anthology 正式论文页与 BibTeX |
| `wang2025adaat` | [Rumor Detection with Adaptive Data Augmentation and Adversarial Training](https://doi.org/10.1613/jair.1.16963) | 自适应增强、对抗难例与鲁棒性 | JAIR 官方页面核验 |
| `wang2026seegraphmae` | [Robust and Generalizable Rumor Detection with Semantic Evolving Graph Masked Autoencoder](https://doi.org/10.1016/j.patcog.2025.112995) | 语义演化重构、uniformity 和 test-time training | ScienceDirect 页面核验；PHEME 为 9-event |
| `ding2026tgacmf` | [Interpretable Temporal Graph Attention Network and Cross-Modal Fusion for Early Rumor Detection](https://doi.org/10.1016/j.inffus.2026.104486) | 时间衰减图注意力与结构引导文本融合 | ScienceDirect 页面核验 |
| `he2021deberta` | [DeBERTa: Decoding-Enhanced BERT with Disentangled Attention](https://openreview.net/forum?id=XPZIaotutsD) | DeBERTa 基础编码机制 | OpenReview 论文条目 |
| `he2023debertav3` | [DeBERTaV3](https://openreview.net/forum?id=sE7-XhLxHA) | 最终模型文本编码器的预训练机制 | ICLR/OpenReview 正式论文条目 |
| `reimers2019sbert` | [Sentence-BERT](https://doi.org/10.18653/v1/D19-1410) | 384 维 MiniLM 句向量与余弦检索背景 | ACL Anthology/DOI |
| `liang2021rdrop` | [R-Drop: Regularized Dropout for Neural Networks](https://proceedings.neurips.cc/paper/2021/hash/5a66b9200f29ac3fa0ae244cc2a51b39-Abstract.html) | 双随机前向的一致性正则相关工作 | NeurIPS 官方论文页 |
| `foret2021sam` | [Sharpness-Aware Minimization for Efficiently Improving Generalization](https://openreview.net/forum?id=6Tm1mposlrM) | 最终模型的 SAM 目标与两步优化背景 | ICLR/OpenReview 论文条目 |
| `ma2015svmts` | [Detect Rumors Using Time Series of Social Context Information on Microblogging Websites](https://doi.org/10.1145/2806416.2806607) | 4.2 中 SVM-TS 的时序社会上下文特征与线性 SVM 基线 | ACM DOI 与作者论文页核验 |
| `xu2019dlstm` | [Deep Recurrent Neural Network and Data Filtering for Rumor Detection on Sina Weibo](https://doi.org/10.3390/sym11111408) | 4.2 中 DLSTM 的回复分组、用户影响过滤和堆叠 LSTM 基线 | MDPI 正式论文页核验 |
| `liu2025pagcn` | [PAGCN: Structural Semantic Relationship and Attention Mechanism for Rumor Detection](https://doi.org/10.3390/app15168984) | 4.2 中 PAGCN 的语义、传播路径 GCN 与路径注意力基线 | MDPI 正式论文页核验 |
| `huang2025mst` | [Multiview Spatio-Temporal Learning With Dual Dynamic Graph Convolutional Networks for Rumor Detection](https://doi.org/10.1109/TCSS.2024.3520105) | 4.2 中 MST 的累计时间图、双动态图卷积与交叉注意力基线 | IEEE DOI、DBLP 元数据及本地作者仓库核验 |
| `zhang2026rrdn` | [Robust Rumor Detection Against Noise](https://doi.org/10.1016/j.neucom.2026.132741) | 4.2 中 RRD-N 的信息瓶颈对比预训练与贝叶斯变分微调基线 | ScienceDirect DOI、DBLP 元数据及本地作者仓库核验 |

## 2026-07-28 实验章节补充核验

- Table 2 的帖子统计来自两个数据集经过统一 240 小时窗口处理后实际输入模型的
  `graph_final/*.pt`，不是从论文表格反推。PHEME 为 6,425 个事件、105,238 个保留帖子；
  Ma-Weibo 为 4,664 个事件、1,771,329 个保留帖子。
- Ma-Weibo 原论文报告的 3,805,656 条原始帖子只在正文中用于解释预处理前后的规模差异；
  Table 2 的均值、标准差、四分位数、最大最小值和 source-only 比例均按实际模型输入重算。
- 4.2 当前列出的实验基线固定为 SVM-TS、DLSTM、Bi-GCN、RAGCL、PAGCN、
  TGA-CMF、ADAAT-FGM、RRD-N 和 MST。SEE-GraphMAE、CDGCN、MTAS 仍仅保留为
  论文报告结果，不混入本轮九个复现实验基线。

## 2026-07-29 模型简称冲突检查

- `UniMEL` 已被 2024 年的多模态实体链接框架使用：
  [UniMEL: A Unified Framework for Multimodal Entity Linking with Large Language Models](https://arxiv.org/abs/2407.16160)。
- `UniME` 已被 2025 年的通用多模态嵌入模型使用：
  [Breaking the Modality Barrier: Universal Embedding Learning with Multimodal LLMs](https://arxiv.org/abs/2504.17432)。
- 因此稿件不采用 `UniMEL` 或 `UniME`；候选简称改为与主标题直接对应的 `UMER`
  （Unified Multi-Evidence Rumor detection）。上述两篇只用于名称冲突检查，不作为正文
  方法依据，也不加入 `references.bib`。

## 2026-07-29 Introduction 分类叙事候选文献

以下论文用于补充 Introduction 的背景动机，以及“传统机器学习—时序深度模型—
传播结构模型—增强与重构模型”的演进及分类型局限。目前仅完成检索和内容核验，待用户
确认 Introduction 修改稿后再加入 `references.bib` 和正文。为避免方法引用过密，计划
新增引用调整为两篇背景论文和两篇方法论文；其余已检索论文保留记录但不加入正文。

| 候选 key | 论文与链接 | 拟支撑内容 | 核验状态 |
|---|---|---|---|
| `vosoughi2018spread` | [The Spread of True and False News Online](https://doi.org/10.1126/science.aap9559) | 大规模实证说明虚假信息比真实信息传播得更远、更快、更深且更广 | Science 论文 PDF 与 MIT 作者页面核验；计划加入背景 |
| `budak2024harms` | [Misunderstanding the Harms of Online Misinformation](https://doi.org/10.1038/s41586-024-07417-w) | 当前危害证据具有分布异质性，高风险集中于暴露分布尾部，避免开篇作无依据的普遍化陈述 | Nature 正式论文页核验；计划加入背景 |
| `castillo2011credibility` | [Information Credibility on Twitter](https://doi.org/10.1145/1963405.1963500) | 传统方法使用文本、用户行为、转发和外部链接等人工特征评估可信度 | WWW 2011 元数据、作者 PDF 与 DBLP 核验；计划加入方法演进 |
| `ma2018rvnn` | [Rumor Detection on Twitter with Tree-structured Recursive Neural Networks](https://aclanthology.org/P18-1184/) | 自顶向下/自底向上的树结构递归表示，以及序列模型忽略分支结构的局限 | ACL Anthology 正式论文页与 PDF；计划加入方法演进 |
| `kwon2013prominent` | [Prominent Features of Rumor Propagation in Online Social Media](https://doi.org/10.1109/ICDM.2013.61) | 传统方法组合时序、结构和语言统计特征 | IEEE 页面、作者 PDF 与 KAIST 出版记录核验；已检索但暂不加入正文 |
| `ma2020treetransformer` | [Debunking Rumors on Twitter with Tree Transformer](https://aclanthology.org/2020.coling-main.476/) | 树边局部聚合和完全连接聚合各自对会话交互建模的限制 | ACL Anthology 正式论文页与 PDF；已检索但暂不加入正文 |

## 2026-07-29 Related Work 修改候选文献

本轮检索只用于补足 Related Work 中“联合内容与传播建模、跨事件语义支持、SAM
变体”三个明确缺口。待用户确认修改稿后再决定加入 `references.bib`。

| 候选 key | 论文与链接 | 拟支撑内容 | 核验与采用状态 |
|---|---|---|---|
| `tu2021rumor2vec` | [Rumor2vec: A Rumor Detection Framework with Joint Text and Propagation Structure Representation Learning](https://doi.org/10.1016/j.ins.2020.12.080) | 通过跨事件 union graph 联合学习文本和传播表示；说明端到端联合建模本身并非本文首创 | ScienceDirect 正式论文页与 DBLP 核验；计划采用 |
| `tian2022duck` | [DUCK: Rumour Detection on Social Media by Modelling User and Comment Propagation Networks](https://aclanthology.org/2022.naacl-main.364/) | Transformer 与图注意力联合建模会话内容、评论网络和用户网络 | ACL Anthology 正式论文页核验；计划采用 |
| `ren2021crosstopic` | [Cross-Topic Rumor Detection using Topic-Mixtures](https://aclanthology.org/2021.eacl-main.131/) | 训练主题表示及其混合用于跨主题泛化，与实例级跨事件邻域证据区分 | ACL Anthology 正式论文与 PDF 核验；计划采用 |
| `ran2023metacross` | [A Metric-Learning Method for Few-Shot Cross-Event Rumor Detection](https://doi.org/10.1016/j.neucom.2023.02.044) | 用历史事件上的原型/关系度量和 episodic training 适应少样本新事件 | Neurocomputing/ScienceDirect 正式论文页核验；计划采用 |
| `wu2022crossdoc` | [Cross-document Misinformation Detection based on Event Graph Reasoning](https://aclanthology.org/2022.naacl-main.40/) | 对相关文档簇构建跨文档事件图，作为相邻领域的跨样本证据方法 | ACL Anthology 正式论文页与 BibTeX 核验；计划采用，但需明确其任务和数据不同 |
| `kwon2021asam` | [ASAM: Adaptive Sharpness-Aware Minimization for Scale-Invariant Learning of Deep Neural Networks](https://proceedings.mlr.press/v139/kwon21b.html) | 通过参数尺度自适应邻域缓解原始 SAM 的重缩放敏感性 | ICML/PMLR 正式论文页核验；计划采用 |
| `zhuang2022gsam` | [Surrogate Gap Minimization Improves Sharpness-Aware Training](https://openreview.net/forum?id=edONMAnhLu-) | GSAM 在 perturbed loss 外显式减小 surrogate gap | ICLR/OpenReview 正式论文页核验；计划采用 |
| `kim2022fishersam` | [Fisher SAM: Information Geometry and Sharpness Aware Minimisation](https://proceedings.mlr.press/v162/kim22f.html) | 以 Fisher 信息诱导的椭球替代欧氏参数邻域 | ICML/PMLR 正式论文页核验；计划采用 |
| `mi2022ssam` | [Make Sharpness-Aware Minimization Stronger: A Sparsified Perturbation Approach](https://proceedings.neurips.cc/paper_files/paper/2022/hash/c859b99b5d717c9035e79d43dfd69435-Abstract-Conference.html) | 仅扰动选择参数以降低 SAM 全参数扰动成本 | NeurIPS 正式论文页核验；已检索，篇幅有限时暂不采用 |
| `tahmasebi2024universalsam` | [A Universal Class of Sharpness-Aware Minimization Algorithms](https://proceedings.mlr.press/v235/tahmasebi24b.html) | 统一不同 Hessian sharpness measures，并提出 Frob-SAM/Det-SAM | ICML/PMLR 正式论文页核验；已检索，暂不采用 |
| `shin2025overparam` | [Critical Influence of Overparameterization on Sharpness-aware Minimization](https://proceedings.mlr.press/v286/shin25a.html) | 分析过参数化、噪声与稀疏条件对 SAM 的影响 | UAI/PMLR 正式论文页核验；已检索，暂不采用 |
| `he2021eventaugment` | [Rumor Detection on Social Media with Event Augmentations](https://doi.org/10.1145/3404835.3463001) | 事件级增强的相邻工作 | SIGIR 出版元数据核验；当前 RAGCL/ADAAT 已覆盖增强线，暂不采用 |

## 2026-07-29 Figure 1 视觉表达参考

本轮只检查正式论文架构图如何使用数据对象、运算符和交互连线表达模型，不从这些
论文引入新模块，也不复用其图形布局或视觉资产。第二版候选图仍严格依据 UMER 的实际
实现绘制。

| 论文与链接 | 检查的图形表达 | 采用边界 |
|---|---|---|
| [DUCK: Rumour Detection on Social Media by Modelling User and Comment Propagation Networks](https://aclanthology.org/2022.naacl-main.364/) | Figure 1/2 使用传播树、评论链、动态图节点编码和图聚合表现不同数据结构及其变换 | 只借鉴“直接画数据结构”的表达原则，不复用其 BERT+GAT 架构 |
| [Rumor Detection on Twitter with Claim-Guided Hierarchical Graph Attention Networks](https://aclanthology.org/2021.emnlp-main.786/) | Figure 2 用图节点、层级注意力和 claim 引导连线解释模块作用及交互 | 只借鉴注意力关系的可视表达，不引入 claim-guided attention |
| [Propagation Tree Is Not Deep: Adaptive Graph Contrastive Learning Approach for Rumor Detection](https://doi.org/10.1609/aaai.v38i1.27757) | Figure 3 用原始图、增强视图和表示关系区分数据对象与学习约束 | 只用于确认“多视图关系应被直接画出”，不引入图对比增强 |
| [Rumor Detection on Social Media with Temporal Propagation Structure Optimization](https://aclanthology.org/2025.coling-main.261/) | 用加权传播树和编码树展示结构变化，而非使用纯文字模块框 | 只借鉴结构变换画法，不引入时间加权或编码树 |

第三版候选图另核验了 ACM 相关技术要求：

- [GECCO 2026 Paper Submission Instructions](https://sigevo.hosting.acm.org/gecco-2026/Paper%2BSubmission%2BInstructions)：
  提交 PDF 应使用嵌入的 Type 1 或 TrueType 字体，不能包含 Type 3 字体。
- [Creating Accessible Figures and Tables](https://dis.acm.org/2023/creating-accessible-figures-and-tables/)：
  图形应避免只靠颜色传递信息，栅格图建议至少 300 DPI，并在最终排版尺寸下保持清晰。
- `fig1_umer_candidate_v3.pdf` 已使用嵌入式 Arial TrueType 字体，`pdffonts` 检查
  三个字体资源均为 `emb=yes` 且不存在 Type 3；按 ACM `figure*` 约 506 pt 的最终宽度
  估算，图中最小 22 pt 画布文字对应约 7.0 pt 的排版字号。

## 使用边界

- 最终模型的数据规模、窗口、节点统计、五折划分、超参数、选模规则和最终指标来自
  原研究代码、配置和正式结果，不从上述论文反推。
- SEE-GraphMAE 明确使用 9-event PHEME；不得与 5-event/5802 版本结果混用。
- TGA-CMF、SEE-GraphMAE 等 2026 工作目前只用于相关工作陈述，不用于尚未完成的
  公平对比结论。
- WSDM 2026 两篇参考稿只用于学习章节结构和版式，没有复用其具体文字。
- WSDM 2027 CFP 明确要求在参考文献前保留 `Ethical Considerations`，且该部分不计入
  9 页正文限制。因此即使两篇 WSDM 2026 参考稿在实验后只显示 Conclusion，本稿也不能
  删除伦理章节。
