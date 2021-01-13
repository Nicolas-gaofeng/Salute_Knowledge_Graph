## 一、表示方式

属性图和传统的RDF格式都可以作为知识图谱的表示和存储方式，但二者还是有区别的。

目前来看，RDF主要还是用于学术的场景，在工业界我们更多的还是采用图数据库（比如用来存储属性图）的方式。

## 二、属性图

在现实世界中，实体和关系也会拥有各自的属性，比如人可以有“姓名”和“年龄”。当一个知识图谱拥有属性时，我们可以用属性图（Property Graph）来表示。

属性图的表达很贴近现实生活中的场景，也可以很好地描述业务中所包含的逻辑。

假设我们用知识图谱来描述一个事实（Fact） - “李明是李飞的父亲”。这里的实体是李明和李飞，关系是“父亲”（is_father_of）。当然，李明和李飞也可能会跟其他人存在着某种类型的关系（暂时不考虑）。当我们把电话号码也作为节点加入到知识图谱以后（电话号码也是实体），人和电话之间也可以定义一种关系叫 has_phone，就是说某个电话号码是属于某个人这个电话号开通时间是2018年，这里可以把时间作为属性（Property）添加到 has_phone 关系里来表示开通电话号码的时间。这种属性不仅可以加到关系里，还可以加到实体当中，类似的，李明本人也带有一些属性值比如年龄为25岁、职位是总经理等。当我们把所有这些信息作为关系或者实体的属性添加后，所得到的图谱称之为属性图 （Property Graph）。

