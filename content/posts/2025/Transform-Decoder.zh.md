+++
date = '2025-04-06T01:10:35-04:00'
draft = false
title = 'Transformer 编码器'
tags = [
	"transformer",
	"nlp"
]
series = [
	"nlp-transformers"
]
categories = [
	"reading-notes"
]
+++

Transformer 编码器通常用于 NLP 任务。它是 BERT、RoBERTa、DistilBERT 等模型的主干，也是 T5 模型的编码器部分。

整体的 Transformer 编码器由 N 个相同的层组成，每一层有两个主要的子层：
1. 多头自注意力机制（Multi-Head Self-Attention）
2. 前馈神经网络（Feed-Forward Neural Network，FNN）

每个子层都有残差连接和层归一化。

```
输入嵌入（Input Embeddings）
	→ [添加位置编码]
	→ [编码器层 1]
	→ [编码器层 2]
	→ ...
	→ [编码器层 N]
	→ 最终编码器输出
```

单个编码器层内部结构：
```
输入
	→ [多头自注意力 + 相加与归一化]
	→ [前馈网络 + 相加与归一化]
	→ 输出
```

## 1. 输入嵌入 + 位置编码


## 2. 多头自注意力机制


## 3. 相加与归一化


## 4. 前馈神经网络（FFN）


## 5. 再次相加与归一化


## 6. 最终输出

