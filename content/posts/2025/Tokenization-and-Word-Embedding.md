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
In Hugging Face Transformer library, we can use tokenization like this:
```
from transformers import BertTokenizer

tokenizer = BertTokenizer.from_pretrained("bert-base-uncased")

text = "Hello, world!"
tokens = tokenizer(text, return_tensors="pt")

print(tokens)
print(tokenizer.convert_ids_to_tokens(tokens["input_ids"][0]))
```
Output:
```
{'input_ids': tensor([[ 101, 7592, 1010, 2088,  999,  102]]), 'token_type_ids': tensor([[0, 0, 0, 0, 0, 0]]), 'attention_mask': tensor([[1, 1, 1, 1, 1, 1]])}

['[CLS]', 'hello', ',', 'world', '!', '[SEP]']
```
## What is Word Embedding?

Right now we could use tokenization to turn raw text into structured input for models. But there are still problems for them:
- The simple integers doesn't represent the relationship between the words. For example, 'apple' and 'banana' are both fruit so they should have some common feature but we can't get this info from two.
- It also introduces unnecessary order. Like from the above output, 'Hello' is encoded as number 7592 while 'world' is 2088, but the two words doesn't have an actual sequence relation.

Word Embedding would use a vector instead of a single number which could remove the drawbacks. By using vector, two words can have a semantic relation if we draw all words into a multiple dimension space. A word can have different meanings like 'fly' can be an insect or an action moving one place to the other in air. The different meaning can be represented by the numbers on different dimensions in the vector.

Word2Vec provides a way to generate word embedding by training using a large corpus. The final result might be like this:
```
"king"  → [0.25, -0.63, 0.14, ..., 0.98] (say, 100–300 dimensions)
"queen" → [0.21, -0.60, 0.18, ..., 1.00]

king - man + woman ≈ queen
```
These vector operations capture relationships like gender, country-capital, tense and more.

## Is Tokenization and Work Embedding pre-processing of NLP?

Tokenization can be considered as a pre-process in NLP. But there are two different ways to use work embedding.

The traditional NLP pipeline would use the result trained by Word2Vec, Glove or FastText as inputs to downstream models like LSTMs, GRUs, CNNs for text and so on.

However modern AI models like Transformer (like BERT, GPT) would integration the word vector training into the whole pipeline. They learn and apply embedding internally as the first layer. So when these models are trained, the word vectors are also trained together.