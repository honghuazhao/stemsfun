+++
date = '2025-04-03T23:12:28-04:00'
draft = false
title = 'Tokenization and Word Embedding'
tags = [
	"Transformer",
	"NLP"
]
series = [
	"Natural Language Processing with Transformers"
]
categories = [
	"Book Reading Note"
]
+++

Tokenization and Word Embedding are two common NLP processes before we do anything else. The reason is that AI models can only handle numbers as input and output but the target that NLP handles is mostly about language data, like words or sentences. So tokenization and word embedding are needed to transform natural languages into numbers so AI models can handle them.
## What is Tokenization?
Tokenization is usually pretty straight forward. For a given word sequence, tokenization would turn them to a series of numbers. Usually one sequence unit corresponds to a number in the output number sequence.

In some tokenizer in Hugging Face Transformer library, the output would usually be added two special tokens: [CLS] and [SEP] which represent the beginning and ending of the sequence.
```
"Hello, world!" → ["CLS", "hello", ",", "world", "!", "[SEP]"]
```

## What is Word Embedding?
## Is Tokenization and Work Embedding pre-processing of NLP?
