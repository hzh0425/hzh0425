## 前言


更新时间 2021 12 12


## 个人信息

姓名: 黄章衡

学校: 福州大学19级计算机系

邮箱: 642256541@qq.com

微信: hwuzheng


## 个人荣誉

- SOFAStack/SOFAJRaft contributor
- 2021 '开源软件供应链点亮计划' -- '突出贡献奖'
- TIDB / PD contributor
- 2021年 中国大学生服务外包创新创业大赛国家级 一等奖
- 2020年 泛珠三角 + 大学生计算机作品大赛 国家级二等奖
- 2021年 中国大学生移动应用创新赛华南赛区 一等奖
- 2021年 福州大学软件设计与服务外包创新创业竞赛 一等奖
- ...................



## 数据库研发经验

**1.CreatorStack/CreatorKv - -A distributed and fault-tolerant key-value storage** 

**主要工作:完成一款支持分布式事务的键值存储系统,开发语言: go**

- 根据Raft论文,实现了Raft模块,具备Leader选举,日志复制,Snapshot等基础功能,同时引入了Batch-Pipeline,

Read-Index等优化。

- 搭建了Multi-Raft架构,对数据基于Range进行分区,支持Region split和Region merge的功能。

- 搭建了Scheduler模块,通过Region心跳收集,对Region进行负载调度,平衡每个Store上的Regoin和Leader。

- 实现了Mvcc多版本并发控制,并基于Percolator模型,支持高性能分布式事务。

仓库地址:https://github.com/CreatorsStack/CreatorKv

**2.CreatorStack/CreatorDB-- Asimple Database management system** 

**主要工作:完成一款支持sql解析和优化的数据库管理系统, 开发语言:Java**

- 完成了基于HeapFile的数据存储功能,并具备BufferPool(基于LRU算法),支持Page缓存与淘汰功能。

- 基于Volcano火山模型,构建Operator执行树,同时具备各种常见的算子,如SortMergeJoin,Aggregation,Filter。

- 支持Sql解析和查询优化,基于Left-Deep-Tree和DynProgramming实现了Join优化器。

- 具备事务功能,基于Page粒度下的2PL协议以及DeadLockDetector,实现了事务的ACID特性。通过日志和Checkpoint机制,支持事务的回滚与恢复。

- 完成了B+树索引模块,支持查询,插入删除,以及页合并,页分裂的特性。

仓库地址:https://github.com/CreatorsStack/CreatorDB



## 开源贡献

### **SOFAStack / SOFAJRaft 社区**

**1.SOFAJRaft   -- 重构日志模块 (进行中)**

- 该项目为2021年暑期开源软件供应链点亮计划的高难度项目,并获得了'最佳开源贡献奖'的奖项

- 基于软件分层思想,构建了索引与数据存储一体化存储架构。

- 利用mmap内存映射技术,文件预分配,文件预热,组提交等,有效的提高了读写性能。

- 项目说明: https://summer.iscas.ac.cn/#/org/prodetail/210170433

- Pr 地址: https://github.com/sofastack/sofa-jraft/pull/696

- [详细文章地址](https://mp.weixin.qq.com/s?__biz=MzUzMzU5Mjc1Nw==&mid=2247497065&idx=1&sn=41cc54dbca1f9bb1d2e50dbd181f062d&chksm=faa31ab3cdd493a52bac26736b2d66c9fcda77c6591048ae758f9663ded0a1a068947a8488ab&mpshare=1&scene=23&srcid=1026H0gUsE1GGJq3hgzmKpGe&sharer_sharetime=1635251084804&sharer_shareid=4685e37971dd76c96606e8a800ad9755#rd)




**2.SOFAJRaft / Rheakv    -- 并行化状态机**

- 借鉴Mysql并行复制的特性,针对分布式状态机单线程执行的弊端,提出通用的多线程并行状态机,任何基于状态机的共识算法都能使用该思想构建多线程状态机。

- 基于BloomFilter+Dag有向无环图+高性能并发队列Disruptor。

- 通过批量提交与依赖检测,将无依赖的任务批次进行并行化执行。

- 显著的提高了Rheakv的吞吐量和并行度。

- Pr 地址: https://github.com/sofastack/sofa-jraft/pull/678
- Issue 地址:  https://github.com/sofastack/sofa-jraft/issues/614




**3.SOFAJRaft / Rheakv   -- 并行压缩日志**

- 描述: 基于 Common-compress 进行日志的并行化压缩与解压缩  

- Pr 地址: https://github.com/sofastack/sofa-jraft/pull/603
- Issue 地址: https://github.com/sofastack/sofa-jraft/issues/596





### TIDB 社区

**1.TIDB/PD -- Enhance Split Table Stability and Usability (进行中)**

描述: 该项目为 TIDB 社区 的 Tallent challenge program 2021 中的任务 , 主要负责在 PD 中新增一个接口, 使得 TIDB / 工具 可以直接通过 PD  进行 split and scatter table regions, 以提升稳定性和性能

Tracking issue: https://github.com/pingcap/tidb/issues/29034



## 实验室经历

本人在 2020年6月份 便加入了福州大学 <ACM服务外包协同创新 实验室>

在导师学长的引领下, 我积极参与了各类软件设计类竞赛, **并担任队伍队长, 拿下众多奖项。**

同时, 我为实验室尽心尽责, 较好的完成了多个实验室交给我的任务, 包括但不局限于:

- 较好的完成了 福建医科大学病例系统 后端工程。
- 作为负责人, 组织2021年暑期实验室举办的夏令营活动, 为实验室培养了各方面的优秀人才。
- 担任 Web 组后端组长, 引领学弟学妹学习 Java 技术, 为实验室培养了众多优秀的后端人才。
- 组织学弟学妹参与竞赛, 持续为实验室贡献奖状。
- .......................
