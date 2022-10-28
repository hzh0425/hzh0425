

- [1. 个人信息](#个人信息)
- [2. 个人荣誉](#个人荣誉)
- [3. 实习经历](#实习经历)
- [4. 开源贡献](#开源贡献)
  - [4.1 Apache / Rocketmq](#apache--rocketmq)
    - [1.支持 Master-Slave 主从切换](#1支持-ha-主从切换)
  - [4.2 SOFAStack / SOFAJRaft](#sofastack--sofajraft)
    - [1.SOFAJRaft   -- 构建日志存储模块](#1sofajraft------构建日志存储模块)
    - [2.SOFAJRaft / Rheakv    -- 并行化状态机](#2sofajraft--rheakv-------并行化状态机)
    - [3.SOFAJRaft / Rheakv   -- 并行压缩日志](#3sofajraft--rheakv------并行压缩日志)
  - [4.3 数据库研发经验](#数据库研发经验)
    - [1.Pingcap/Tinykv](#1pingcaptinykv)
    - [**2.Mit6.830**](#2mit6830)

## 个人信息

邮箱: hzh0425@apache.org

个人公众号: 小衡开源之路

## 个人荣誉

- **Committer of Apache/Rocketmq**
- **Committer of SOFAStack/SOFAJRaft**
- Contributor of Pingcap/TiFlash
- Member of Pingcap/talent-plan
- [2021 '开源软件供应链点亮计划' -- '突出贡献奖'](https://summer.iscas.ac.cn/#/fintermdata)
- [2021 'Pingcap tinykv 分布式存储训练营 第一名'](https://asktug.com/t/topic/393068)
- 腾讯, 华为 -- fzu校园大使
- 2021年 中国大学生服务外包创新创业大赛国家级 一等奖
- ...................

## 实习经历
#### 腾讯
#### Microsoft


## 开源贡献

### Apache / Rocketmq

#### 1.支持 HA 主从切换

![image](https://user-images.githubusercontent.com/58988019/167562365-a083f415-1701-425f-92cc-eb72eb2b3f0c.png)

- 主要工作: 升级 Rocketmq 主从切换架构, 统一 Rocketmq 日志复制链路, 代替原有的 Dledger 切换模式, 是 Rocketmq 5.0 全新架构的重要功能特性之一。
- RIP: https://shimo.im/docs/N2A1Mz9QZltQZoAD
- Tracking issue: https://github.com/apache/rocketmq/issues/4330
- 为 Dledger 新增 statemachine , pr: [Feature: add statemachine for dledger by hzh0425 · Pull Request #128 · openmessaging/dledger (github.com)](https://github.com/openmessaging/dledger/pull/128)
- 基于 Raft 算法库 Dledger, 实现高可用, 强一致的元数据管理中心 Controller, 赋能 Broker 选举能力: pr: [[Summer of Code\] Dledger controller by hzh0425 · Pull Request #4195 · apache/rocketmq (github.com)](https://github.com/apache/rocketmq/pull/4195)
- 设计全新的日志复制协议, 配合 Controller 进行日志的截断, 统一 Rocketmq 日志复制链路: pr: [[Summer of Code] Support switch role for ha service ](https://github.com/apache/rocketmq/pull/4236) 
- 对接 Controller 与 Broker api 协议, 实现主从切换功能, 让 Broker 具备自动切换 Master 和 Slave 角色的能力. pr: [[Summer of Code] Support switch role for broker](https://github.com/apache/rocketmq/pull/4272)
- 支持 Async Learner Broker 角色, 以异步的方式接入 Master 日志复制链路, 适用于不同数据中心日志备份场景: https://github.com/apache/rocketmq/pull/4367


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

















