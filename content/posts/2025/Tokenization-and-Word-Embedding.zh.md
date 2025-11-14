+++
date = '2025-04-03T23:12:28-04:00'
draft = false
title = 'Tokenization 和 Word Embedding'
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

Tokenization 和 Word Embedding 是在进行任何其他 NLP 处理之前的两个常见过程。原因是 AI 模型只能处理数字作为输入和输出，但 NLP 处理的目标主要是语言数据，如单词或句子。因此需要 tokenization 和 word embedding 将自然语言转换为数字，以便 AI 模型可以处理它们。

## 什么是 Tokenization？

Tokenization 通常非常简单直接。对于给定的单词序列，tokenization 会将它们转换为一系列数字。通常一个序列单元对应输出数字序列中的一个数字。

在 Hugging Face Transformer 库的某些 tokenizer 中，输出通常会添加两个特殊标记：[CLS] 和 [SEP]，分别表示序列的开始和结束。

```
"你好，世界！" → ["CLS", "你好", "，", "世界", "！", "[SEP]"]
```

在 Hugging Face Transformer 库中，我们可以这样使用 tokenization：

```python
from transformers import BertTokenizer

tokenizer = BertTokenizer.from_pretrained("bert-base-uncased")

text = "Hello, world!"
tokens = tokenizer(text, return_tensors="pt")

print(tokens)
print(tokenizer.convert_ids_to_tokens(tokens["input_ids"][0]))
```

输出：
```
{'input_ids': tensor([[ 101, 7592, 1010, 2088,  999,  102]]), 'token_type_ids': tensor([[0, 0, 0, 0, 0, 0]]), 'attention_mask': tensor([[1, 1, 1, 1, 1, 1]])}

['[CLS]', 'hello', ',', 'world', '!', '[SEP]']
```

## 什么是 Word Embedding？

现在我们可以使用 tokenization 将原始文本转换为模型的结构化输入。但仍然存在一些问题：
- 简单的整数无法表示单词之间的关系。例如，'苹果'和'香蕉'都是水果，因此它们应该有一些共同特征，但我们无法从两个数字中获得这些信息。
- 它还引入了不必要的顺序关系。从上面的输出来看，'Hello' 被编码为数字 7592，而 'world' 是 2088，但这两个词之间并没有实际的顺序关系。

Word Embedding 使用向量而不是单个数字，这可以消除这些缺点。通过使用向量，如果我们将所有单词绘制到多维空间中，两个单词可以具有语义关系。一个词可以有不同的含义，比如 'fly' 可以是昆虫，也可以是在空中移动的动作。不同的含义可以通过向量中不同维度上的数字来表示。

Word2Vec 提供了一种通过使用大型语料库进行训练来生成 word embedding 的方法。最终结果可能是这样的：

```
"king"  → [0.25, -0.63, 0.14, ..., 0.98] (例如，100-300 维)
"queen" → [0.21, -0.60, 0.18, ..., 1.00]

king - man + woman ≈ queen
```

这些向量运算可以捕获性别、国家-首都、时态等关系。

## Tokenization 和 Word Embedding 是 NLP 的预处理吗？

Tokenization 可以被视为 NLP 中的预处理。但使用 word embedding 有两种不同的方式。

传统的 NLP 流程会使用 Word2Vec、Glove 或 FastText 训练的结果作为下游模型（如 LSTM、GRU、文本 CNN 等）的输入。

然而，现代 AI 模型如 Transformer（如 BERT、GPT）会将词向量训练集成到整个流程中。它们在内部学习并应用 embedding 作为第一层。因此，当这些模型被训练时，词向量也会一起被训练。
