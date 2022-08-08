# SFedChain

#### Introduction
SFedChain: blockchain-based federated learning scheme for secure data sharing in distributed energy storage networks

## kjy

### Environment

- python@3.8.13, 原作者用的3.8.10，但目前（8月7日）看来没啥问题。尝试过更高的版本比如 3.10 甚至 3.9 都不行（无法下载wikipedia2vec）

- wikipedia2vec==0.1.13，这个用最新版1.几的会报错，虽然原作者没有注明，但是根据python版本推测原作者用的也是0.几
    但是0.1.13虽然import不报错，运行时仍然表现不正常

- 其他的dependencies貌似不用刻意注意版本，直接pip下载最新版就行

### Progress

- 8-7
    1. main 40行处的 embedding 和 entity_linker
       报错（wikipedia2vec找不到一个文件？？？）
       暂时先注释掉了，去跑后面加载数据的部分

    2. 加载 agnews 时 'text_gcn/data/agnews.txt' 是哪个文件？
       发现 reformat_agnews.py
       中原作者将文件路径硬编码了，尝试着改成相对路径，不知改对与否

