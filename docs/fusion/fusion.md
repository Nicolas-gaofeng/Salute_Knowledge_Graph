## 一、知识融合

知识融合是高层次的知识组织，使来自不同知识源的知识在同一框架规范下进行异构数据整合、消歧、加工、推理验证、更新等步骤，达到数据、信息、方法、经验以及人的思想的融合，形成高质量的知识库。

由于知识图谱中的知识来源广泛，存在知识质量良莠不齐、来自不同数据源的知识重复、知识间的关联不够明确等问题，所以必须要进行知识的融合。

知识融合又分为模式层的融合以及数据层的融合。

- 模式层的融合主要包括概念、概念的上下位、概念的属性这些统一
- 数据层的融合主要是将不同数据来源的数据的相同实体的不同表达形式进行融合，包括实体的合并、实体属性与关系的合并等。这一步工作涉及的技术有实体对齐、指代消解等。

### 1.1 实体统一

在实体命名识别和关系抽取过程中，比前两个问题更具挑战性的问题一个是实体统一，也就是说有些实体写法上不一样，但其实是指向同一个实体。比如“NYC”和“New York”表面上是不同的字符串，但其实指的都是纽约这个城市，需要合并。实体统一不仅可以减少实体的种类，也可以降低图谱的稀疏性（Sparsity）

![image-20210112174152241](https://gitee.com/zgf1366/pic_store/raw/master/img/20210112175042.png)

### 1.2 指代消解

比前两个问题更具挑战性的问题另一个是指代消解，也是文本中出现的“it”, “he”, “she”这些词到底指向哪个实体，比如在本文里两个被标记出来的“it”都指向“hotel”这个实体。

## 二、知识更新

知识更新是一个重要的部分。人类的认知能力、知识储备以及业务需求都会随时间而不断递增。因此，知识图谱的内容也需要与时俱进，不论是通用知识图谱，还是行业知识图谱，它们都需要不断地迭代更新，扩展现有的知识，增加新的知识。

从逻辑上看，知识库的更新包括概念层的更新和数据层的更新。

- 概念层的更新是指新增数据后获得了新的概念，需要自动将新的概念添加到知识库的概念层中。

- 数据层的更新主要是新增或更新实体、关系、属性值，对数据层进行更新需要考虑数据源的可靠性、数据的一致性（是否存在矛盾或冗杂等问题）等可靠数据源，并选择在各数据源中出现频率高的事实和属性加入知识库。

知识图谱的内容更新有两种方式：

- 全面更新：指以更新后的全部数据为输入，从零开始构建知识图谱。这种方法比较简单，但资源消耗大，而且需要耗费大量人力资源进行系统维护；
- 增量更新：以当前新增数据为输入，向现有知识图谱中添加新增知识。这种方式资源消耗小，但目前仍需要大量人工干预（定义规则等），因此实施起来十分困难。