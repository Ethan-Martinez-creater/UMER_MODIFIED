# 社会反馈操纵与偏移：补充检索和证据边界

日期：2026-10-25。责任整理：本机 Codex；辅助工作：两个只读检索智能体分别核查社会行为研究与情绪/评论方法，主线程检查阅读范围与结论边界后汇总。辅助检索不是 Zcode 或 ChatGPT 网页的意见，也不新增外部讨论参与者。没有运行模型、访问原始数据、写入其他客户端目录或发送推理请求。

## 1. 本次补充的含义

用户要求考虑的场景包括：水军或机器人放大、群体历史矛盾、带节奏与离题讨论，以及与当前事件判断关系较弱的情绪表达。它们可能由有组织操纵产生，也可能自然发生。**现实成因、可观察的评论变化、检测器实际误差，是三个不同证据层次。**

可先区分四类可观察变化：内容重复或集中放大；情绪分布变化；议题或反应对象偏移；回复数量、挂接与可见性变化。该分类是研究整理，不是已经验证的噪声标签体系。强情绪或反对不等于恶意；同一事件内表现相似也不足以认定水军、机器人或历史群体关系。

## 2. 一手研究与实际阅读深度

| 文献 | 阅读范围与已支持的认识 | 对 UMER 的限制 |
| --- | --- | --- |
| [Shao et al., The spread of low-credibility content by social bots，Nature Communications 2018](https://www.nature.com/articles/s41467-018-06930-7) | 辅助核读结果、采集和 bot 评分方法及限制：特定 Twitter 语料中自动化程度较高的账户参与低可信内容放大，包含早期传播和面向高关注账户的互动 | bot 是分类器评分，低可信来源不等于每篇内容已证伪；传播/转发不证明人类相信，也不证明 UMER 误判。识别主体通常需要账号历史与互动资料 |
| [Pacheco et al., Uncovering Coordinated Networks on Social Media: Methods and Case Studies，ICWSM 2021](https://ojs.aaai.org/index.php/ICWSM/article/view/18075) | 辅助核读方法框架、案例与误报讨论：利用内容复用、共同转发、同步行为等构建账户协同网络 | 协同可能由人类或机器人完成，并不天然恶意；热门内容也可导致误报，需要跨账户记录和进一步核验 |
| [Rathje et al., Out-group animosity drives engagement on social media，PNAS 2021](https://pmc.ncbi.nlm.nih.gov/articles/PMC8256037/) | 辅助核读数据、词典、回归与讨论：美国政治语境中外群体相关表达与更多互动相关 | 是观察性关联，不直接检验谣言回复的离题性、内容真假或检测器；不能把美国政治词典直接移植到本项目两种语言 |
| [MALCOM，ICDM 2020，作者公开稿](https://pike.psu.edu/publications/icdm20.pdf) | 主线程读 §III–IV、§V-A/D 及 §VI-C：追加评论攻击；同时优化表达和话题连贯性，检验过滤防御；文中含政治身份措辞引起模型预测翻转的示例 | 说明误导不要求显式真假表态，但不证明自然群体争吵造成 UMER 错误。其 PHEME 处理后子集、评论长度和协议与 UMER 不同，不搬用攻击率 |
| [Mining Dual Emotion for Fake News Detection，WWW 2021，作者稿](https://www.cs.emory.edu/~kshu5/files/www21_dual_emotion.pdf) | 辅助核读方法、数据与实验：源帖情绪、评论情绪均值/最大值及二者差距，可作为预测信号 | 情绪也可能有用，不能以强情绪定义噪声；统计关联不证明因果，也未直接验证本项目的群体极化或反馈操纵 |
| [Don't Be Misled by Emotion!，IEEE Transactions on Big Data 2024](https://doi.org/10.1109/TBDATA.2023.3334634) | 辅助核对出版信息与摘要，未读完整方法/实验：已有情绪与语义分离及跨语言、跨域适配路线 | 不能再泛称首次提出情绪解耦；全文未核对，不断言它已经解决离题、群体冲突或本项目场景 |
| [Rumor Detection on Twitter with Claim-Guided Hierarchical Graph Attention Networks，EMNLP 2021](https://aclanthology.org/2021.emnlp-main.786/) | 辅助核读方法、实验与消融：源帖引导帖子信息权重和交互图聚合，直接讨论离题回复影响 | 按源帖相关性选择信息已有强近邻；其注意力并非回复相关性的人工真值，未将本项目所述社会反馈偏移作独立受控验证 |
| [Rumor Detection Based on Conflict and Bot Features，BDSC 2024](https://link.springer.com/chapter/10.1007/978-981-97-5803-6_17)，[作者稿](https://cbfu-net.com/papers/Fu_BDSC_24.pdf) | 辅助通过作者稿可检索正文核读方法与结果片段，未完整逐页通读：冲突关系、bot 评分与图建模已有直接工作 | 不能泛称首次结合冲突和 bot 信息；评分不是恶意意图真值。尚未证实本项目有相同数据或标签可复用 |
| [KPG，WWW 2025，作者稿](https://www1.se.cuhk.edu.hk/~swang/KPG.pdf) | 主线程读摘要、§1 与 §3.1/3.2 开头：关键传播图筛选，结合生成候选与分类奖励，已有处理无关/冗余结构的路线 | 本轮未审完整公式和实验闭包。生成或筛选关键回复不是空白，分类奖励也不能当事实证据标注 |
| [Adversary-Aware Rumor Detection，Findings ACL 2021](https://aclanthology.org/2021.findings-acl.118.pdf) | 主线程在 R3 已读 §3.2–3.3、§4.1–4.3：带位置的回复生成、边过滤和对抗微调 | 评论攻击、过滤与对抗训练已有直接先例；本项目若只组合这些处理，不支持独立机制贡献 |

以上自撰摘要不是文献穷尽审计。“原文提到”与“实验证实”必须区分。个别出版全文不可访问时按实际公开稿或摘要标注，没有以二手聚合页补写全文结论。

## 3. 对候选研究问题的约束

**可作为动机**：社会反馈会受自动化、协同、群体关系与情绪影响；已有检测器可以被评论攻击；评论的情绪和相关性本来就可能影响预测。

**尚需 UMER 自身证据**：这些变化是否导致错误、影响哪路表示、是否只是输入预算/节点数效应、正常有效讨论是否也被压制，以及干预能否超过简单强控制。

**不能直接宣称的新意**：首次利用评论情绪、首次进行情绪语义解耦、首次根据源帖选择相关回复、首次建模冲突/bot、首次以回复攻击进行稳健训练。扩大场景名称也不创造方法差异。

若保留该问题框架，潜在增量须进一步落在：有依据地分开事件相关信息与旁观情绪/群体反应的影响；对同一输入变化在图、文本和标签记忆中的传播做受控测量；用匹配的信息与计算预算证明特定机制的必要性。**这些是待论证位置，不是已确认研究空白。**

## 4. 数据、标注和评价边界

- 当前公开材料只描述事件级标签、帖子/传播输入与部分节点/用户特征；没有证实长期账户历史、机器人真值、协同群组、历史矛盾或评论相关性标注已经可用。先核实资源，不能默认存在。
- 可观察维度应分开：评论针对当前主张、人物/机构还是其他群体；是否含有事件相关补充；情绪强度及分布；重复与时间/连接模式；对模型输出的实际影响。它们不能由一个“恶意”分数替代。
- 词面不相似的纠错可能有价值；词面相似的内容也可能只有重复。所谓安全变换、离题和有效信息都需清晰规则与必要人工核验。
- 操纵与自然偏移分开报告；合成压力测试不等于真实水军活动。固定源帖与旧事件标签的测试，不支持任意事实变更后的标签仍然合法。
- 评价需同时检查对干扰的稳健性与对正常有效回复的利用；把全部上下文忽略掉可能降低攻击敏感度，却不支持本项目希望的能力。
- 若涉及旧测试标签挖掘，披露探索接触，重新安排开发/确认边界。没有开展任何数据级诊断，不承诺效果、显著性或录用。

## 5. 检索来源与范围

本轮承接 Codex R3 检索，新增主线程查询包括 `rumor detection emotion bias comments adversarial irrelevant comments social context manipulation`、`misinformation detection coordinated inauthentic behavior bots comment manipulation sentiment polarization`、`rumor detection community conflict political polarization stance unrelated comments robustness`、`rumor detection emotional comments bias dual emotion social emotion`、`rumor detection off-topic comments`、`MALCOM Generating Malicious Comments`、`Improving Rumor Detection by Promoting Information Campaigns` 等，并定向打开上表一手来源。

辅助检索按“机器人/协同与群体反应”“情绪与评论方法”两条只读任务进行；核验范围见表。没有正式系统综述的全量检索、去重和覆盖率；中文社会行为研究与通用稳健学习仍非穷尽。补充材料只含摘要与来源，不上传论文 PDF、帖子内容或账号数据。
