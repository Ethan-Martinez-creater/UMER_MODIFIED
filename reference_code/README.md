# UMER 关键源码阅读快照

本目录用于核对模型结构与训练机制，**不是可以直接运行的项目**。未导入完整依赖闭包、配置、数据、模型或检查点。本次没有执行这些代码，也没有核验正式检查点与代码的完全对应关系。

| 本仓库文件 | 历史源码相对标识 | 阅读内容 |
|---|---|---|
| round_013_joint_trifusion/model.py | project/optimization_rounds/round_013_joint_trifusion/model.py | 三路模型、近邻记忆、融合、辅助损失 |
| round_013_joint_trifusion/run_fold.py | project/optimization_rounds/round_013_joint_trifusion/run_fold.py | 数据与视图、划分、选点、训练循环、SAM 重放 |
| original_model.py | project/src/rumor_detection/models/original_model.py | Set 编码、结构特征、一层 Transformer 图分支 |
| sam.py | project/optimization_rounds/round_032_sam/sam.py | RNG 状态、累积窗口、扰动与精确恢复 |
| regularization.py | project/optimization_rounds/round_021_cross_view_consistency/regularization.py | 跨视图广义 JSD |

run_fold.py 中两个私有部署默认值已改为 generic relative placeholders；其余算法正文不作方法改写。模型支持的可选融合、认知蒸馏钩子与历史默认值不代表正式 UMER 启用了这些功能。正式设置看 [实验记录](../docs/UMER_EXPERIMENTS.md)。

训练环境锁定文件和部署说明不在本公开资料包中；不应据此推测任何当前运行环境。原始与发布文本校验值、来源标识及变更说明见 [SOURCE_MANIFEST.json](../SOURCE_MANIFEST.json)。
