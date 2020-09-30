- 底层是从学者网抽取出来的知识图谱
- 接着通过图神经网络算法将事件抽取出来形成一层新的知识图谱，并且与旧的知识图谱有关系相连接



# 论文

- AAAI2018: **Graph convolutional networks with argument-aware pooling for event detection**

- - Author: Nguyen, Thien Huu and Grishman, Ralph
  - url: **[http://ix.cs.uoregon.edu/~thien/pubs/graphConv.pdf](https://link.zhihu.com/?target=http%3A//ix.cs.uoregon.edu/~thien/pubs/graphConv.pdf)**
  - DataSet: **[ACE2005 English Corpus](https://link.zhihu.com/?target=https%3A//catalog.ldc.upenn.edu/LDC2006T06)**
  - Keywords: GCN, Argument-aware Pooling

- **中文事件抽取研究综述**



------

# 知识点

- **事件抽取任务**：从非结构化的文本识别并抽取时间信息并结构化表示。

- **相关术语**：

  - **实体(entity):**语义类别中的一个或一组对象,包
    括人名、地名、组织机构、交通工具等。

  - **事件提及(event mention):**描述事件的短语或句
    子,包括事件触发词和事件元素。

  - **事件触发词(event trigger):**最清晰准确表达事件
    发生的关键词,通常是动词或名词。（**重要概念**）

  - **事件元素(event arguments):**参与一个具体事件
    的元素提及,包括概念、实体、数值、时间等。

  - **元素角色(argument roles):**事件元素与其参与事
    件的关系。

- **目前事件抽取的主流研究方向**
  - 深度学习
  - 神经网络（成功应用）
    - 全连接神经网络
    - 卷积神经网络
    - **循环神经网络**（未学）
	- **基于机器学习的方法**
     - 特征工程：将事件抽取任务建模为多分类问题，提取文本的语义特征，然后输入分类器进行事件抽取。
     - 常用的机器学习分类方法
      - 最大熵模型
      - 支持向量机模型
      - 隐马尔科夫模型
   - **基于神经网络的方法**
     - 神经网络方法将事件抽取建模成端到端的系统，使用包含丰富语言特征的**词向量**作为输入自动提取特征。
   - **弱监督的方法**

- **中文事件抽取的方法**
  - 目前存在的问题：
    - 中文语言太灵活，触发词数量远高于英文，导致测试集中存在训练集中没有出现过的**未知触发词**。