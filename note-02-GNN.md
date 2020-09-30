#  GNN综述

- [机器之心公众号文章介绍](https://mp.weixin.qq.com/s?__biz=MzA3MzI4MjgzMw==&mid=2650755237&idx=1&sn=2dd0468552e69057681eec58fd265cbb&chksm=871a94dbb06d1dcd90451b17cc94a38811619fd49c07f1d1cf1909436746bae9b79717c345b2&mpshare=1&scene=1&srcid=0927KXOGWXh1rtKAvxB6F8Dm&sharer_sharetime=1601193294657&sharer_shareid=8657153b269bef7b4c6080deddd43a1f&key=694ad12351d974dc52249d2a6a4636168a498f04baec4a66c253a722c5b1286ad5768860e838d3c910039ac4462275dc954b8af0ab4c6a34097878ee0409c7787602bec28917713484d33249202f82c0950d3f109675dbc138d22e7fc01a230ff65b5a1a616cfd58b06922e912237022037a106c835cbb1f0f793b3ab8a71a8d&ascene=1&uin=MTgxMDcyNjc4Mg%3D%3D&devicetype=Windows+10+x64&version=62090538&lang=zh_CN&exportkey=A3XOtAlQIj%2FgoHf1N4eoYPw%3D&pass_ticket=PXlIJPr8dFl2DZ5EYLNOz5vZJCQbL7sm0UQSUTnnRcI2ZPKutFTZp%2BJ5OCdJeAIx&wx_header=0)

- [论文：A Comprehensive Survey on Graph Neural Networks](https://arxiv.org/pdf/1901.00596v1.pdf)

- **常用符号合集**
  ![img](https://mmbiz.qpic.cn/mmbiz_png/KmXPKA19gWibiaV87Z36x7bhhtHI8tib9FC6TQK0rM9XjHgsibia4Rrw8AlDRmxlibPJzqfYjQPwAUicPZbh6JY3TvcxA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

- **框架**
  ![img](https://mmbiz.qpic.cn/mmbiz_png/KmXPKA19gWibiaV87Z36x7bhhtHI8tib9FCibyxxPcRQSxK10Shu8pwaUiboMydGM2AWN747AcudTcT3BnSCo9ewZ4Q/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

- **数据集**
  ![img](https://mmbiz.qpic.cn/mmbiz_png/KmXPKA19gWibiaV87Z36x7bhhtHI8tib9FCarlmI1PWv4Lqz4Dy4yCFpiaiaibj9PibFQdcrYfEib7qOicibSyPUWA5VdfGQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

- **基准Benchmark(用相同的数据集)和开源实现**
  ![img](https://mmbiz.qpic.cn/mmbiz_png/KmXPKA19gWibiaV87Z36x7bhhtHI8tib9FCHwDBAA5LHFY08iapltNNrDFKlEwpM8aZwjfd4OnibHb8AsyMol4lQylQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

  *表 6：各种方法在四种最常用数据集上的基准性能。以上列出的方法都使用相同的训练、验证和测试数据集进行评估。*

  - **基准的作用**：相同的数据集在新模型上跑才有说服力、比较性

  ![img](https://mmbiz.qpic.cn/mmbiz_png/KmXPKA19gWibiaV87Z36x7bhhtHI8tib9FCCEGiayvOnib6W2D1jJopCdOibXGTluKibgMCdwy7ZfBJRa1xEmRLWVrF7w/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

- GNN领域文章整合的resp：**
  https://github.com/thunlp/GNNPapers

-----------

- ![image-20200927204639533](D:\docs\myDocs\第一学期\paper\img\0202.png)	
  比较受欢迎的两种模型：GAT/GCN

----------

# GNN模型

* **谱域卷积**(Spectral Graph Theory)
  ![image-20200928102541920](D:\docs\myDocs\第一学期\paper\img\0204.png)

  **正向学习过程**：$g_{\theta}(\Lambda)$ 为待学习参数(绿框)，$g_{\theta}(·)$可以为任意的函数，比如$g_{\theta}(L)=log(1+L)=L - L^2/2 + L^3/3+....$， 时间复杂度 $O(N)$ , 与图节点数量有关，这是不好的事情。其中$L = D - A, L为拉普拉斯式，D为度矩阵，A为邻接矩阵$ /

  - 如果$g_{\theta}(L) = L，则 y = Lx$ ：
    ![image-20200928103813522](D:\docs\myDocs\第一学期\paper\img\0205.png)

    图的各个节点的：

    ![image-20200928103903250](D:\docs\myDocs\第一学期\paper\img\0206.png)

    可以看到$L[0][3]=0$ ，刚好可以反应出v3对v0没信号影响（甚至很小）。

  - 如果$g_{\theta}(L) = L^2，则 y = L^2x$ ：
    ![image-20200928104236923](D:\docs\myDocs\第一学期\paper\img\0207.png)

    这样会导致模型**只考虑了全局而没有考虑局部**。

* **切比雪夫**(ChebNet)

  * 将$g_{\theta}(L)$设为多项式
    	$g_{\theta} = \sum_{k=0}^K\theta_kL^k$

    此时

    ​	$y=Ug_{\theta}(\Lambda)U^Tx=U(\sum_{k=0}^K\theta_kL^k)U^Tx$

    可以解决全局与局部的问题，但是**计算复杂度为$O(N^2)$**

  - 解决方式（神奇操作）：

    将$g_{\theta}(\Lambda)=\sum_{k=0}^K\theta_kL^k$换成$g_{\theta'}(\hat{\Lambda})=\sum_{k=0}^K\theta_k’T_k(\hat{\Lambda)}$

    ![image-20200928110804371](D:\docs\myDocs\第一学期\paper\img\0208.png)

    ![image-20200928110903524](D:\docs\myDocs\第一学期\paper\img\0209.png)

    ![image-20200928110931465](D:\docs\myDocs\第一学期\paper\img\0210.png)

    其中$[\theta_0'\theta_1'...\theta_K']$是要**学习的参数**，$[\bar{x_0} \bar{x_1}...\bar{x_K}]$ 是由递归的方式算出的。

* **GCN**

  ![image-20200928111249302](D:\docs\myDocs\第一学期\paper\img\0211.PNG)

  ![image-20200928111320688](D:\docs\myDocs\第一学期\paper\img\0212.png)

  **最核心的式子：**

  $h_v = f(\frac{1}{|N_(v)|}\sum_{u\in N(v)}W_{x_u}+b), \forall v\in V$

  若要更新某个节点的参数，则需要把所有节点的参数（包括自己）经过filter后得到的W都相加起来，取个平均值(N(v)是节点数)，加上偏执项b，送入激活函数f后可得。

-------------

# GNN总结
[B站李宏毅讲深度学习](https://www.bilibili.com/video/BV1JE411g7XF?p=19)

![image-20200928094829395](D:\docs\myDocs\第一学期\paper\img\0203.png)

- GAT和GCN是当下比较流行的图卷积神经网络模型；
- 尽管GCN数学上可行，但一般都忽略数学证明；
- GNN（或GCN）都**随着层数变深**而丢失了信息；
- 许多深度学习模型为了适配图数据，都做了细微的修改和设计，比如Deep Graph InfoMax, Graph Transformer和GraphBert；
- 针对当下的信息丢失问题的**理论分析**是未来需要解决的问题；
- GNN可以应用在众多任务上。