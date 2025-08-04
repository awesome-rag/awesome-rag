# RAG 2025

## 2025.02
### CAG【缓存即知识】
> **缓存即知识**：像一位把常用参考书提前复印并装订成册的老教授，不再临时翻图书馆，而是直接把整本“知识”塞进 32K/64K 长上下文 LLM 的 KV-Cache。遇到提问，模型无需检索，直接从缓存里秒读原文，既省延迟又避幻觉，把 RAG 的“查-拼-答”三步曲简化成一步“读-答”。
> 

* 时间：02.23
* 论文：[Don't Do RAG: When Cache-Augmented Generation is All You Need for Knowledge Tasks](https://arxiv.org/abs/2412.15605)

Cache-Augmented Generation（CAG）把知识库一次性离线编码进长上下文 LLM 的 KV-Cache，推理阶段零检索、零延迟，直接读缓存输出答案。在 SQuAD 与 HotPotQA 多档规模实验中，CAG 的 BERTScore 均优于或持平传统 BM25/Dense RAG，且消除检索开销。

![](https://i.imgur.com/aNdQZdl.png)


## 2025.04
### AlayaDB【长程记忆库】
> **长程记忆库**：像一座为超大模型量身定制的“智能图书馆”，把原本散落在 GPU 显存里的 KV-Cache 和检索索引统一搬进高性能分块存储层，实现“冷热分层、按需取阅”。在实验验证的 192 K token 级别上下文下，系统仍能在毫秒级定位并加载关键片段，既显著节省显存又保持与全注意力相当的精度，让长文本推理像翻书一样流畅。
>

* 时间：04.14
* 论文：[AlayaDB: The Data Foundation for Efficient and Effective Long-context LLM Inference](https://arxiv.org/abs/2504.10326)

AlayaDB 提出面向长上下文 LLM 的统一数据底座：通过 KV-Cache 分块、向量索引与专用缓冲管理协同，将冷 KV 数据下沉至 CPU/SSD，热数据常驻 GPU；支持动态稀疏注意力查询（DIPR）、窗口缓存与上下文复用。实验在 ∞-Bench 43K–192K token 任务上，与全注意力相比 TTFT 最高提速 42×。AlayaDB 能够在保证服务等级目标（SLO）的同时，实现长上下文 LLM 推理的低资源消耗与高生成质量。

![](https://i.imgur.com/hPIz9Q4.png)



## 2025.05
### Rethinking Memory in AI【记忆建筑师】
> **记忆建筑师**：像一位系统化的档案管理员，把 AI 的“记忆”拆成“表示-操作-主题”三层架构，再给出六大原子操作的形式化公式，最后把记忆能力映射到四大研究主题，为下一代智能体提供可扩展、可解释、可演化的长期记忆蓝图。
>

* 时间：05.27
* 论文：[Rethinking Memory in AI: Taxonomy, Operations, Topics, and Future Directions](https://arxiv.org/abs/2505.00675)

论文把 AI 记忆重新梳理为“表示-操作-主题”三层架构：先区分参数记忆与情境记忆，再定义 Consolidation 等六大原子操作，随后将能力映射到长期记忆、长上下文、参数修改、多源融合四大主题，并盘点 50+ 数据集、90+ 方法与 Replika 到 Mem0 的完整工具链，最终指出统一评估、KV效率、跨模态冲突与终身学习仍是未来突破口。

![](https://i.imgur.com/lNcsT1Q.png)


## 2025.06
### Reasoning RAG【双系统智检】
> **双系统智检**：像一位既会“快思”又会“慢想”的侦探，把RAG拆成两条赛道——System 1用模块化流水线闪电出招，System 2让LLM自己决定何时、如何检索与反思；两者配合，既能稳定落地，又能应对开放世界的复杂推理。
>

* 时间：06.12
* 论文：[Reasoning RAG via System 1 or System 2: A Survey on Reasoning Agentic Retrieval-Augmented Generation](https://arxiv.org/abs/2506.10408)

Reasoning RAG 以“快思”式固定模块流水线与“慢想”式自主检索双轨并行。论文系统梳理两大范式下 Self-RAG、ReAct、DeepResearcher 等代表工作的架构、策略、工具及奖励设计，并指出现实 Web 环境端到端 RL 训练是通往可信、高效、开放世界推理 RAG 的关键。

![](https://i.imgur.com/86dsow4.png)

### RetroInfer【时光压缩器】
> **时光压缩器**：像一位把长篇连续剧剪成高能集锦的导演，先离线把整段 KV 历史切成“关键帧”存入向量仓库，推理时只回放与问题最相关的几幕，既保留剧情精髓，又把显存和算力开销压到最低，让超长上下文模型也能“秒回”任意时刻的细节。
>

* 时间：06.30
* 论文：[RetroInfer: A Vector-Storage Approach for Scalable Long-Context LLM Inference](https://arxiv.org/abs/2505.02922)

RetroInfer 将 KV-Cache 视为向量仓库，提出 Wave Index（注意力感知向量索引）与 Wave Buffer（异构内存调度器）。推理时先用 Wave Index 的三区近似（稳态区 + 检索区 + 估计区）挑出最关键 token，再让注意力仅在 1.8% KV 上精确计算，其余用质心估计，复杂度从 O(n²) 降到 O(k·n)。实验显示在长上下文任务上，解码吞吐比全注意力提升 4.5×，比现有稀疏注意力再快 10.5×，显存占用<5%，精度与全注意力持平。

![](https://i.imgur.com/Bxyx2kA.png)
