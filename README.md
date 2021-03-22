### 2021-GAIIC-Track1-idea

非常荣幸能够拿到本周周星星，目前线上分数是5折nezha-base模型融合得到，采用pretrian+finetuning，具体细节如下：

### Pretrain

1. 由于数据是脱敏，所以直接从头开始训练bert模型，没有加载已有的预训练模型权重，模型采用的是nezha-base，代码参考；[nezha](https://github.com/lonePatient/NeZha_Chinese_PyTorch)
2. mask方法：采用ngram mask方法，以及动态mask方法，具体可以参考：[albert](https://github.com/lonePatient/albert_pytorch)
3. 预训练代码使用的是tansformers模块自带的，具体可以参考；[transformers](https://github.com/huggingface/transformers)
4. 预训练参数：lr=1e-4，batchSize=128，seql_length=128，动态batch length，最终mlm损失为0.3左右

### Finetuning

1. k折： 采用的multilabel进行划分，默认k=5
2. 模型：nezha模型微调，并直接使用CLS进行分类，采用sigmoid
3. 损失； 二分类交叉熵损失函数

4. 对抗：加入对抗训练，使用的是fgm

5. 自融合方法，采用是SDA,可以参考：[SDA](https://github.com/lonePatient/BERT-SDA)
5. 优化器：加入lookahead方法，具体可以参考：[lookahead](https://github.com/lonePatient/lookahead_pytorch)
5. 线下dev：0.96

总体上没有新的技巧，都是自己仓库中的方法拿来堆的，线上线下差距很大，也很难同步，所以摸奖看人品。
