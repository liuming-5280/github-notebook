# S2-02-Transformer&MOE

RNN
- 特点：**有“记忆”**，当前时刻的输出不仅取决于当前输入，还取决于之前的信息
- 缺点：梯度消失，顺序进行；长距离信息丢失

LSTM
- 特点：：LSTM 多了一个**细胞状态** CtCt，像一条“记忆传送带”，可以在时间步之间传递信息。它用三个门来控制信息流：
  - **遗忘门**：决定丢掉哪些旧信息；
  - **输入门**：决定写入哪些新信息；
  - **输出门**：决定输出哪些信息。
- 缺点：计算量大；不能并行计算，串行效率低；

Tranformer
- 输入准备阶段：把数据分解为token，然后Embedding成向量，然后放在矩阵里（postional Encoding位置编码）位置编码
  - Embedding [ɪm'beding]嵌入
    - 把文字、图片、用户、商品等token对象，变成一串连续的数字向量，让计算机能计算它们之间的相似关系。是RAG的基础
    - 词向量的表征
      - one hot[0.1.0.0.0...]
        - 相乘除以模的夹角无法表征词向量之间的关系
        - 稠密词向量：余弦相似度
  - RAG（Retrieval-Augmented Generation，检索增强生成）[rɪˈtriːvl]取回[ɔ:g'mentɪd]增加
    - 是一种让大模型在回答前先从外部知识库检索相关信息，再结合检索内容生成答案的技术，由 Facebook AI Research 在 2020 年提出，用于提升回答准确性、时效性与专业性。--幻觉：自信的给出合理但是不真实的答案
- 编码器*n---阅读理解---衍生BERT：理解类任务
  - 输入：词嵌入 + 位置编码
  - 每层：多头自注意力 → 残差连接+层归一化 LN→ 前馈网络FFN → 残差+层归一化
    - 多头自注意力机制
      - 考虑别的token对当前向量的影响，让其能够在高纬度的向量里表达语义特征
      - Q*K/^dk保证将数值进行缩小，再用sofemax归一化
      - 自注意力，多头注意力，掩码注意力
        ![image-1](https://api2.imubu.com/v3/document_image/9089822_7573fb3e-5b61-4618-e635-837dc7b517c2.png)
      - QKV
        ![image-1](https://api2.imubu.com/v3/document_image/9089822_3b5e22dd-c466-408b-9474-fbed74a1d78f.png)
        - Q查询向量：Q*K很大就是Q和K 的关系大
      -
    - 残差链接+层归一化
      - 层归一化使向量乘积稳定在0-1分布里面
      - 残差连接-为了防止原始信息丢失
        - 残差连接就是**每一层人传话的时候，除了把话往下传，还要把最开始的原话也直接抄一份，一起传到后面。在RNN里有**
      - 跳过不好的训练层，直接将输入*权重+输出->下一层，解决了层数增加训练效果下降的困境
        - 在残差之前做层 归一化LayerNorm
    - FFN+层归一化
      ![image-1](https://api2.imubu.com/v3/document_image/9089822_e4900b8c-21c0-4011-cae2-c4a20b7b45a3.png)
      - 对每个词的向量，FFN 做三步---引入非线性：
        - **先升维**：线形层；对于经过上层的残差链接和归一化的向量，把向量变大，比如 768 维 → 3072 维。
        - **过激活函数**：非线性层，ReLu/GELU，让模型能学复杂模式。
        - **再降维**：线性层，变回原来的大小，比如 3072 维 → 768 维。
        - 进行残差链接：输出=输入+FFN
        - 输出
      - FFN在应用中的作用
        ![image-1](https://api2.imubu.com/v3/document_image/9089822_75dcfb85-3c08-4370-f1dd-004e07dbc3bc.png)
  - BERT--阅读理解机器
    - 缩写解释
      - Bidirectional--[ˌbaɪdɪˈrekʃ(ə)nəl]--双向的
      - Encoder-- [ɪn'kəʊdə]--编码器
      - Representations--[ˌreprɪzenˈteɪʃ(ə)n]--表示；代表；陈述
      - from Transformers--转换器
    - 任务1：MLM 掩码语言模型--Masked Language Model
      - 把句子里的一些词遮住，让模型猜原来是什么。【完型填空】
    - 任务2：NSP 下一句预测--Next Sentence Prediction
      - 给两句话，让模型判断它们是不是连续的。【句子接龙】
- 解码器*n---负责写--自回归生成--衍生GPT
  - 输入：目标序列嵌入 + 位置编码
  - 每层：掩码多头自注意力 → 残差+LN → 编码器-解码器注意力 → 残差+LN → FFN → 残差+LN
- 输出阶段
  - Linear  [ˈlɪniər]a.线性的
  - Softmax
- 注意力机制的三种衍生架构
  ![image-1](https://api2.imubu.com/v3/document_image/9089822_85de1b1e-15e7-49a7-96e6-71a0a24a289b.png)

GPT**生成式预训练变换器**
- **Generative 生成式**：它能生成新内容，比如写文章、回答问题、翻译、写代码。
  ![image-1](https://api2.imubu.com/v3/document_image/9089822_8d2abd4e-fa74-43fd-9f88-695bd66ae103.png)
- **Pre-trained [treɪnd]预训练**：先在海量文本上学习语言规律，比如预测“下一个词”是什么。
- **Transformer 变换器**：一种神经网络架构，核心是“自注意力机制”，能处理长文本并理解词与词之间的关系。

prompt提示
![image-1](https://api2.imubu.com/v3/document_image/9089822_69c214fa-b1c8-4e97-9486-055a2ae5a085.png)

MOE**Mixture of Experts，[ˈmɪkstʃə(r)] [ˈekˌspɜrt]混合专家就是模型里养了很多个“专家小网络”**
- deeepseek
- 有很多FFN
  ![image-1](https://api2.imubu.com/v3/document_image/9089822_b95f6433-ddcc-4057-b53e-f33ff22cc099.png)
- share expert sparse Moe
  ![image-1](https://api2.imubu.com/v3/document_image/9089822_a41ec261-b0a6-4393-de82-2f5c4a828aab.png)
- corpus--NLP语料库