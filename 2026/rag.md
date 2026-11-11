# RAG 2026

## 2026.06
### SPARK【自适应知识参与】
> **自适应知识参与**：像开卷答题时给记忆调音量：每生成一步，轻量策略就根据当前状态调节各层 FFN 的参与程度，让参数记忆与检索证据的取舍能够随生成过程变化。
>

* 时间：06.26
* 论文：[SPARK: Adaptive Parametric Knowledge Participation for Faithful Retrieval-Augmented Generation](https://arxiv.org/abs/2606.27786)

SPARK 将参数知识控制建模为潜在参与策略学习。在冻结主干大模型的前提下，轻量参与策略在每个解码步骤自适应缩放 FFN 对生成的贡献，并通过面向忠实性的奖励进行优化，以缓解参数知识与检索上下文冲突时的不忠实生成。该方法需要训练参与策略，不需要修改主干模型权重。

![](https://raw.githubusercontent.com/OpenBMB/SPARK/main/figs/framework.png)