![image-20210112171844579](https://gitee.com/zgf1366/pic_store/raw/master/img/20210112171844.png)

## 三、RDF

除了属性图，知识图谱也可以用RDF来表示，它是由很多的三元组（Triples）来组成。RDF在设计上的主要特点是易于发布和分享数据，但不支持实体或关系拥有属性，如果非要加上属性，则在设计上需要做一些修改。

RDF(Resource Description Framework)，即资源描述框架，是W3C制定的，用于描述实体/资源的标准数据模型。RDF图中一共有三种类型，International Resource Identifiers(IRIs)，blank nodes 和 literals。下面是SPO每个部分的类型约束：

1. Subject可以是IRI或blank node。
2. Predicate是IRI。
3. Object三种类型都可以。

IRI我们可以看做是URI或者URL的泛化和推广，它在整个网络或者图中唯一定义了一个实体/资源，和我们的身份证号类似。

literal是字面量，我们可以把它看做是带有数据类型的纯文本。

blank node简单来说就是没有IRI和literal的资源，或者说匿名资源。

## 四、深度学习表示方式

近年来，以深度学习为代表的表示学习技术取得了重要的进展，可以将实体的语义信息表示为稠密低维实值向量，进而在低维空间中高效计算实体、关系及其之间的复杂语义关联，对知识库的构建、推理、融合以及应用均具有重要的意义。graph embedding 就是一种表示学习。

## 五、知识图谱的存储

知识图谱主要有两种存储方式：一种是基于RDF的存储；另一种是基于图数据库的存储。

![image-20210112180811960](https://gitee.com/zgf1366/pic_store/raw/master/img/20210112180916.png)

### 5.1 RDF存储方式

RDF一个重要的设计原则是数据的易发布以及共享。其次，RDF以三元组的方式来存储数据而且不包含属性信息。

### 5.2 图数据库存储方式

图数据库把重点放在了高效的图查询和搜索上，图数据库一般以属性图为基本的表示形式，所以`实体和关系可以包含属性`，这就意味着更容易表达现实的业务场景。

如果设计的知识图谱带有属性，图数据库可以作为首选。但至于选择哪个图数据库也要看业务量以及对效率的要求。如果数据量特别庞大，则Neo4j很可能满足不了业务的需求，这时候不得不去选择支持准分布式的系统比如OrientDB, JanusGraph等，或者通过效率、冗余原则把信息存放在传统数据库中，从而减少知识图谱所承载的信息量。 通常来讲，对于10亿节点以下规模的图谱来说Neo4j已经足够了。

图数据库存储的特点：

- 包含节点和关系
- 节点可以有属性（键值对形式存储）
- 节点可以有一个或者多个标签
- 关系有名字和方向，并总是有一个开始节点和一个结束节点
- 关系也可以有属性

#### 5.2.1 Neo4j

数据库的划分

![image-20210112224520058](https://gitee.com/zgf1366/pic_store/raw/master/img/20210112224805.png)

##### 5.2.1.1 安装及部署

1. 进入官网：https://neo4j.com/download/?ref=try-neo4j-lp，点击下载 Neo4j server

![image-20210112225612614](https://gitee.com/zgf1366/pic_store/raw/master/img/20210112225612.png)

2. 然后找到对应自己的操作系统点击下载对应的社区版即可

![image-20210112225721772](https://gitee.com/zgf1366/pic_store/raw/master/img/20210112225721.png)

3. 下载完成后解压到主目录，“D:\Program Files\neo4j-community-4.2.”。

Neo4j应用程序有如下主要的目录结构：

- bin目录：用于存储Neo4j的可执行程序；
- conf目录：用于控制Neo4j启动的配置文件；
- data目录：用于存储核心数据库文件；
- plugins目录：用于存储Neo4j的插件；

4. 创建ne04j的环境变量

创建主目录环境变量NEO4J_HOME，并把主目录设置为变量值。

##### 5.2.1.2 网络连接配置

neo4j支持三种网络协议，默认情况下，不需要配置就可以在本地直接运行。

1. Neo4j支持三种网络协议（Protocol）

Neo4j支持三种网络协议（Protocol），分别是Bolt，HTTP和HTTPS，默认的连接器配置有三种，为了使用这三个端口，需要在Windows防火墙中创建Inbound Rules，允许通过端口7687，7474和7473访问本机。

![img](https://gitee.com/zgf1366/pic_store/raw/master/img/20210112234601.png)

2. 连接器的可选属性

![img](https://gitee.com/zgf1366/pic_store/raw/master/img/20210112234630.png)

listen_address：设置Neo4j监听的链接，由两部分组成：IP地址和端口号（Port）组成，格式是：<ip-address>:<port-number>

3. 设置默认的监听地址

设置默认的网络监听的IP地址，该默认地址用于设置三个网络协议（Bolt，HTTP和HTTPs）的监听地址，即设置网络协议的属性：listen_address地址。在默认情况下，Neo4j只允许本地主机（localhost）访问，要想通过网络远程访问Neo4j数据库，需要修改监听地址为 0.0.0.0，这样设置之后，就能允许远程主机的访问。

```text
# With default configuration Neo4j only accepts local connections.
# To accept non-local connections, uncomment this line:
dbms.connectors.default_listen_address=0.0.0.0
```

4. 分别设置各个网络协议的监听地址和端口

HTTP链接器默认的端口号是7474，Bolt链接器默认的端口号是7687，必须在Windows 防火墙中允许远程主机访问这些端口号。

```text
# Bolt connector
dbms.connector.bolt.enabled=true
#dbms.connector.bolt.tls_level=OPTIONAL
#dbms.connector.bolt.listen_address=0.0.0.0:7687

# HTTP Connector. There must be exactly one HTTP connector.
dbms.connector.http.enabled=true
#dbms.connector.http.listen_address=0.0.0.0:7474

# HTTPS Connector. There can be zero or one HTTPS connectors.
#dbms.connector.https.enabled=true
#dbms.connector.https.listen_address=0.0.0.0:7473
```

##### 5.2.1.3 启动Neo4j程序

1. 通过控制台安装Neo4j程序

点击组合键：Windows+R，输入cmd，启动DOS命令行窗口，切换到主目录，以管理员身份运行，输入以下命令，通过控制台启用neo4j程序

```bash
neo4j.bat console
```

如果出现以下提示，说明neo4j已经开始运行

![img](https://gitee.com/zgf1366/pic_store/raw/master/img/20210112231122.png)

2. 把Neo4j安装为服务（Windows Services）

安装和卸载服务：

```bash
bin\neo4j install-service
bin\neo4j uninstall-service
```

启动服务，停止服务，重启服务和查询服务的状态：

```bash
bin\neo4j start
bin\neo4j stop
bin\neo4j restart
bin\neo4j status
```

3. 打开浏览器输入地址http://localhost:7474  默认跳转到  http://localhost:7474/browser

默认用户名为neo4j，默认密码为neo4j，第一次成功connect到Neo4j服务器之后，需要重置密码。例如我改成了123456。

![image-20210112234247725](https://gitee.com/zgf1366/pic_store/raw/master/img/20210112234247.png)

**卸载：**

当我们需要卸载它的时候，会发现没有卸载的软件。

此时以管理员身份进入cmd，进入到./bin目录下，执行以下命令 ，就会自动停止服务并卸载。

注意一定要在管理员身份下进入cmd

win10下的操作是：开始菜单搜索栏中搜索cmd，右键，以管理员身份运行。

```bash
neo4j uninstall-service
```

##### 5.2.1.4 使用

![image-20210112185336155](https://gitee.com/zgf1366/pic_store/raw/master/img/20210112225019.png)



![image-20210112185340776](https://gitee.com/zgf1366/pic_store/raw/master/img/20210112225026.png)





### 5.3 如何选择存储方式

﻿根据最新的统计（2018年上半年），图数据库仍然是增长最快的存储系统。相反，关系型数据库的增长基本保持在一个稳定的水平。同时，我们也列出了常用的图数据库系统以及他们最新使用情况的排名。 其中 Neo4j 系统目前仍是使用率最高的图数据库，它拥有活跃的社区，而且系统本身的查询效率高，但唯一的不足就是不支持准分布式。相反，OrientDB和JanusGraph（原Titan）支持分布式，但这些系统相对较新，社区不如Neo4j活跃，这也就意味着使用过程当中不可避免地会遇到一些刺手的问题。如果选择使用RDF的存储系统，Jena或许一个比较不错的选择。

![image-20210112181105114](https://gitee.com/zgf1366/pic_store/raw/master/img/20210112181105.png)

 

 

 