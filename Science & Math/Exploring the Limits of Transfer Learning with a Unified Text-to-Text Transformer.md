#Paper 
Unified framework to convert text-based problems to text-to-text.
Compares:
- Pre-training objectives
- Architectures
- Unlabeled data sets
- Transfer approaches

Since unlabeled text data is available in massive amounts and neural networks have great scalability, pretraining for later transfer learning has become a powerful approach.

The proposed model is Text-to-Text Transfer Transformer or T5.
It was trained on hundreds of GBs of clean English from the web.
All studied models are transformers.

T5 Architecture:
- Input sequence of tokens is mapped to a sequence of embeddings 
- The embeddings are passed to an encoder.
- The encoder consists of:
	- Block:
		- Layer normalization (no bias)
		- Residual In
		- Self-attention layer
		- Residual Out
		- Dropout
		
		- Layer normalization (no bias)
		- Residual In
		- Shallow MLP
		- Residual Out
		- Dropout
	- Dropout
- The decoder consists of:
	- Block:
		???

In decoder: 
- Attention after self-attention, attending to the output of the encoder.
- Self-attention is causal
Dense layer with softmax whose weights are shared with input embedding matrix. This is known as [[Tied Embedding|tied embedding]].

All attentions are separated in independent heads.

To provide positional information to the self-attention layer, relative positional embeddings are used. 
These are scalars added to the logits that compute attention weights. These are shared across layers but are distinct between heads.
32 embeddings that increase logarithmically up to 128 are learned

It differs from original transformer in: 
- Not having a bias in layer normalization
- Layer normalization is placed outside residual
- Distinct positional embedding.

Models are trained on slices with 1024 TPUs v3 connected in a 2D mesh with supporting CPUs.
Makes use of Mesh TensorFlow.

Common Crawl is a public archive of text internet data.
This was filtered such that only relevant text was kept.
It was dubbed Colossal Clean Common Crawl and is about 750GB

Maximum likelihood was used as objective.
...

# Results
Encoder-decoder with denoising objective was best.
Sharing weights in encoder and decoder only reduced performance slightly. 
Layer depth is important.
The denoising objective is such that it randomly drops 15% of the input sequence and replaces the spans by sentinel tokens. Each distinct span has a unique token ID.

# Unsupervised Objectives
| Objective                       | Inputs                                              | Targets                                             |
| ------------------------------- | --------------------------------------------------- | --------------------------------------------------- |
| Prefix language modeling        | Thank you for inviting   | me to your party last week . |
| BERT-style Devlin | Thank you < M > < M > me to your party apple week .  | (original text) |
| Deshuffling | party me for your to . last fun you inviting week Thank | (original text) |
| MASS-style | Thank you < M > < M > me to your party < M > week . | (original text) |
| I.i.d. noise, replace spans | Thank you < X > me to your party < Y > week | < X > for inviting < Y > last < Z >|
| I.i.d. noise, drop tokens | Thank you me to your party week . | for inviting last  |
| Random spans | Thank you < X > to < Y > week | < X > for inviting me < Y > your party last < Z >|

Replace spans had the best performance, followed by drop tokens.
Best corruption rate was 15%

Replacing spans with with a single token results in unlabeled data being processed into shorter sequences. Thus, instead of randomly replacing separate tokens, spans of tokens are corrupted such that the desired drop rate is achieved for a given number of spans. A span length of 3 was found to be best. 

# Fine-tuning
Adaptive layers are implemented as dense-ReLU-dense blocks after MLPs.
Higher inner dimension performs best for more intensive tasks.
