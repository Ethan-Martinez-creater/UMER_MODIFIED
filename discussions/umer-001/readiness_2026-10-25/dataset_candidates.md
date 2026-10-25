# R4 数据候选：标签匹配与真实可得性

核验日期：2026-10-25。范围：作者/组织方材料、官方发布页及一项静态包的本地检查。只公开科研说明，不发布原始文字、标识或数据副本。

## 当前选择建议

**优先准入 RumourEval 2019 作为事件判断主任务候选；继续核实 C3 的文章相关性子标注作为辅助测量。** 两者角色分开，不拼接成虚假的逐事件联合标签。Conversations Gone Awry 可覆盖人身攻击维度，但不替代相关性或谣言判断。

尚未发现并核实一个同时具有事件标签、回复相关性、操纵意图及完整结构、又可直接使用的数据包。更换数据可减少部分标注工作，不能凭数据名称补齐其没有的标签。本轮不承诺已经获得完整新基准。

## 主任务候选：RumourEval 2019

官方页提供静态归档（16,512,097 字节，MD5 85b37dc70106c2b9f584e63164fcbb92）。本轮实际下载并核对，训练/开发部分有 365 份源帖、6,337 份回复及 365 份结构；抽查 Twitter/Reddit 均含文字。train/dev 事件答案分别 327/38 条，实际标签为 true/false/unverified；SDQC 标注分别 5,217/1,485 条，包含源帖，不全是回复。测试包和测试答案未打开。[官方发布](https://figshare.com/articles/dataset/RumourEval_2019_data/8845580)、[组织方说明](https://github.com/kippfreud/RumourEval)、[任务论文](https://aclanthology.org/S19-2147/)

可取之处是已有人工事件判断、回复立场和结构。comment 仅表示未明确贡献于判断主张真伪，不能当纯离题；任务也不同于原 rumor/non-rumor。发布页为 CC BY 4.0，组织方同时要求遵守 Twitter 条款。与 PHEME 有共同来源，须查线程/主张重合，不能称为天然独立外部测试。

## 辅助与备选资源

| 资源 | 可测维度与可得性证据 | 局限与当前定位 |
| --- | --- | --- |
| [C3 / 作者数据入口](https://github.com/kvarada/constructiveness)、[论文](https://firstmonday.org/ojs/index.php/fm/article/download/13163/11006/82451) | 12,000 条顶层新闻评论，有人工建设性子特征 non relevant（针对关联文章）；每条 3–5 名标注者 | 最接近现有人工离题信号，但该子特征统计采用至少一人勾选，不代表多数一致；导出列名、SOCC 关联键与数据包许可尚待核实。无事件真假标签，暂为优先辅助候选 |
| [SOCC](https://github.com/sfu-discourse-lab/SOCC) | 有文章正文、评论和线程关联，另有小型人工建设性/毒性标注 | 不建设性不等于离题；用于给 C3 恢复文章上下文，须先核对连接。仓库许可 CC BY-NC-SA 4.0 |
| [Conversations Gone Awry WIKI](https://convokit.cornell.edu/documentation/awry.html) | 官方 schema 含发言、回复结构和由三名众包者判断的个人攻击；4,188 对话、30,021 条发言；有官方下载入口 | 可作人身攻击辅助；不是离题/谣言标签。本轮未下载，语料许可另核，不套用工具包许可 |
| [Unhealthy Conversations 官方仓库](https://github.com/conversationai/unhealthy-conversations)、[论文](https://arxiv.org/abs/2010.07410) | 44,355 条短评论，人工敌意、挖苦、轻蔑等维度；提供个体标注与划分 | 标注者未见文章上下文，不能用于相关性判断；与 SOCC 的连接键未核实。可作较低优先行为辅助，CC BY-NC-SA 4.0 |
| [SCRum-9](https://zenodo.org/records/18167949)、[论文](https://arxiv.org/abs/2505.18916) | 7,516 个源帖/回复对，九语言，多标注者立场和信心；官方有 CSV | 论文说明发布 ID，文字需平台回填；comment 混合多种情形。当前比静态文本更费事，暂不优先；作者说明 CC BY-NC-SA 4.0 |
| [SRQ](https://zenodo.org/records/3609277)、[论文](https://arxiv.org/abs/2006.00691) | 争议话题中目标帖与回复/引用的人工立场；有标注包入口 | 不是事件真假或离题标签；本轮未下载，文本实际字段与许可需再核；跨主题立场辅助备选 |
| [Tunnels 评论集](https://zenodo.org/records/4698969)、[作者机构说明](https://research.uni-hannover.de/en/datasets/dataset-of-video-comments-of-a-vision-video-classified-by-their-r/) | 有文字与针对需求工程的相关性、极性；评论三人标，回复一人标 | 仅一条技术愿景视频，标签不是一般事件相关性；只适合窄域探针，非主任务；本轮未下载、许可未核 |
| [AARD](https://github.com/yunzhusong/AARD)、[MALCOM](https://github.com/lethaiq/MALCOM) | 作者提供攻击实现及数据入口，可比较构造攻击的稳健性 | 本轮未运行或核实外链数据。生成攻击不是人工恶意/离题 gold，也不覆盖所有群体争执 |

2026 年的 [Discourser 论文](https://www.nature.com/articles/s41599-026-07900-x)讨论 1,684 对 YouTube 文字的人工作用/跑题标注，但明确称原评论未释放；补充物为匿名化表，未核实含可用文字，作者代码示例不能替代语料。故不把它列为已可用基准。它也提醒：跑题不自动等于恶意意图。

## 划分原则与下一步

最终先选一个主任务和必要的辅助资源，不同时训练所有语料。RumourEval 先检查官方划分的线程、主张及来源重叠；C3/SOCC 按文章分组；CGA 按页面/对话并保留配对关系。所有扰动变体随原主张同组，辅助数据与主任务重合另查。

下一项选型检查是 C3 的真实下载字段、文章连接和许可。本轮 DOI 元数据指向 [SFU 仓储](https://summit.sfu.ca/item/35642)，但页面返回访问拒绝，元数据 rightsList 为空，不能据此补出许可。若无法闭合，保留 RumourEval 的人工立场能力测量，把相关性解释限定为探索性 agent 筛查，不把后者升级成人工真值。最终数据、确认集和任务头尚未冻结，暂不开展新训练。
