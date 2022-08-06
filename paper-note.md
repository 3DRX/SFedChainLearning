# SFedChain

## Background

- 如果不使用区块链技术，FL系统的攻击者仍然可以通过根据模型反推等方式得到原始数据中可能存在的敏感信息
- FL系统具有分布式、去中心化的结构，适用区块链技术。
- 2个此前未被重视的问题，此文旨在解决
    1. 关于安全的思考大多集中在防御中心服务器或边缘节点被攻击上，而忽略了边缘节点本身作为攻击者提供低质量参数的情况。
    2. 一些安全策略可能会导致参与者兴趣降低。

## System Model

### Roles

- TaskRequester
系统中的任意一个边缘节点
- DataHolders
    所有的边缘节点
- TaskCollaborators
    参与特定任务的边缘节点
- ConsensusMembers
    具有高信誉、高贡献度的边缘节点，负责从所有 TaskCollaborators 上传的模型中整合出最优模型

### SFedChain scheme

- MasterChain
    1. 发布 requested task
    2. 储存过去已完成 task 的合并后的模型信息
    3. 储存所有参与FL的边缘节点信息

- RetrievalChain
    1. 


- ArgChain
    1. TaskCollaborators 在这里上传自己通过本地数据训练的模型参数

