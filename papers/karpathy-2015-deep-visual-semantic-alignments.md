Authors:Andrej Karpathy, Li Feifei
Field: Computer Vision, NLP, Multimodal Learning, Image Captioning

Research question:
Why this problem matters:
Method in plain English:
Key result:
What I still don't understand:
Connection to my own interests:



abstract:
一个可以根据image生成一句话text/根据image局部生成label的模型。
文字和图像align实现手段：图像（CNN），文字（bidirectional RNN），所有变量放进同一个空间比较相似度。
产出：先用 alignment model 推断图像区域和文字片段的对应关系，然后用这些 inferred alignments 训练 Multimodal RNN 去生成新的描述。 

（CNN（Convolutional Neural Network）：
看图extract特征的机器。
擅长处理图片、图像区域、视觉信息。
filters / kernels识别线条形状等pattern。

RNN（Recurrent Neural Network）：
擅长处理sequential data。
按顺序读并hidden state记忆

BRNN（Bidirectional RNN）：
两个方向同时读，每个字 contains information from both previous and following 
处理完整句子）

写作逻辑：提出任务--解决了什么问题/目标--方法/如何实现--结果

introduction：
人类看图能力很强 → 传统视觉模型太受限 → 以前 caption 方法也受限 → 本文目标是 dense descriptions → 难点是什么 → 核心思路是什么 → 两个贡献


为什么这个问题重要：人类的视觉理解能力很强，但对视觉识别模型很难实现

以前方法哪里不够：以前主流只能从fixed set里面labeling image，相比人类很受限。早期模型依赖人工模版，非常死板。

这篇论文想往哪里推进：generating dense descriptions of images

挑战/难点：
1.同时理解 image content 和 natural language representation 
2.网络大量 image-caption 数据，但不知道一个 caption 里混合提到了多个实体在图里的具体位置。

核心洞察：利用大量 image-sentence 数据，把句子当作 weak labels。推断这些对齐关系，然后用它们学习一个生成描述的模型

贡献：
1.开发了一个深度神经网络模型，用来推断句子片段和它们所描述的图像区域之间的潜在对齐关系。
2.提出了一个多模态 RNN 架构，输入图像，输出文字描述。后面还会利用 inferred correspondences 训练在 region-level annotations 上做区域描述
