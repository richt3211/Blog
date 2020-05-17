---
title: "Music Transformer: Generating Music With Long Term Structure"
date: 2020-05-14T13:03:49-06:00
draft: false
tags: ['Paper Review', 'Music Generation', 'Transfomer']
---
* [Google Scholar Link](https://scholar.google.com/scholar?hl=en&as_sdt=0%2C45&q=Music+transformer%3A+Generating+music+with+long-term+structure&btnG=)
* [Content Link](https://openreview.net/pdf?id=rJe4ShAcF7)
* [Website Link](https://magenta.tensorflow.org/music-transformer)

# Abstract
Music relies heavily on repetition to build structure and meaning. Self-reference
occurs on multiple timescales, from motifs to phrases to reusing of entire sections
of music, such as in pieces with ABA structure. The Transformer (Vaswani
et al., 2017), a sequence model based on self-attention, has achieved compelling
results in many generation tasks that require maintaining long-range coherence.
This suggests that self-attention might also be well-suited to modeling music.
In musical composition and performance, however, relative timing is critically
important. Existing approaches for representing relative positional information
in the Transformer modulate attention based on pairwise distance (Shaw et al.,
2018). This is impractical for long sequences such as musical compositions because
their memory complexity for intermediate relative information is quadratic in the
sequence length. We propose an algorithm that reduces their intermediate memory
requirement to linear in the sequence length. This enables us to demonstrate
that a Transformer with our modified relative attention mechanism can generate
minute-long compositions (thousands of steps) with compelling structure, generate
continuations that coherently elaborate on a given motif, and in a seq2seq setup
generate accompaniments conditioned on melodies. We evaluate the Transformer
with our relative attention mechanism on two datasets, JSB Chorales and Maestro,
and obtain state-of-the-art results on the latter.

# Notes By Section

## 1 Introduction
Self-attention is a good task for generating music because of the self-referential nature of music and the way that builds on patterns that already exist. Self-attention models can access previous outputs at any step of the model, whereas recurrent neural networks have to proactively store state in a fixed size, making training more difficult. The original formulation of attention was an absolute self-attention, but relative self-attention was introduced as a way to capture pairwise relationships between different dimensionalities of the data (such as pitch and timing).  

Idiomatic piano gestures such as scales, arpeggios, and other motifs all exhibit a certain grammar, pattern and recurr periodically. A relative self-attention approach should perform better because of the knowledge of the relative position from one structure to another, as opposed to the absolute position of each structure. 

### 1.1 Contributions
#### Domain Contributions
First successful use of Transformers in generating music that exhibits long-term structure. Relative self-attention is essential to model's quality. 

#### Algorithmic Contributions
Space complexity of self-attention in its original formulation was O(L^2D), and the new algorithm reduced it to O(LD) (where L is the sequence length and D is the hidden state size). 

## 2 Related Work
Traditional sequence models have been the canonical choice for modeling music, from Hidden Markov Models to RNNs and LSTMs. Sequential models in polphonic music requires serializing musical score or performance into a single sequence. A 2D pianoroll approach can be used with RBMs, or because they are image-like, with CNNs trained as a GAN.  

Self-similarity has been used in a style-transfer fashion. Self-attention can be seen as a generalization of self-similarity. Dot-product self attention (not sure what this is) is the core mechanism of the transformer. A key challenge for this approach is scaling attention computationally to long sequences. Time and space complexity of self-attention grows quadratically in the sequence length. 

## 3 Model 
### 3.1 Data Representation
They use a language-modeling approach for the abstract representation of the music. Music is represented as a sequence of discrete tokens where the vocabulary is determined by the dataset. The JSB Choral dataset is four-part scored choral music and is represented as a matrix where rows are the voices and columns are time (discretized to sixteength notes). Matrix's entries are integers which denote which pitch is being played. The matrix is serialized by first going down the rows and moving right through the columns. This gives $$S_1,A_1,T_1,B_1,S_2,A_2,T_2,B_2$$ where $$S,A,T,B$$ are the different voices and the index is each sixteenth note.  

The MAESTRO dataset is also used which comes in MIDI format. The data is represented as a series of events, given by [Oore]({{<ref "/research/reviews/this-time-with-feeling-learning-expressive-musical-performance.md">}}). 

### 3.2 Self-Attention in Transformer
The Transformer decoder is an autoregressive model that uses primarily self-attention mechanisms, and learned sinusoidal position information. Each layers consists of a self-attention sub-layer followed by a feedforward sub-layer. See [Attention is All You Need]({{<ref "/research/resources.md#other">}})

### 3.3 Relative Positional Self-Attention
The transformer model relies solely on positional sinusoids to represent timing information, but a relative position position representation was introduced to allows for two positions in a sequence to inform each other based on how far apart they are. This is done by adding a relative position embedding matrix into the original attention model which has an embedding for each possible pairwise distance between a query and a key for a given position. 

### 3.4 Memory Efficient Implementation of Relative Position-Based Attention
They improve the implementation of relative self-attention by reducing the memory requirement from $$O(L^2 D)$$ to $$ O(LD)$$. 

### 3.5 Relative Local Attention
For long sequences the quadratice memory requirment of Transformer models is impractical. Local attention is used to address this by chunking the input sequence into non-overlapping blocks. They adapt relative self-attention to the local case. 

## 4 Experiments
### 4.1 J.S. Bach Chorales
The relative self-attention model is applied to this dataset. Becuase the sequence is laid out one chord at a time the relative nature of the transformer should make it easier to learn the grammar and structure. The relative attention drastically improves the negative log-likelihood over baseline transformer model. 

#### 4.1.1 Generalizing Relative Attention To Capture Relational Information
I'm not exactly sure what this paragraph is saying. It has to do with adding other dimensions of information on top of pitch and timing. The problem is that doing this increases the memory complexity back to what it was before the optimization. I don't fully understand the math behind their algorithmic optimization so I'm not sure how relevant this is. 

### 4.2 MAESTRO
This data set uses the event-based tokens as introduced by [Oore]({{<ref "/research/reviews/this-time-with-feeling-learning-expressive-musical-performance.md">}}). They train on random crops of 2048-token sequences and augment the data with pitch and timing transpositions. I'm not sure exactly how they split, but they end up with 1128 and 1183 subsequences in the validation and test set respectively.  

There are comparisons to other architectures. For the JSB Chorale they are the Coconet and baseline Transformer model. For the MAESTRO, they are the PerformanceRNN and the LSTM with attention. The negative log-likelihood performs the best on the relative self-attention.  

Implentation was done with the Tensor2Tensor framework with default hyperparamaters. 

#### 4.2.2 Harmonization: Conditioning on Melody 
They also conducted an experiment when the encoder takes in a given melody and the decoder has to realize the entire performance by generating the accompaniment. The relative attention outperforms the baseline Transfomer model for this task 

#### 4.2.3 Human Evalutions
Human input is sampled comparing all of the different types of models. Next to the actual data itself, the relative transformer outperforms all other models when considering the question "which one is more musical". 

# Thoughts
I think that this paper is going to be a good basis for the research that I conduct. The conclusion me and my advisor came to after our first meeting was to take the Transformer based models and apply them to music as has been done for NLP. Given that this has already happened as shown in this paper, the specific direction to head in may be in applying the same transformer model to a different application, or in coming up with a novel way to improve the transformer. I haven't seen anything application of the GPT-2 or BERT models for music, so that is worth looking into. 




