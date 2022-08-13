# 简易分布式计算系统架构

（主要参考[tinysql](https://github.com/talent-plan/tinysql)和部分上课内容）

实现一个简易分布式计算系统最核心的部分：CLI、连接协议、SQL解析、优化器、执行器、多种支持算子、多机调度

在这里我们不考虑垃圾回收、高并发安全等拓展功能。

代码主要结构参考tinysql，在其基础上添加或删减功能，关于tinysql的资料几乎都在tinysql的库中能够找到。

难点：

* 实现MySQL协议
* Executor调度粒度（OLTP还是OLAP，Shuffle）
* 分布式事务支持
* 数据源处理（构建元数据）

## 运行＆使用

编译（可能需要换源）

~~~go
make
~~~

显示`Build TiDB Server successfully!`后运行服务

~~~bash
./bin/tidb-server
~~~

之后就可以用mysql协议直接连接了

~~~bash
mysql -h127.0.0.1 -P4000 -uroot
~~~

### 支持算子

目前只支持一些基本算子



## 代码结构

### 交互

举例：使用cobra工具（基于go语言）开发命令行工具，实现增删查改的反馈逻辑

| 文件 | 说明 | 备注 |
| :--: | :--: | :--: |
|      |      |      |
|      |      |      |
|      |      |      |

### 协议层|LB层

实现SQL的网络包收发，或许再实现Load Balancer

| 文件 | 说明 | 备注 |
| :--: | :--: | :--: |
|      |      |      |
|      |      |      |
|      |      |      |

### SQL处理

#### 解析

使用Lex & Yacc实现构建AST

| 文件 | 说明 | 备注 |
| :--: | :--: | :--: |
|      |      |      |
|      |      |      |
|      |      |      |

#### 验证

结合元数据分析SQL逻辑是否合理

| 文件 | 说明 | 备注 |
| :--: | :--: | :--: |
|      |      |      |
|      |      |      |
|      |      |      |

#### 编译

RBO优化：一大堆

CBO优化：非常难，因为涉及到统计信息的存储与收集

| 文件 | 说明 | 备注 |
| :--: | :--: | :--: |
|      |      |      |
|      |      |      |
|      |      |      |

### 执行器

#### 执行模型

火山模型：自顶向下的调用函数，数据就会被next函数自底向上的拉取出来，算子之间大量虚函数调用，开销大

向量化模型：传输数据为批次而不是单个数据

| 文件 | 说明 | 备注 |
| :--: | :--: | :--: |
|      |      |      |
|      |      |      |
|      |      |      |

#### 执行算子

调用算子计算并返回数据

| 文件 | 说明 | 备注 |
| :--: | :--: | :--: |
|      |      |      |
|      |      |      |
|      |      |      |

#### 获取数据

调用数据源接口（[Shuffle？](使用开源RPC框架实现mapreduce)）

| 文件 | 说明 | 备注 |
| :--: | :--: | :--: |
|      |      |      |
|      |      |      |
|      |      |      |

### 数据源和分布式

这里所指的分布式和Flink、Spark不同，SQL Server层只对接入客户端和分布式存储负责，多个计算节点之间的任务是相互独立的

如何调度读取在不同节点的不同partition的数据

| 文件 | 说明 | 备注 |
| :--: | :--: | :--: |
|      |      |      |
|      |      |      |
|      |      |      |



## 项目分工

|  姓名  | 负责模块 | 备注 |
| :----: | :------: | :--: |
|  崔颢  |          |      |
| 廖温建 |          |      |
| 李梓迦 |          |      |
| 梁程智 |          |      |
| 罗思琦 |          |      |
| 亓胜鹏 |          |      |
|  李季  |          |      |





