# S2-03-手撕LLAMA

相比于transformer,LLaMA做的改变
- 激活函数：SwiGLU:增强非线性表达的函数，改善了relu在接近0时不可导的问题
  ![image-1](https://api2.imubu.com/v3/document_image/9089822_afa15330-493b-4c80-f871-3e701c2e0337.png)
- ### LayerNorm层归一化改用RMS Norm
- RoPE旋转位置编码
- 只有解码器
- GQA
  - **MHA（多头注意力）**：每个 Query 头都有自己独立的 Key/Value 头。质量最好，但 KV Cache 最大。
  - **MQA（多查询注意力）**：所有 Query 头共享**唯一一组** Key/Value 头。KV Cache 最小，推理最快，但质量可能下降。
  - **GQA**：把 Query 头分成若干组，**每组共享一组 Key/Value**。在速度、显存和质量之间取得平衡。