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

- 8-8
    1. 手动创建agnews数据集所需要的text_gcn目录及其中文件，
       解决了8-7 问题2

    2. 20ng模式下修改了文件路径硬编码问题

    3. agnews 与 20ng 遇到了一个共同问题：  
       'entity_linker' has no attribute 'detect_mentions'

报错如下：
Traceback (most recent call last):
  File "main_fedweight.py", line 80, in <module>
    dataset.load_data(tokenizer, entity_linker, val_ratio=args.val_ratio_global)
  File "/Users/kjy/Documents/SFedChainLearning/data_fed/utils_data_fed.py", line 214, in load_data
    entity_counter.update(m.title for m in detect_mentions(instance.text))
  File "/Users/kjy/Documents/SFedChainLearning/data_fed/utils_data_fed.py", line 164, in detect_mentions
    return entity_linker.detect_mentions(text)
AttributeError: module 'entity_linker' has no attribute 'detect_mentions'

