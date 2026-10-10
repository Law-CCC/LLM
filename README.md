可以。这个资料库不应该做成普通的“大模型八股合集”，而应该做成：

> **LLM 基础八股 → RAG 专项八股 → Cook-RAG 项目八股 → 实验与指标 → 代码手撕 → 系统设计 → 大厂追问**

这样面试官从 Transformer 一路问到你的项目时，你能够形成完整的知识链。

你指定的 `tcsnyy/llm-interview-notes` 这类资料库的核心特点，就是按照知识模块组织题目，并针对每道题给出考察点、答题框架和参考答案；目前公开的 LLM 面试资料也普遍采用“基础 → 微调 → 推理 → RAG → Agent → 评测”等模块化结构。[GitHub](https://github.com/Imironman123/llm-interview-notes/blob/main/%E5%AD%97%E8%8A%82%E8%B7%B3%E5%8A%A8%E5%A4%A7%E6%A8%A1%E5%9E%8B%E9%9D%A2%E8%AF%95_%E9%9D%A2%E7%BB%8F%E4%B8%8E%E7%9C%9F%E9%A2%98%E5%A4%8D%E7%9B%98.md?utm_source=chatgpt.com)

下面我直接按照这个思路，为你的 **Cook-RAG 大模型算法实习项目**设计一套可以长期复习的资料库。

---

# Cook-RAG 大模型算法实习面试八股资料库

## 0. 资料库定位

这套资料库的目标不是单纯背八股，而是解决面试中最常见的一条链：

```text
大模型基础
    ↓
Transformer
    ↓
Embedding
    ↓
向量检索
    ↓
BM25
    ↓
Hybrid Retrieval
    ↓
RRF
    ↓
RAG
    ↓
Query Rewrite / Router
    ↓
Context Construction
    ↓
Generation
    ↓
RAG Evaluation
    ↓
RAGAS
    ↓
项目实验
    ↓
系统设计
    ↓
大厂项目追问
```

最终做到：

> **面试官问理论，你能回答理论；  
> 面试官问公式，你能推公式；  
> 面试官问代码，你能写；  
> 面试官问为什么这么设计，你能解释；  
> 面试官问实验，你能拿数据说话；  
> 面试官质疑指标，你能解释指标局限；  
> 面试官继续深挖，你还能往底层讲。**

---

# 一、推荐的 GitHub 仓库结构

建议最终整理成下面这样：

```text
cook-rag-llm-interview-notes/
│
├── README.md
│
├── 00-项目面试总览/
│   ├── 01-项目介绍.md
│   ├── 02-项目架构.md
│   ├── 03-项目一分钟介绍.md
│   ├── 04-项目三分钟介绍.md
│   ├── 05-项目亮点.md
│   └── 06-项目可能被质疑的问题.md
│
├── 01-大模型基础/
│   ├── 01-Transformer.md
│   ├── 02-Self-Attention.md
│   ├── 03-Multi-Head-Attention.md
│   ├── 04-FFN.md
│   ├── 05-LayerNorm.md
│   ├── 06-Residual.md
│   ├── 07-位置编码.md
│   ├── 08-Tokenizer.md
│   ├── 09-Causal-LM.md
│   ├── 10-Pretraining.md
│   └── 11-Loss与优化.md
│
├── 02-Embedding与向量检索/
│   ├── 01-Embedding.md
│   ├── 02-BGE.md
│   ├── 03-Cosine-Similarity.md
│   ├── 04-Euclidean-Distance.md
│   ├── 05-FAISS.md
│   ├── 06-ANN.md
│   ├── 07-HNSW.md
│   └── 08-向量检索常见问题.md
│
├── 03-传统信息检索/
│   ├── 01-BM25.md
│   ├── 02-TF-IDF.md
│   ├── 03-BM25-vs-Dense.md
│   └── 04-Sparse-Dense-Hybrid.md
│
├── 04-RAG/
│   ├── 01-RAG是什么.md
│   ├── 02-RAG完整流程.md
│   ├── 03-Chunking.md
│   ├── 04-Metadata.md
│   ├── 05-Parent-Child-Retrieval.md
│   ├── 06-Hybrid-Retrieval.md
│   ├── 07-RRF.md
│   ├── 08-Reranker.md
│   ├── 09-Query-Rewrite.md
│   ├── 10-Query-Router.md
│   ├── 11-Context-Construction.md
│   ├── 12-Context-Pruning.md
│   ├── 13-RAG幻觉.md
│   └── 14-RAG常见失败原因.md
│
├── 05-RAG评测/
│   ├── 01-为什么需要RAG评测.md
│   ├── 02-Precision@K.md
│   ├── 03-Recall@K.md
│   ├── 04-Hit@K.md
│   ├── 05-MRR.md
│   ├── 06-NDCG.md
│   ├── 07-Faithfulness.md
│   ├── 08-Answer-Relevancy.md
│   ├── 09-Answer-Correctness.md
│   ├── 10-RAGAS.md
│   └── 11-评测集构造.md
│
├── 06-Cook-RAG项目/
│   ├── 01-项目背景.md
│   ├── 02-项目架构.md
│   ├── 03-数据处理.md
│   ├── 04-检索系统.md
│   ├── 05-Query-Router.md
│   ├── 06-Query-Rewrite.md
│   ├── 07-Parent-Child.md
│   ├── 08-Generation.md
│   ├── 09-RAGAS.md
│   ├── 10-实验设计.md
│   ├── 11-结果分析.md
│   └── 12-项目不足.md
│
├── 07-项目高频面试题/
│   ├── 01-项目介绍题.md
│   ├── 02-RAG设计题.md
│   ├── 03-检索追问题.md
│   ├── 04-评测追问题.md
│   ├── 05-工程追问题.md
│   ├── 06-为什么这么做.md
│   └── 07-项目压力面.md
│
├── 08-手撕代码/
│   ├── 01-Self-Attention.py
│   ├── 02-Softmax.py
│   ├── 03-Cross-Entropy.py
│   ├── 04-KL-Divergence.py
│   ├── 05-BM25.py
│   ├── 06-Cosine-Similarity.py
│   ├── 07-RRF.py
│   ├── 08-Precision-Recall-MRR.py
│   └── 09-TopK.py
│
├── 09-系统设计/
│   ├── 01-设计一个企业RAG.md
│   ├── 02-设计一个知识库问答系统.md
│   ├── 03-百万文档RAG.md
│   ├── 04-高并发RAG.md
│   └── 05-RAG质量监控.md
│
├── 10-大厂真题/
│   ├── 01-字节跳动.md
│   ├── 02-阿里巴巴.md
│   ├── 03-腾讯.md
│   ├── 04-美团.md
│   └── 05-快手.md
│
└── 11-项目复习清单/
    ├── 01-一面.md
    ├── 02-二面.md
    ├── 03-三面.md
    └── 04-终面.md
```

这个结构和成熟的 LLM 面试资料库思路是一致的：把 Transformer、Tokenization、推理、微调、RAG、评测等拆成独立模块，而不是全部堆在一个 Markdown 文件里。[GitHub](https://github.laiyagushi.com/wdndev/llm_interview_note?utm_source=chatgpt.com)

---

# 二、README.md

下面这份可以直接作为这个资料库的首页。


# Cook-RAG LLM Interview Notes

> 面向大模型算法工程师 / 大模型应用算法 / RAG 算法实习岗位的项目型面试复习资料库。

本资料库围绕个人项目 **Cook-RAG** 构建，不仅整理大模型基础知识，同时将 Transformer、Embedding、BM25、Hybrid Retrieval、RRF、Query Rewrite、RAGAS、评测指标等知识点与实际项目实现进行关联。

目标不是“背八股”，而是做到：

> **理解原理 → 能写公式 → 能写代码 → 能解释项目 → 能分析实验 → 能回答追问。**

---

## 1. 项目核心

Cook-RAG 是一个面向菜谱知识问答场景的检索增强生成系统。

整体流程：

```text
用户 Query
    ↓
Query Router
    ↓
Query Rewrite
    ↓
Metadata Filter
    ↓
┌───────────────┐
│               │
BM25          FAISS
│               │
└───────┬───────┘
        ↓
    Hybrid Retrieval
        ↓
        RRF
        ↓
 Parent Document Mapping
        ↓
 Context Construction
        ↓
 Context Pruning
        ↓
      LLM
        ↓
     Answer
        ↓
     RAGAS
```

---

## 2. 核心技术

### 大模型

- Transformer
- Self-Attention
- Causal LM
- Tokenization
- Cross Entropy
- KL Divergence
- Adam

### Embedding

- Sentence Embedding
- BGE
- Cosine Similarity
- Vector Search
- FAISS
- ANN

### Retrieval

- BM25
- Dense Retrieval
- Hybrid Retrieval
- Reciprocal Rank Fusion
- Metadata Filtering
- Parent-Child Retrieval

### Query Understanding

- Query Routing
- Query Rewrite
- Query Classification

### Generation

- Context Construction
- Context Pruning
- Prompt Engineering
- Grounded Generation

### Evaluation

- Precision@K
- Recall@K
- Hit@K
- MRR
- NDCG
- Faithfulness
- Answer Relevancy
- Answer Correctness
- RAGAS

---

## 3. 当前项目实验结果

当前 20 条测试集的结果：

| 指标 | 当前结果 |
|---|---:|
| Evaluation Samples | 20 |
| RAGAS Success Rate | 100% |
| Retrieval Hit@3 | 95% |
| Source Recall | 95% |
| Faithfulness | 0.657 |
| Answer Relevancy | 0.858 |
| Answer Correctness | 0.517 |

需要特别注意：

当前代码统计的 Retrieval Hit@K / Source Recall 并不等价于 Precision@K 或 MRR。

因此面试时不能把：

> Hit@3 = 0.95

说成：

> Precision@3 = 0.95。

后续应补充 Precision@K、Recall@K、MRR 等严格检索指标。

---

## 4. 面试核心目标

面试官可能沿着以下路径深入：

```text
项目介绍
 ↓
为什么做 RAG？
 ↓
为什么不用 Fine-tuning？
 ↓
为什么 BM25 + Dense？
 ↓
为什么 BGE？
 ↓
为什么 FAISS？
 ↓
为什么 Hybrid？
 ↓
为什么 RRF？
 ↓
为什么 Query Rewrite？
 ↓
为什么 Parent-Child？
 ↓
为什么 Context Pruning？
 ↓
为什么 Faithfulness 只有 0.657？
 ↓
为什么 Correctness 只有 0.517？
 ↓
如何做 Ablation？
 ↓
如何提高 Recall？
 ↓
如何提高 Precision？
 ↓
如何降低延迟？
 ↓
百万级文档怎么办？
 ↓
高并发怎么办？
 ↓
如何证明你的方案优于 Baseline？
```

这也是本资料库最重要的复习路径。

---

## 5. 学习原则

每个问题按照以下结构回答：

### ① 一句话定义

先告诉面试官“是什么”。

### ② 原理

说明“为什么”。

### ③ 数学公式

能够公式化就公式化。

### ④ 工程实现

说明“代码怎么做”。

### ⑤ 项目映射

说明“Cook-RAG 中怎么用”。

### ⑥ 优缺点

说明“为什么不是另一个方案”。

### ⑦ 实验

说明“怎么证明有效”。

### ⑧ 追问

提前准备面试官下一层问题。

---

## 6. 最终目标

不是记住 300 道题。

而是形成：

```text
一个项目
+
一套理论
+
一套代码
+
一套实验
+
一套指标
+
一套系统设计
```

最终可以独立完成大模型算法实习面试中的：

- 项目介绍
- RAG 原理
- 检索算法
- 大模型基础
- 评测
- 手撕代码
- 系统设计
- 实验分析
- 项目追问


---

# 三、第一章：大模型基础

这一章是**面试官验证你是不是“真正懂大模型”**的地方。

---

## Q1：Transformer 为什么能够替代 RNN？

### 考察点

- Transformer
- Attention
- 并行计算
- 长距离依赖

### 标准回答

RNN 按时间步递归计算：

$$
h_t=f(x_t,h_{t-1})
$$

因此当前 token 必须依赖前一个时间步，训练过程难以完全并行。

Transformer 使用 Self-Attention：

$$
Attention(Q,K,V)=softmax\left(\frac{QK^T}{\sqrt{d_k}}\right)V
$$

所有 token 可以同时参与计算，因此训练阶段具有更好的并行性。

同时 Self-Attention 可以直接建立任意两个 token 之间的依赖关系，因此相比 RNN 更容易建模长距离依赖。

---

## Q2：Self-Attention 为什么要除以 $\sqrt{d_k}$？

这是非常典型的大模型面试题。

假设：

$$
q_i,k_i\sim N(0,1)
$$

那么：

$$
q^Tk=\sum_{i=1}^{d_k}q_ik_i
$$

其方差大约为：

$$
Var(q^Tk)=d_k
$$

因此 $d_k$ 增大以后，点积结果的方差也会增大。

如果直接进入 Softmax：

$$
softmax(QK^T)
$$

容易产生非常尖锐的概率分布。

Softmax 进入饱和区域之后梯度变小。

所以使用：

$$
\frac{QK^T}{\sqrt{d_k}}
$$

把方差控制在相对稳定的范围。

### 面试追问

**为什么不能除以 $d_k$？**

因为希望把方差从 $d_k$ 缩放到常数量级，而不是缩放得过小。

标准差和维度之间是：

$$
\sigma\propto\sqrt{d_k}
$$

所以除以：

$$
\sqrt{d_k}
$$

而不是 $d_k$。

---

# 四、第二章：Embedding

这是 Cook-RAG 必问模块。

---

# Q3：什么是 Embedding？

Embedding 是把离散文本映射到连续向量空间。

例如：

```text
宫保鸡丁怎么做？
        ↓
[0.12, -0.37, 0.81, ...]
```

语义相近的文本，在向量空间中通常距离更近。

例如：

```text
宫保鸡丁怎么做？
宫保鸡丁的制作方法是什么？
宫保鸡丁需要哪些步骤？
```

应该具有较高的语义相似度。

Cook-RAG 使用：

```text
BAAI/bge-small-zh-v1.5
```

生成文本向量，再使用 FAISS 进行向量检索。

---

# Q4：为什么 RAG 不直接使用 BM25？

这是你的项目非常重要的问题。

### BM25 优势

BM25 属于稀疏检索。

它非常擅长：

```text
关键词精确匹配
实体名称
菜名
专有名词
```

例如：

```text
“宫保鸡丁”
```

BM25 对“宫保鸡丁”这个词的匹配非常直接。

### Dense Retrieval 优势

Dense Retrieval 更关注语义。

例如：

```text
“鸡肉怎么做成宫保口味？”
```

即使文本中没有完全出现：

```text
宫保鸡丁怎么做
```

Embedding 也可能认为两者语义相近。

所以：

```text
BM25
+
Dense Retrieval
```

能够形成互补。

---

# Q5：为什么使用 BGE？

回答不要只说：

> BGE 效果好。

应该回答：

BGE 属于专门用于文本表示和检索场景的 Embedding 模型。

相比直接使用生成模型的 hidden states，专门训练的 embedding 模型更加适合：

- semantic similarity
- dense retrieval
- document retrieval

同时 Cook-RAG 属于中文菜谱场景，因此选择中文 Embedding 模型能够减少跨语言表示带来的额外问题。

---

# 五、第三章：BM25

## Q6：BM25 的公式是什么？

BM25：

$$
score(D,Q)=\sum_{t\in Q}IDF(t)\cdot\frac{f(t,D)(k_1+1)}{f(t,D)+k_1\left(1-b+b\frac{|D|}{avgdl}\right)}
$$

其中：

- \(f(t,D)\)：词 \(t\) 在文档中的出现次数
- \(IDF(t)\)：逆文档频率
- \(|D|\)：文档长度
- \(avgdl\)：平均文档长度
- \(k_1\)：词频饱和参数
- \(b\)：文档长度归一化参数

---

# Q7：为什么 BM25 比 TF-IDF 更适合搜索？

BM25 相比 TF-IDF 做了两个重要改进。

### 第一：TF 饱和

一个词出现 1 次和出现 10 次，不应该让相关性无限增加。

BM25 使用：

$$
\frac{f(k_1+1)}
{f+k_1}
$$

实现词频饱和。
- 第一次出现，分数会增加
- 第二次、第三次出现，增加幅度会越来越小
- 词出现很多次以后，贡献不会无限制地继续增长

### 第二：文档长度归一化

长文档天然更容易出现关键词。

BM25 通过：

$$
1-b+b\frac{|D|}{avgdl}
$$

进行长度修正。

---

# 六、第四章：Hybrid Retrieval

## Q8：什么是 Hybrid Retrieval？

Hybrid Retrieval 是同时使用：

```text
Sparse Retrieval
+
Dense Retrieval
```

然后进行融合。

Cook-RAG：

```text
Query
 ├── BM25
 │
 └── FAISS
      ↓
    RRF
      ↓
Final Ranking
```

---

# Q9：为什么不能简单把 BM25 分数和向量相似度直接相加？

这是非常好的追问。

因为两种检索算法的 score 不一定在同一个尺度上。

例如：

```text
BM25 score：
1.2
5.8
13.4
```

而 cosine similarity：

```text
0.71
0.83
0.92
```

如果：

\[
score=BM25+cosine
\]

BM25 很可能在数值尺度上占据主导。

因此需要：

- normalization
- weighted fusion
- rank fusion

Cook-RAG 使用 RRF，可以避免直接比较两个不同 scoring space。

---

# 七、第五章：RRF

## Q10：RRF 是什么？

RRF：

> Reciprocal Rank Fusion

核心思想不是比较不同检索器的原始 score，而是比较：

> **文档在不同检索结果中的排名。**

公式：

$$
RRF(d)=\sum_{r\in R\frac{1}{k+rank_r(d)}}
$$

其中：

- \(d\)：文档
- \(r\)：检索器
- \(rank_r(d)\)：文档在检索器中的排名
- \(k\)：平滑参数

---

# Q11：RRF 为什么有效？

例如：

BM25：

```text
A
B
C
D
```

Dense：

```text
C
A
E
B
```

A 同时进入两个检索器的前列。

C 也是如此。

因此：

```text
A
C
B
```

这类结果会被融合到前面。

RRF 的优势是：

> 不要求 BM25 和 Dense 的原始 score 在同一尺度。

---

# 八、第六章：RAG

## Q12：什么是 RAG？

RAG：

> Retrieval-Augmented Generation

基本思想：

```text
Query
 ↓
Retriever
 ↓
Relevant Documents
 ↓
LLM
 ↓
Answer
```

让模型在生成答案之前获取外部知识。

相比单纯依赖模型参数，可以：

- 使用最新知识
- 使用私有知识
- 降低部分幻觉
- 不需要重新训练模型

---

# Q13：RAG 为什么可以降低幻觉？

这里不能回答：

> RAG 可以解决幻觉。

这是错误的。

正确回答：

RAG 只能通过提供外部证据，**降低一部分知识性幻觉**。

最终答案仍然由 LLM 生成。

因此可能出现：

```text
Retrieval 正确
        ↓
Context 正确
        ↓
LLM 错误理解
        ↓
错误答案
```

所以你的项目中才需要：

```text
Retrieval Evaluation
+
Generation Evaluation
```

分别测：

```text
Precision
Recall
MRR
        +
Faithfulness
Correctness
Relevancy
```

---

# 九、第七章：Chunking

## Q14：为什么 RAG 必须 Chunk？

因为原始文档通常太长。

假设一篇菜谱：

```text
菜名
食材
步骤1
步骤2
步骤3
注意事项
营养信息
```

如果整个 Markdown 直接 Embedding：

```text
一个 embedding
```

会导致局部语义被稀释。

例如：

```text
“什么时候放盐？”
```

真正相关的可能只有：

```text
步骤3
```

因此需要切分。

---

# Q15：Chunk 太大有什么问题？

```text
Chunk ↑
↓
语义信息更多
↓
Recall 可能提高
```

但：

```text
Chunk ↑
↓
无关信息 ↑
↓
Noise ↑
↓
Context 变长
↓
LLM 处理成本 ↑
```

---

# Q16：Chunk 太小有什么问题？

```text
Chunk ↓
↓
信息不完整
↓
语义断裂
↓
Retrieval Recall ↓
```

所以 Chunking 本质是：

> Recall、Precision、Context Length 三者之间的 trade-off。

---

# 十、第八章：Parent-Child Retrieval

这是你项目比较值得讲的一个点。

## Q17：为什么要 Parent-Child Retrieval？

假设：

```text
Parent Document

宫保鸡丁
├── 食材
├── 步骤1
├── 步骤2
├── 步骤3
└── 注意事项
```

Child：

```text
步骤2：加入花生米……
```

检索时：

```text
Query
 ↓
Child Chunk
 ↓
找到 Parent
 ↓
返回完整菜谱
```

这样：

### Retrieval

保持粒度小。

### Generation

保持上下文完整。

因此解决：

> 检索粒度和生成粒度之间的矛盾。

---

# 十一、第九章：Query Rewrite

## Q18：为什么需要 Query Rewrite？

用户的问题可能并不适合直接检索。

例如：

```text
“那个鸡肉菜怎么做？”
```

Query Rewrite：

```text
“鸡肉菜的制作方法和步骤”
```

可以提高检索效果。

---

## Q19：Query Rewrite 会不会导致信息损失？

会。

例如：

```text
原始 Query：
“宫保鸡丁不用花生可以吗？”
```

错误 Rewrite：

```text
“宫保鸡丁怎么做？”
```

那么：

```text
“不用花生”
```

这个关键约束就丢失了。

因此 Query Rewrite 不是：

> 越激进越好。

而是：

> 在保留原始意图和约束的情况下提高检索表达能力。

---

# 十二、第十章：Query Router

Cook-RAG 可以根据 Query 类型进行路由：

```text
list
detail
general
```

例如：

```text
“有哪些川菜？”
        ↓
list

“宫保鸡丁怎么做？”
        ↓
detail

“鸡肉适合怎么处理？”
        ↓
general
```

---

# Q20：为什么需要 Router？

因为不同问题的：

```text
检索策略
+
生成策略
+
Prompt
```

可能不同。

例如：

### List Query

用户需要：

```text
多个结果
```

### Detail Query

用户需要：

```text
具体步骤
```

如果所有 Query 都使用同一个 Prompt：

```text
统一检索
+
统一生成
```

容易造成：

- 信息冗余
- 生成格式不稳定
- 不同任务之间性能互相影响

---

# 十三、第十一章：Context Pruning

## Q21：为什么不能把 Top-K 全部扔给 LLM？

因为：

```text
Top-K ↑
↓
Context Length ↑
↓
Noise ↑
↓
推理成本 ↑
↓
注意力分散
```

所以需要：

> Context Pruning。

即：

```text
Retrieved Documents
        ↓
Relevant Content
        ↓
Final Context
        ↓
LLM
```

---

# Q22：Context Pruning 和 Retrieval 有什么区别？

这是一个很重要的面试问题。

### Retrieval

解决：

> **哪些文档值得拿回来？**

### Context Pruning

解决：

> **拿回来以后，哪些内容真正需要给 LLM？**

因此：

```text
Retrieval
= document-level filtering

Context Pruning
= context-level filtering
```

---

# 十四、第十二章：RAG 评测

这是你的项目最容易被深挖的部分。

---

# Q23：为什么 RAG 不能只看最终答案对不对？

因为 RAG 是一个 Pipeline：

```text
Query
 ↓
Retrieval
 ↓
Context
 ↓
Generation
 ↓
Answer
```

最终答案错了，不知道究竟是谁的问题。

可能是：

### Retrieval Error

正确文档没有检索到。

### Ranking Error

正确文档检索到了，但是排名太靠后。

### Context Error

正确文档存在，但是 Context 构造错误。

### Generation Error

Context 正确，但是 LLM 生成错误。

因此需要分层评测。

---

# 十五、Precision@K

## Q24：Precision@K 是什么？

\[
Precision@K
=
\frac{
|\text{Relevant}\cap\text{Retrieved}_K|
}{
K
}
\]

例如：

Gold：

```text
A B
```

Retrieved@5：

```text
A C D E F
```

那么：

```text
Precision@5 = 1/5 = 0.2
```

---

# 十六、Recall@K

$$
Recall@K=\frac{|\text{Relevant}\cap\text{Retrieved}_K|}{|\text{Relevant}|}
$$

上面的例子：

```text
Gold = A B
Retrieved = A C D E F
```

因此：

```text
Recall@5 = 1/2 = 0.5
```

---

# 十七、Precision 和 Recall 的核心区别

一句话：

> Precision 关心“拿回来的东西有多少是对的”。

> Recall 关心“应该拿回来的东西拿回来多少”。

RAG 中：

```text
Recall 低
→ 正确知识根本没回来
→ LLM 再强也没用
```

而：

```text
Precision 低
→ 噪声很多
→ LLM 更容易受到干扰
```

因此 RAG 通常需要同时优化：

```text
Recall
+
Precision
```

而不是只追求一个。

---

# 十八、MRR

## Q25：什么是 MRR？

Mean Reciprocal Rank。

单个 Query：

$$
RR=\frac{1}{rank}
$$

如果：

```text
第一名就是正确答案
```

那么：

$$
RR=1
$$

如果：

```text
正确答案排名第三
```

那么：

$$
RR=\frac13
$$

如果没有找到：

$$
RR=0
$$

最后：

$$
MRR=
\frac1N
\sum_{i=1}^{N}RR_i
$$

---

# Q26：为什么 RAG 需要 MRR？

因为 Recall 只告诉你：

> 找没找到。

但是不告诉你：

> 排在第几。

例如：

```text
系统 A：

正确文档：
第 1 名
```

系统 B：

```text
正确文档：
第 10 名
```

如果 K=10：

```text
Recall@10
```

两个系统可能都是：

```text
1.0
```

但是显然 A 更好。

MRR 就可以区分这种情况。

---

# 十九、NDCG

如果面试官继续追问：

> “那 MRR 只能看第一个 relevant document，多个 relevant documents 怎么办？”

就可以引出：

> NDCG。

NDCG 可以考虑多个相关文档以及它们的排序位置。

因此：

```text
Hit@K
↓
Recall@K
↓
MRR
↓
NDCG
```

是非常自然的一条面试追问链。

---

# 二十、RAGAS

## Q27：RAGAS 是什么？

RAGAS 是用于 RAG 系统评估的一套框架。

你的项目当前主要使用：

```text
Faithfulness
Answer Relevancy
Answer Correctness
```

同时自己统计 Retrieval：

```text
Hit@K
Source Recall
```

后续应补充：

```text
Precision@K
Recall@K
MRR
```

---

# 二十一、Faithfulness

## Q28：Faithfulness 是什么？

它关注：

> 答案中的内容是否能够被提供的 Context 支持。

例如：

Context：

```text
鸡肉需要腌制10分钟。
```

Answer：

```text
鸡肉需要腌制10分钟。
```

Faithfulness 高。

如果 Answer：

```text
鸡肉需要腌制30分钟。
```

但是 Context 没有这个信息。

那么 Faithfulness 会下降。

---

# 二十二、为什么你的 Faithfulness = 0.657？

这是你项目必须能够解释的问题。

不能直接说：

> RAG 效果不好。

应该拆解：

```text
Retrieval
    ↓
95% Hit@3
    ↓
说明多数 Query 至少找到相关 source
```

但：

```text
Source Hit
≠
Context 完全正确
```

可能存在：

### 1. Top-K 中存在噪声

相关文档找到了，但是同时加入了无关文档。

### 2. Parent Document 太长

检索到 Child 后映射到 Parent。

虽然保证了完整性，但也可能带入：

```text
无关步骤
+
其他信息
```

### 3. Context Construction

检索结果经过组合后，可能出现：

```text
重复
+
冗余
+
信息冲突
```

### 4. Generation Hallucination

即使 Context 正确：

```text
LLM
↓
错误推断
```

仍然可能降低 Faithfulness。

因此：

> Hit@3 = 95% 并不能推出 Faithfulness 必然很高。

---

# 二十三、为什么 Correctness 只有 0.517？

这是项目最重要的实验分析题。

首先区分：

```text
Faithfulness
=
答案有没有根据 Context 说

Correctness
=
答案和 Reference 是否真正一致
```

因此：

```text
Faithfulness = 0.657
Correctness = 0.517
```

说明一个非常值得分析的现象：

> 模型生成的答案有相当一部分是基于检索上下文生成的，但与标准参考答案之间仍存在明显差异。

可能原因：

### 原因 1：Reference 与真实知识存在表达差异

例如：

Reference：

```text
先炒香葱姜蒜，再加入牛肉。
```

模型：

```text
先将牛肉炒至变色，然后加入葱姜蒜。
```

语义可能部分正确，但与 Reference 存在顺序差异。

---

### 原因 2：Generation Context 不完整

Retrieval Hit：

```text
1
```

不代表：

```text
完整答案需要的信息全部存在。
```

例如：

```text
Query：
宫保鸡丁具体怎么做？
```

检索到了：

```text
食材
步骤1
步骤2
```

但是：

```text
步骤3
步骤4
```

没有进入最终 Context。

模型只能自行补全。

于是：

```text
Faithfulness ↓
Correctness ↓
```

---

### 原因 3：模型自身知识与 Context 混合

模型可能：

```text
Context
+
Parametric Knowledge
```

一起生成。

如果自身知识与当前菜谱不一致：

```text
Correctness ↓
```

---

### 原因 4：评测模型本身存在判断偏差

RAGAS 的 Answer Correctness 不是传统字符串 exact match。

它本身依赖 LLM-based evaluation，因此存在：

- evaluator bias
- semantic judgment bias
- reference sensitivity

所以：

> 0.517 并不能简单解释成“答案只有 51.7% 正确”。

---

# 二十四、项目实验应该怎么做？

这是面试官很喜欢问的问题。

不能只跑一次：

```text
Hybrid + Rewrite + Router
```

然后说：

> 效果很好。

必须做 Ablation。

---

# 二十五、推荐 Ablation

建议：

```text
Baseline
    ↓
BM25
    ↓
Dense
    ↓
BM25 + Dense
    ↓
BM25 + Dense + RRF
    ↓
+ Query Rewrite
    ↓
+ Metadata Filter
    ↓
+ Parent-Child
    ↓
+ Context Pruning
```

然后比较：

| 方法 | Precision@K | Recall@K | MRR | Faithfulness | Correctness |
|---|---:|---:|---:|---:|---:|
| BM25 | | | | | |
| Dense | | | | | |
| Hybrid | | | | | |
| Hybrid+RRF | | | | | |
| +Rewrite | | | | | |
| +Filter | | | | | |
| +Parent | | | | | |
| +Pruning | | | | | |

这张表比单纯说：

> 我用了 BM25 + FAISS + RRF。

有价值得多。

---

# 二十六、项目最重要的面试题库

下面是你真正应该重点背的。

---

## A. 项目介绍类

### Q1

**请介绍一下你的 Cook-RAG 项目。**

### Q2

**为什么做这个项目？**

### Q3

**项目最大的技术难点是什么？**

### Q4

**为什么选择 RAG，而不是 Fine-tuning？**

### Q5

**你的项目和普通 RAG 有什么区别？**

### Q6

**你的项目创新点是什么？**

### Q7

**整个系统的数据流是什么？**

### Q8

**项目中哪个模块是你自己设计的？**

### Q9

**如果让你重新做一次，你会怎么设计？**

---

# 二十七、检索类

### Q10

为什么 BM25？

### Q11

为什么 Dense Retrieval？

### Q12

为什么两个都要？

### Q13

为什么用 BGE？

### Q14

为什么用 FAISS？

### Q15

FAISS 的原理是什么？

### Q16

Flat、IVF、HNSW 有什么区别？

### Q17

为什么不用 Milvus？

### Q18

为什么不用 Elasticsearch？

### Q19

BM25 和 Dense 哪个更好？

正确回答：

> 没有绝对结论，需要通过数据集进行 Ablation。

---

# 二十八、RRF 类

### Q20

为什么 RRF？

### Q21

RRF 和加权平均有什么区别？

### Q22

RRF 的公式？

### Q23

RRF 的 \(k\) 是什么？

### Q24

RRF 有没有缺点？

有。

例如：

- 只考虑 rank
- 不利用原始 score 的置信度
- 不同 Retriever 的质量差异没有直接建模

---

# 二十九、RAG 类

### Q25

RAG 的完整流程是什么？

### Q26

RAG 为什么会出现幻觉？

### Q27

RAG 一定比 Fine-tuning 好吗？

不一定。

### Q28

什么时候 Fine-tuning？

### Q29

什么时候 RAG？

### Q30

什么时候 RAG + Fine-tuning？

---

# 三十、Chunking 类

### Q31

为什么 Chunk？

### Q32

Chunk Size 怎么选？

### Q33

Overlap 为什么需要？

### Q34

Overlap 太大会怎么样？

### Q35

Overlap 太小会怎么样？

### Q36

为什么使用 Markdown Header Chunking？

---

# 三十一、Parent-Child 类

### Q37

Parent-Child Retrieval 为什么有效？

### Q38

Parent 太大怎么办？

### Q39

Child 太小怎么办？

### Q40

为什么不直接检索 Parent？

核心回答：

> Parent 粒度太粗会降低检索精度。

---

# 三十二、Query Rewrite 类

### Q41

为什么 Rewrite？

### Q42

Rewrite 会不会引入错误？

### Q43

Rewrite 的成本是什么？

### Q44

Rewrite 什么时候应该关闭？

例如：

```text
Query 已经非常明确
```

不一定需要 Rewrite。

---

# 三十三、评测类

### Q45

为什么 Hit@K 不够？

### Q46

Precision@K 和 Recall@K 的区别？

### Q47

MRR 为什么重要？

### Q48

NDCG 和 MRR 的区别？

### Q49

Faithfulness 和 Correctness 的区别？

### Q50

Relevancy 是什么？

### Q51

RAGAS 是否可靠？

正确回答：

> RAGAS 适合作为自动化评测工具，但不能完全替代人工评测。

---

# 三十四、你的结果为什么不好？

这个问题非常可能出现。

面试官：

> “你这个 Faithfulness 只有 0.657，Correctness 只有 0.517，你怎么好意思写这个项目？”

不要防御。

应该回答：

> 这组结果反而帮助我定位了系统的主要瓶颈。目前 Retrieval Hit@3 和 Source Recall 都达到 0.95，说明多数 Query 至少能够召回相关 source，因此第一阶段的瓶颈已经不完全是“有没有召回”，而更多出现在召回结果的精确性、Context 构造以及 Generation 阶段。
>
> 具体来看，Faithfulness 只有 0.657，说明部分回答没有完全被最终提供给模型的 Context 支撑；Correctness 更低，说明即使回答基于 Context 生成，与 reference answer 之间仍存在明显差异。
>
> 下一步我会进一步拆成 Retrieval、Context、Generation 三层进行错误归因，并增加 Precision@K、Recall@K、MRR，同时进行 BM25、Dense、Hybrid、RRF、Query Rewrite、Metadata Filter 和 Context Pruning 的 Ablation，而不是只看最终答案指标。

这个回答比：

> “因为模型不够强。”

强很多。

---

# 三十五、手撕代码

这部分建议单独建立一个章节。

---

## 1. 手撕 Softmax

必须会：

$$
softmax(x_i)=\frac{e^{x_i}}{\sum_j e^{x_j}}
$$

并知道为什么需要：

```python
x = x - x.max()
```

防止：

```text
exp(x)
```

数值溢出。

---

# 三十六、手撕 Cross Entropy

语言模型：

$$L
=-\frac1N\sum_i\log P(y_i|x_{<i}
$$

要理解：

```text
logits
↓
softmax
↓
probability
↓
log
↓
negative
↓
loss
```

---

# 三十七、手撕 KL Divergence

$$
D_{KL}(P||Q)=\sum_x P(x)\log\frac{P(x)}{Q(x)}
$$

必须知道：

```text
KL(P||Q)
≠
KL(Q||P)
```

KL 不对称。

---

# 三十八、手撕 Cosine Similarity

$$
cos(x,y)=\frac{x\cdot y}{||x||||y||}
$$

RAG 中：

```text
Query Embedding
        ↓
Cosine Similarity
        ↓
Document Embedding
```

---

# 三十九、手撕 RRF

必须能在白板上写：

```python
for rank, doc in enumerate(results):
    score[doc] += 1 / (k + rank + 1)
```

然后解释：

```text
多个 Retriever
↓
rank
↓
reciprocal rank
↓
fusion
```

---

# 四十、手撕 Precision / Recall / MRR

必须能自己实现：

```text
precision_at_k()
recall_at_k()
mrr()
```

并且能回答：

> 如果没有 relevant document 怎么办？

```text
RR = 0
```

---

# 四十一、系统设计题

## Q52：如果让你设计一个企业级 RAG，你怎么设计？

推荐回答：

```text
                User Query
                    │
                    ↓
              Query Analysis
                    │
          ┌─────────┴─────────┐
          ↓                   ↓
       Rewrite              Router
          │                   │
          └─────────┬─────────┘
                    ↓
             Metadata Filter
                    ↓
          ┌─────────┴─────────┐
          ↓                   ↓
        BM25                Dense
          │                   │
          └─────────┬─────────┘
                    ↓
                   RRF
                    ↓
                 Reranker
                    ↓
             Parent Retrieval
                    ↓
            Context Pruning
                    ↓
                   LLM
                    ↓
             Grounded Answer
                    ↓
                Evaluation
```

然后继续讨论：

```text
缓存
权限
多租户
向量数据库
高并发
监控
日志
数据更新
Embedding 更新
索引重建
模型降级
```

---

# 四十二、百万级文档怎么办？

面试官：

> “你的 FAISS 如果变成一千万甚至一亿文档怎么办？”

不能回答：

> “换成 Milvus。”

要继续讲：

```text
数据规模
↓
ANN
↓
分片
↓
索引
↓
Metadata Filtering
↓
Candidate Retrieval
↓
Reranking
```

例如：

```text
10M Documents

        ↓

Metadata Filter

        ↓

ANN Top-100

        ↓

Reranker Top-20

        ↓

LLM Top-5
```

这样才能体现算法思维。

---

# 四十三、高并发怎么办？

考虑：

### 1. Embedding Cache

相同 Query 不重复计算。

### 2. Retrieval Cache

热点 Query 缓存检索结果。

### 3. LLM Batch

提高 GPU 利用率。

### 4. Streaming

降低用户感知延迟。

### 5. Model Quantization

降低推理成本。

### 6. vLLM

提高 LLM serving throughput。

### 7. Async Pipeline

让：

```text
Retrieval
+
Generation
+
Logging
```

减少不必要的同步阻塞。

---

# 四十四、为什么不用 LoRA？

这个问题尤其要准备，因为你之前考虑过 LoRA，后来决定不采用。

标准回答：

> 当前 Cook-RAG 的主要问题并不是模型缺少领域知识，而是 Retrieval 和 Context 构造。因此我优先通过 RAG 解决知识注入问题，而不是通过 LoRA 修改模型参数。
>
> 如果模型在正确 Context 下仍然存在稳定的任务格式问题、领域表达问题或者特定任务能力不足，再考虑 LoRA 等参数高效微调。

这个回答非常重要。

因为它体现：

> **先定位问题，再选择技术。**

而不是：

> “因为现在流行 LoRA，所以我用了 LoRA。”

---

# 四十五、项目创新点应该怎么回答？

不要说：

> “我的创新是用了 RAG。”

这没有价值。

应该说：

### 1. Hybrid Retrieval

```text
BM25
+
Dense
+
RRF
```

利用 lexical 和 semantic retrieval 的互补性。

### 2. Query-aware Pipeline

通过：

```text
Router
+
Rewrite
```

针对不同 Query 类型采用不同处理路径。

### 3. Parent-Child Retrieval

解决：

```text
检索粒度
vs
生成粒度
```

之间的矛盾。

### 4. Evaluation-driven Optimization

不是只看最终答案，而是：

```text
Retrieval
↓
Context
↓
Generation
```

分层评估。

---

# 四十六、字节 / 阿里面试最容易出现的“灵魂拷问”

这部分建议单独背。

---

## Q：你这个项目到底有什么技术含量？

回答：

> 我认为项目的技术含量主要不在于简单调用一个向量数据库，而在于对 RAG Pipeline 的完整优化和评测。
>
> 我把系统拆成 Query Understanding、Retrieval、Context Construction 和 Generation 四个阶段，并分别引入 Query Rewrite、BM25 + Dense Hybrid Retrieval、RRF、Parent-Child Retrieval 和 Context Pruning。
>
> 同时没有只使用最终答案作为评价，而是进一步拆成 Retrieval Metrics 和 Generation Metrics，通过 Hit@K、Recall、MRR、Faithfulness、Relevancy、Correctness 定位系统瓶颈。

---

## Q：如果只让你保留一个模块，你保留哪个？

比较好的回答：

> 如果目标是保证系统的基本能力，我会优先保留高质量 Retrieval，因为生成模型的能力存在上限，但如果正确知识没有进入 Context，Generation 很难恢复。

---

## Q：如果只能优化一个指标？

不能直接说：

> Correctness。

应该回答：

> 要根据错误分析决定。如果当前 Recall 明显不足，我会优先 Recall；如果 Recall 已经较高但 Faithfulness 和 Correctness 较低，我会进一步分析 Precision、Context Noise 和 Generation，而不是盲目继续增加 Top-K。

---

# 四十七、最重要的“为什么”链

你的整个项目最终应该能够回答这一串：

```text
为什么 RAG？
↓
为什么 Chunk？
↓
为什么 Markdown Header Chunking？
↓
为什么 Embedding？
↓
为什么 BGE？
↓
为什么 BM25？
↓
为什么 Dense？
↓
为什么 Hybrid？
↓
为什么 RRF？
↓
为什么 Query Rewrite？
↓
为什么 Router？
↓
为什么 Parent-Child？
↓
为什么 Context Pruning？
↓
为什么不能直接 Top-K？
↓
为什么需要 RAGAS？
↓
为什么需要 Retrieval Metrics？
↓
为什么 Hit@K 不够？
↓
为什么需要 Recall？
↓
为什么需要 Precision？
↓
为什么需要 MRR？
↓
为什么 Faithfulness 低？
↓
为什么 Correctness 更低？
↓
怎么做 Ablation？
↓
怎么证明优化有效？
```

**这条链才是你这个项目真正的面试主线。**

---

# 四十八、最终项目知识图谱

建议你把整个资料库最终压缩成下面这张知识图：

```text
                    LLM
                     │
        ┌────────────┴────────────┐
        │                         │
    Transformer                Generation
        │                         │
 ┌──────┼──────┐                  │
 ↓      ↓      ↓                  │
Attention FFN Norm                │
        │                         │
        └──────────┬──────────────┘
                   ↓
                  RAG
                   │
       ┌───────────┼───────────┐
       ↓           ↓           ↓
   Query理解    Retrieval    Context
       │           │           │
   Router       BM25         Parent
   Rewrite      Dense        Pruning
                  │
                 RRF
                  │
                  ↓
              Generation
                  │
                  ↓
               Evaluation
                  │
       ┌──────────┴───────────┐
       ↓                      ↓
 Retrieval Metrics       Generation Metrics
       │                      │
 Precision@K              Faithfulness
 Recall@K                 Relevancy
 MRR                      Correctness
 NDCG
```

---

# 四十九、你的项目八股复习优先级

如果目标是**字节 / 阿里大模型算法实习**，不要平均用力。

## S级：必须熟练

```text
★★★★★

Transformer
Attention
Embedding
Cosine Similarity
BM25
Dense Retrieval
Hybrid Retrieval
RRF
RAG
Chunking
Parent-Child
Query Rewrite
RAG Evaluation
Precision
Recall
MRR
Faithfulness
Correctness
```

## A级：必须理解

```text
★★★★☆

FAISS
ANN
HNSW
IVF
Reranker
NDCG
Metadata Filtering
Context Pruning
Prompt Engineering
Hallucination
RAG vs Fine-tuning
```

## B级：需要知道

```text
★★★☆☆

LoRA
DPO
RLHF
PPO
GRPO
KV Cache
vLLM
Quantization
Distillation
Agent
Function Calling
MCP
```

原因很简单：

**你的项目本质是 RAG 项目，而不是训练大模型项目。**

所以面试官更可能从：

```text
RAG
↓
Retrieval
↓
Embedding
↓
Evaluation
```

向下深挖，而不是突然让你讲完整的 GRPO 源码。

---

# 五十、最终面试准备路线

建议把这套资料库按四轮复习。

### 第一轮：理论

```text
Transformer
↓
Embedding
↓
BM25
↓
RAG
↓
RAGAS
```

目标：

> 每个概念可以脱稿解释。

---

### 第二轮：项目

```text
Cook-RAG
↓
Architecture
↓
Data
↓
Retrieval
↓
Generation
↓
Evaluation
```

目标：

> 每个模块都能指到代码和设计原因。

---

### 第三轮：实验

必须形成：

```text
Baseline
↓
BM25
↓
Dense
↓
Hybrid
↓
RRF
↓
Rewrite
↓
Filter
↓
Parent
↓
Pruning
```

对应：

```text
Precision@K
Recall@K
MRR
Faithfulness
Relevancy
Correctness
```

目标：

> 面试官问“你怎么证明有效”，可以直接拿实验说话。

---

### 第四轮：压力面

重点练：

```text
为什么不用 Fine-tuning？
为什么不用 Reranker？
为什么不用 Milvus？
为什么不用 Elasticsearch？
为什么用 BGE？
为什么用 RRF？
为什么 Recall 高但 Correctness 低？
为什么 Faithfulness 只有 0.657？
你的创新在哪里？
你的实验是否可信？
你的数据集怎么构造？
Reference 怎么来的？
20 条数据够吗？
如何扩大到 1000 条？
如果线上 QPS 1000 怎么办？
如果知识库 1 亿文档怎么办？
如果 LLM 换成更强模型怎么办？
如果不允许调用外部 API 怎么办？
```

---

## 最终定位

你这个资料库最终不要变成“背 300 道题”，而应该形成一个**项目驱动型大模型算法面试知识库**：

> **基础八股负责证明你懂模型；  
> RAG 八股负责证明你懂算法；  
> Cook-RAG 负责证明你做过项目；  
> Ablation 负责证明你会实验；  
> 手撕代码负责证明你能实现；  
> 系统设计负责证明你能落地；  
> 压力面负责证明你不是只会背答案。**

这套组织方式也符合目前主流 LLM 面试资料库将 **基础、推理、微调、RAG、Agent、评测、系统设计和真实面经**分模块整理的方式。[GitHub](https://github.com/Lau-Jonathan/LLM-Agent-Interview-Guide?utm_source=chatgpt.com)

**下一步真正需要做的是把上面这个目录中的每一个 `.md` 文件全部展开成“题目 → 考察点 → 标准答案 → 数学公式 → 项目代码 → 面试官追问 → 深挖答案 → 易错点”的完整内容。**这样才真正达到你指定的 `llm-interview-notes` 那种“资料库”级别，而不是一个目录大纲。
