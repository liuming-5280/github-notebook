# LLM与AI工程基础

幻觉

提示词：软约束

AI全栈简单解读
- 详细解读
  ![image-1](https://api2.imubu.com/v3/document_image/9089822_d71bcd16-f7df-4946-ce9c-2fbe64ddc5d2.png)
  ![image-2](https://api2.imubu.com/v3/document_image/9089822_6c38266c-ddd1-40ef-8b1a-c0dd28da53b0.png)
  ![image-3](https://api2.imubu.com/v3/document_image/9089822_39b1a280-501b-43e0-b088-fc06b2a27c14.png)
  - RAG（Retrieval-Augmented Generation，检索增强生成）
    - 是一种先检索外部知识库、再把检索到的内容交给大语言模型生成回答的技术，用于提升准确性和时效性并减少幻觉。
  - SFT（Supervised Fine-Tuning，监督微调）
    - 是用人工标注的“输入-输出”示例对预训练模型进行有监督训练，让它学会按指令或特定任务格式生成回答
  - AI Infra（AI Infrastructure，人工智能基础设施）
    - 是支撑 AI 模型训练、推理、部署和运维的全套底层软硬件与平台，包括 GPU/TPU 算力、高速网络、存储、分布式训练框架、资源调度、推理服务和监控等。

python
- 字符串：print（f"{name}{age}岁了"）
- 列表：a.append(1) a=[]
- 字典：a={}
- 列表嵌套字典：a=[{"b"=2}]
- 函数:def name(bianliang):return 1
- 读写文件：
  ![image-1](https://api2.imubu.com/v3/document_image/9089822_42110260-09fd-4e43-8f66-042edbc319aa.png)
  ![image-2](https://api2.imubu.com/v3/document_image/9089822_fe427b61-0e2f-42d5-e31e-de43267144a1.png)

JSON
- JSONL
  ![image-1](https://api2.imubu.com/v3/document_image/9089822_41b95ee9-ad49-49b6-f031-e1e35e60a424.png)
  - `从 ROOT/data/questions.jsonl 文件里逐行读取 JSON 数据，跳过空行，解析每一行 JSON，并打印其中的 "question" 字段。`
    ![image-1](https://api2.imubu.com/v3/document_image/9089822_21c2a21d-55ed-4b0f-9444-f5f77f2936e0.png)
- JSONJavaScript Object Notation
  - 是一种文字表示数据的格式;用键值对和数组表示结构化数据
    ![image-1](https://api2.imubu.com/v3/document_image/9089822_27c3f11f-7f2e-463e-b383-1b06ca06a577.png)
  - ### json.loads(s)：JSON 字符串 → Python 字典/列表。
  - json.dump(字典)字典->文字
  - load装上；dump卸载

问题：
- 这是干啥的
  ![image-1](https://api2.imubu.com/v3/document_image/9089822_43d071a0-af13-4bbc-b7aa-debb456dc7d9.png)
- GIT下载

类
- 类的每个方法的第一个参数都是他自己self
- return f"我叫{name}或return "我叫 {}，今年 {} 岁".format([self.name](http://self.name/), self.age)
  ![image-1](https://api2.imubu.com/v3/document_image/9089822_470ef4dc-1e88-451a-d0ef-7d02fe9a632c.png)

@ dataclass
- 自动生成初始化方法
  - @ dataclass作为一个装饰类
    ![image-1](https://api2.imubu.com/v3/document_image/9089822_7aea60f6-061b-4e28-ba34-0f8f1a891edb.png)
    ![image-2](https://api2.imubu.com/v3/document_image/9089822_2cbc233a-fa2f-4892-e9c9-831fe11fc4e3.png)
  - 等价代码
    ![image-1](https://api2.imubu.com/v3/document_image/9089822_624dd4f1-6b1b-4d24-9861-32e41fcd8ef6.png)

@ property
![image-1](https://api2.imubu.com/v3/document_image/9089822_fcde5339-56cf-4b6f-ab83-e162402db198.png)
- 用@ property把一个方法伪装成字段：
  ![image-1](https://api2.imubu.com/v3/document_image/9089822_8689c9eb-01df-4448-d528-24c28d3f155e.png)
- ->bool**类型注解（Type Hints）只是一种“温馨提示”，并不会真正限制你**。
  ![image-1](https://api2.imubu.com/v3/document_image/9089822_0b573aae-24ea-49ca-93ad-378a8f06ff78.png)
- name:str
  ![image-1](https://api2.imubu.com/v3/document_image/9089822_e10f0ce8-4681-4af0-a4e9-939e25dcdfd7.png)
- 读作：greet接收一个字符串name和times,返回一个字符串
  ![image-1](https://api2.imubu.com/v3/document_image/9089822_e9a0dc5d-bff4-4c07-aff2-8eba558efe84.png)
-

