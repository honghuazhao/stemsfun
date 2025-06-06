+++
date = '2025-04-06T01:10:35-04:00'
draft = false
title = 'Transformer Decoder'
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

Transformer encoder is used usually in NLP tasks. It's the backbone of models like BERT, RoBERTa, DistilBERT and the encoder part of T5.

The overall Transformer encoder is made up of N identical layers, where each layer has two main sub-layers:
1. Multi-Head Self-Attention
2. Feed-Forward Neural Network (FNN)
Each sub-layer has a residual connection + layer normalization.

```
Input Embeddings 
	→ [Positional Encoding added] 
	→ [Encoder Layer 1] 
	→ [Encoder Layer 2] 
	→ ... 
	→ [Encoder Layer N] 
	→ Final Encoder Output
```

Inside a Single Encoder Layer
```
Input 
	→ [Multi-Head Self-Attention + Add & Norm] 
	→ [Feed-Forward Network + Add & Norm] 
	→ Output
```

## 1. Input Embedding + Positional Encoding


## 2. Multi-Head Self-Attention


## 3. Add & Norm


## 4. Feed-Forward Network (FFN)


## 5. Add & Norm Again


## 6. Final Output


