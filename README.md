- [1. 个人信息](#个人信息)
- [2. 个人荣誉](#个人荣誉)
- [3.实习经历](#实习经历)
  - [3.1 Tencent](#tencent)

- [4. 开源贡献](#开源贡献)
  - [4.1 Apache / Rocketmq](#apache--rocketmq)
    - [1.支持 HA 主从切换](#1支持-ha-主从切换)
  - [4.2 Pingcap / TiFlash](#pingcap--tiflash)
  - [4.3 SOFAStack / SOFAJRaft](#sofastack--sofajraft)
    - [1.SOFAJRaft   -- 构建日志存储模块](#1sofajraft------构建日志存储模块)
    - [2.SOFAJRaft / Rheakv    -- 并行化状态机](#2sofajraft--rheakv-------并行化状态机)
    - [3.SOFAJRaft / Rheakv   -- 并行压缩日志](#3sofajraft--rheakv------并行压缩日志)
  - [4.4 数据库研发经验](#数据库研发经验)
    - [1.Pingcap/Tinykv](#1pingcaptinykv)
    - [**2.Mit6.830**](#2mit6830)

## 个人信息

姓名: 黄章衡

学校: 福州大学19级计算机系

邮箱: 642256541@qq.com



## 个人荣誉

- **Committer of SOFAStack/SOFAJRaft**
- Contributor of Apache/Rocketmq, OpenMessaging/Dledger
- Contributor of Pingcap/TiFlash
- Member of Pingcap/talent-plan
- [2021 '开源软件供应链点亮计划' -- '突出贡献奖'](https://summer.iscas.ac.cn/#/fintermdata)
- [2021 'Pingcap tinykv 分布式存储训练营 第一名'](https://asktug.com/t/topic/393068)
- 腾讯, 华为 -- fzu校园大使
- 2021年 中国大学生服务外包创新创业大赛国家级 一等奖
- ...................



## 实习经历

### Tencent

**工作内容:** 构建 mpp 大规模分布式并行计算引擎, 负责任务分级监控, 资源隔离, 任务调度等 ~



## 开源贡献

### Apache / Rocketmq

#### 1.支持 HA 主从切换

统一 Rocketmq 日志复制链路, 实现主从切换能力, 代替原有的 dledger 模式, 架构级项目.
![image](https://user-images.githubusercontent.com/58988019/167562365-a083f415-1701-425f-92cc-eb72eb2b3f0c.png)
- RIP: (pending, 后续会发布)
- 为 Dledger 新增 statemachine , pr: [Feature: add statemachine for dledger by hzh0425 · Pull Request #128 · openmessaging/dledger (github.com)](https://github.com/openmessaging/dledger/pull/128)
- 为 Rocketmq 新增 Controller: pr: [[Summer of Code\] Dledger controller by hzh0425 · Pull Request #4195 · apache/rocketmq (github.com)](https://github.com/apache/rocketmq/pull/4195)
- 基于 Nio 实现新的 Ha -- AutoSwitchHAService, 新的日志复制协议 , 在主从切换时进行日志截断: pr: [[Summer of Code] Support switch role for ha service ](https://github.com/apache/rocketmq/pull/4236) 
- 在 Broker 层面实现主从切换的功能. pr: [[Summer of Code] Support switch role for broker](https://github.com/apache/rocketmq/pull/4272)



### Pingcap / TiFlash
Pending, comming soon


### SOFAStack / SOFAJRaft 

#### 1.SOFAJRaft   -- 构建日志存储模块

![image](https://user-images.githubusercontent.com/58988019/167566312-ffff79b7-79f5-4d54-bc5e-ce59bea15da2.png)

- 该项目为2021年暑期开源软件供应链点亮计划的高难度项目,并获得了'突出贡献奖'的奖项
- 主要工作是为 SOFAJRaft 构建新的存储模块.
- 基于软件分层思想,构建了索引与数据存储一体化存储架构。
- 利用mmap内存映射技术,文件预分配,文件预热,组提交等,有效的提高了读写性能。
- 项目说明: https://summer.iscas.ac.cn/#/org/prodetail/210170433
- Pr 地址: https://github.com/sofastack/sofa-jraft/pull/696
- [详细文章地址](https://mp.weixin.qq.com/s?__biz=MzUzMzU5Mjc1Nw==&mid=2247497065&idx=1&sn=41cc54dbca1f9bb1d2e50dbd181f062d&chksm=faa31ab3cdd493a52bac26736b2d66c9fcda77c6591048ae758f9663ded0a1a068947a8488ab&mpshare=1&scene=23&srcid=1026H0gUsE1GGJq3hgzmKpGe&sharer_sharetime=1635251084804&sharer_shareid=4685e37971dd76c96606e8a800ad9755#rd)



#### 2.SOFAJRaft / Rheakv    -- 并行化状态机

- 借鉴Mysql并行复制的特性,针对分布式状态机单线程执行的弊端,提出通用的多线程并行状态机,任何基于状态机的共识算法都能使用该思想构建多线程状态机。

- 基于BloomFilter+Dag有向无环图+高性能并发队列Disruptor。

- 通过批量提交与依赖检测,将无依赖的任务批次进行并行化执行。

- 显著的提高了Rheakv的吞吐量和并行度。

- Pr 地址: https://github.com/sofastack/sofa-jraft/pull/678
- Issue 地址:  https://github.com/sofastack/sofa-jraft/issues/614



#### 3.SOFAJRaft / Rheakv   -- 并行压缩日志

- 描述: 基于 Common-compress 进行日志的并行化压缩与解压缩  

- Pr 地址: https://github.com/sofastack/sofa-jraft/pull/603
- Issue 地址: https://github.com/sofastack/sofa-jraft/issues/596





### 数据库研发经验

#### 1.Pingcap/Tinykv 

- 主要工作:完成一款支持分布式事务的键值存储系统  (暂不开源)

- Pingcap / Talent-plan tinyk **训练营第一名: 97.2 分**

- 根据Raft论文,实现了Raft模块,具备Leader选举,日志复制,Snapshot等基础功能,同时引入了Batch-Pipeline,

Read-Index等优化。

- 搭建了Multi-Raft架构,对数据基于Range进行分区,支持Region split和Region merge的功能。
- 搭建了Scheduler模块,通过Region心跳收集,对Region进行负载调度,平衡每个Store上的Regoin和Leader。
- 实现了Mvcc多版本并发控制,并基于Percolator模型,支持高性能分布式事务。



#### **2.Mit6.830** 

- 主要工作:完成一款支持sql解析和优化的数据库管理系统, 开发语言:Java

- 完成了基于HeapFile的数据存储功能,并具备BufferPool(基于LRU算法),支持Page缓存与淘汰功能。

- 基于Volcano火山模型,构建Operator执行树,同时具备各种常见的算子,如SortMergeJoin,Aggregation,Filter。

- 支持Sql解析和查询优化,基于Left-Deep-Tree和DynProgramming实现了Join优化器。

- 具备事务功能,基于Page粒度下的2PL协议以及DeadLockDetector,实现了事务的ACID特性。通过日志和Checkpoint机制,支持事务的回滚与恢复。

- 完成了B+树索引模块,支持查询,插入删除,以及页合并,页分裂的特性。

仓库地址:https://github.com/CreatorsStack/CreatorDB

















