# MMKG
## introduction
将符号与相应的图象，声音和视频数据联系起来，并将符号映射到物理世界中具有意义的相应参考实体。使机器在遇到特定的实体时，能够产生类似于真实世界的体验。
在关系提取任务中，附加图象通常会大大提高属性和关系提取的性能，这些属性和关系在视觉上很明显，但是在符号和文本中很难识别。
## 定义
原：关系三元组，属性三元组；新：定义一个特定的知识符号与其对应的知识项（图象声音或视频）相关联。
现有表示方式：将多模态数据作为实体或概念的特定属性值->A-MMKG;将多模态数据作为实体->N-MMKG:图象实体关联关系:contain;nearby;sameas;similar;
N-MMKG中，图象往往被抽象成图象描述符(图象描述符内积获取图象相似性)；
NEIL[22]通过预训练分类器用单个标签注释每个图像，并通过关于提取对象位置的启发式规则提取视觉关系。GAIA[21]通过对象识别和细粒度分类提取新闻中的细粒度概念。基于GAIA的框架，RESIN[23]提取视觉新闻事件，并将相关视觉实体和概念识别为小规模资源（新闻文档）的论据。后来，MMEKG[24]优化了一些模块，并适应了数十亿规模的通用事件提取。 
IMGpedia[25]通过已经在DBpedia Commons[26]中提取的RDF格式的结构化；
MMKG[28]通过在多个KG之间对齐实体，将该方法扩展到多个KG。这些基于符号实体对齐（例如通过链接的数据集或实体的URI）的构建方法关注图像的代表性，但由于不同的上下文和视图，图像的多样性也是一个重要问题。
多模态学习侧重于建模多模态之间的对应关系，包括：利用多模态的互补性来学习特征表示；多模态翻译学习从一种模态的源实例翻译到另一种模态中的目标实例；多模态对齐旨在找到不同模态之间的对应关系；多模态融合旨在结合来自不同模态的信息以执行预测；多模式联合学习旨在通过调整其他模式的资源来缓解特定模式中的低资源问题。
VL-PTMs could learn extensive implicit cross-modal knowledge with some designed self-supervised pre-training tasks, such as masked language model, sentenceimage alignment, masked region label classification, maskedregion features regression, masked object prediction, etc.
### 引入MMKG对多模态学习和VL-PTMs的帮助
提供背景知识，使用辅助常识知识来增强图象和文本的表示，以进行图像-文本匹配；MMKG能够理解图像中看不见的物体，符号知识通过提供关于不可见对象的符号信息或在可见对象和不可见对象之间建立语义关系来减轻困难；MMKG支持多模态可解释推理；MMKG通常提供多模态数据作为附加功能，以弥补某些NLP任务中的信息差距；MMKGs提供了显式和细粒度的跨模态相关知识，这是对VL-PTM学习的隐式知识的补充。
## 构建
大多数图像标签解决方案学习从图像内容到各种标签集的映射，包括对象、场景、实体、属性、关系、事件和其他符号。例如，NEIL[22]将图像链接到WordNet[3]，ImageSnippets[54]，[55]将图像链接至DBPedia[6]。
根据要链接的符号类别：视觉实体/概念抽取，视觉关系抽取，视觉事件抽取。
### 视觉实体/概念抽取
视觉实体（或概念）提取旨在检测和定位图像中的目标视觉对象，然后用KG中的实体（或理念）符号标记这些对象。挑战在于学习有效的细粒度提取模型，而不需要大规模、细粒度、注释良好的概念和图象实体数据集。
方法：1）对象识别；2）映射字幕中的单词或短语。
#### 对象识别
检测+分类；
#### visual grounding methods
该问题旨在定位字幕中每个短语的对应图像区域，以获得带有标签的视觉对象 ；
#### 机会
事实证明，基于数亿图像文本数据训练的VL PTM（如CLIP[41]）可以高精度识别许多受欢迎的实体，如名人和地标[73]。2） T轴索切开术延伸。一些具有多个合理标签的视觉对象表示不同的语义级别。
### 视觉关系提取 
视觉关系提取旨在识别图像中检测到的视觉实体（或概念）之间的语义关系，然后用KGs中的关系标记它们。视觉关系提取任务旨在识别KG中定义的更一般类型的语义关系。
#### 基于规则的关系提取
基于规则的关系提取。传统的基于规则的方法主要关注特定的关系类型，如空间关系和动作关系。专家通常预先确定标准，并通过启发式方法对判别特征进行评分和选择。 
#### 基于统计的关系提取
基于统计的方法将检测到的对象的视觉、空间和统计等特征编码为分布式向量，并通过分类模型预测给定对象之间的关系。
#### 机会
我们如何从三重场景信息中识别三重视觉知识。基于推理的关系检测。现有的关系检测方法通过融合视觉特征和语言先验的隐藏统一表示来预测关系。
### 视觉事件提取
一个事件包括一个触发器和几个参数及其参数角色。触发器是表示事件发生的动词或名词。参数角色是事件和参数之间的关系，参数是实体引用、概念或属性值。
具有多个子事件的视频事件提取。例如，事件“制作咖啡”分为一系列步骤，例如清洁咖啡机→ 倒入咖啡豆→ 打开咖啡机，每一步都可以视为一个事件。需要提取顺序步骤并按步骤的时间线列出，这些步骤很难用当前方法解决。  
### 从符号到图象：符号固定
实体固定：DBPidea符号实体->维基百科相应图像和数据->图片覆盖率较低；
另一种实体固定的方法：基于搜索引擎。
概念固定旨在找到具有代表性的有区别性的和多样性的图像。可视化概念判断、代表性图像选择和图像多样化。
### link pridiction
预测两个实体之间缺失的关系。传统的link pridiction由简单的排序过程来处理，该过程从所有的候选实体中找到最合适的组成三元组的实体，在预测阶段，根据得分函数进行rank，最终得到最匹配的实体。MMKGs中融合到实体和关系表示中的图像可以提供额外的视觉知识，以丰富嵌入信息。IMAGEgraph[27]提出将不可见图像和多关系图像检索之间的关系预测表示为视觉关系查询，以便这些查询可用于MMKG完成。类似地，MMKG[28]构建了三个数据集来预测实体之间的多关系关系，所有实体都与数字和视觉数据相关。
## 下游应用
### 多模态实体识别和链接
### Visual Question Answering
视觉问答（VQA）具有挑战性，需要对问题进行准确的语义分析，并深入理解给定图像中不同对象和场景之间的相关性。在最新的VQA基准数据集（如GQA[125]、OK-VQA[49]和KVQA[127]）中，许多问题需要结合外部知识的视觉推理。新提出的VQA任务弥补了人类可以很容易地结合来自各种模式的知识来回答视觉查询的差异。MMKGs中不同模态的实体和关系三元组可以表示为异构图中的节点和边，并以统一格式表示，这有助于使用启发式规则、SPARQL查询[128]或GNN节点之间的加权传递消息进行显式推理。
### 图像文本匹配
图像-文本匹配通常通过将文本和图像映射到联合语义空间中，然后学习统一的多模态表示来进行相似度计算来实现。一般方法是利用多标签检测模块来提取语义概念，然后将这些概念与图像的全局上下文融合[165]，[169]，[170]。MMKGs还可以帮助构建场景图，其引入视觉概念之间的信息相关性知识，并进一步增强图像表示。
### 多模态生成任务




