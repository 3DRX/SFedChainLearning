# SFedChain

#### Introduction
SFedChain: blockchain-based federated learning scheme for secure data sharing in distributed energy storage networks

## kjy

### Environment

- python@3.8.13, 原作者用的3.8.10，但目前（8月10日）看来没啥问题。尝试过更高的版本比如 3.10 甚至 3.9 都不行（无法下载wikipedia2vec）

- 所有代码中用到的库下载最新版的就行

- **Download Wikipedia2Vec embeddings:**

```bash
% wget https://wikipedia2vec.s3-ap-northeast-1.amazonaws.com/misc/text_classification/enwiki_20180420_lg1_300d.pkl.bz2
% bunzip2 enwiki_20180420_lg1_300d.pkl.bz2
```
- **Download entity detector model:**

```bash
% wget https://wikipedia2vec.s3-ap-northeast-1.amazonaws.com/misc/text_classification/enwiki_20180420_entity_linker.pkl.bz2
% bunzip2 enwiki_20180420_entity_linker.pkl.bz2
```

### Progress

- 8-7
    1. main 40行处的 embedding 和 entity_linker
       报错（wikipedia2vec找不到一个文件？？？）
       暂时先注释掉了，去跑后面加载数据的部分

    2. 加载 agnews 时 'text_gcn/data/agnews.txt' 是哪个文件？
       发现 reformat_agnews.py
       中原作者将文件路径硬编码了，尝试着改成相对路径，不知改对与否

- 8-8
    1. 手动创建agnews数据集所需要的text_gcn目录及其中文件，
       解决了8-7 问题2

    2. 20ng模式下修改了文件路径硬编码问题

    3. agnews 与 20ng 遇到了一个共同问题：  
       'entity_linker' has no attribute 'detect_mentions'

报错如下：
```
Traceback (most recent call last):
    File "main_fedweight.py", line 80, in <module>
    dataset.load_data(tokenizer, entity_linker, val_ratio=args.val_ratio_global)
    File "/Users/kjy/Documents/SFedChainLearning/data_fed/utils_data_fed.py", line 214, in load_data
    entity_counter.update(m.title for m in detect_mentions(instance.text))
    File "/Users/kjy/Documents/SFedChainLearning/data_fed/utils_data_fed.py", line 164, in detect_mentions
    return entity_linker.detect_mentions(text)
    AttributeError: module 'entity_linker' has no attribute 'detect_mentions'
```

- 8-9
    1. 8-7 问题3的原因是因为 8-7 问题1注释掉了entity_linker的赋值（I am stupid）

    2. --wikipedia2vec_file 和 --entity_linker_file 的参数默认值  
       （分别是 enwiki_20180420_lg1_300d.pkl 和 enwiki_20180420_entity_linker.pkl），  
       这两个文件是从哪来的？

- 8-10
    1. 8-9 问题2 中提到的文件来源:  
    https://github.com/wikipedia2vec/wikipedia2vec/tree/master/examples/text_classification


