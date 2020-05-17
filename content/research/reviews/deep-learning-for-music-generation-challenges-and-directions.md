---
title: "Deep Learning for Music Generation - Challenges and Directions"
date: 2020-05-06T08:17:35-06:00
draft: false
tags: ['Paper Review', 'Music Generation']
---
# Abstract 
In addition to traditional tasks such as prediction, classification
and translation, deep learning is receiving growing attention as an approach
for music generation, as witnessed by recent research groups such as Magenta
at Google and CTRL (Creator Technology Research Lab) at Spotify. The motivation is in using the capacity of deep learning architectures and training
techniques to automatically learn musical styles from arbitrary musical corpora and then to generate samples from the estimated distribution. However,
a direct application of deep learning to generate content rapidly reaches limits
as the generated content tends to mimic the training set without exhibiting
true creativity. Moreover, deep learning architectures do not offer direct ways
for controlling generation (e.g., imposing some tonality or other arbitrary constraints). Furthermore, deep learning architectures alone are autistic automata
which generate music autonomously without human user interaction, far from
the objective of interactively assisting musicians to compose and refine music.
Issues such as: control, structure, creativity and interactivity are the focus of
our analysis. In this paper, we select some limitations of a direct application
of deep learning to music generation, analyze why the issues are not fulfilled
and how to address them by possible approaches. Variou

# Section 1: Inroduction
* Motivation to use deep learning for music generation is because of its generality (as opposed to hand-crafted or rule based systems)
* Challenges to music generation
    * Control: tonality conformance, maximum number of repeated notes, rhythm
    * Structure: versus wandering music without a sense of direction
    * Creativity: versus imitation and risk of plagiarism
    * Interactivity: versus automated single-step generation

# Section 2: Control
## 2.1: Dimensions of control strategies
Can't control neural networks interactively (as opposed to a Markov model). NN's are also distributed doesn't provide direct correspondence for control. Have to rely on external intervention at entry points 
* Input
* Output
* Encapsulation/reformulation

## 2.2: Sampling
Sample from the output with constraints on the output generation (as opposed to pulling from a deterministic network). Sampling is often combined with other techniques because of the key issue on how to choose the constraints. 

## 2.3: Conditioning
Add conditions (which could be arbitrary) to the network to give more control over what it does. Examples for conditioning are (see references)
* Bass line or beat structure
* Chord progression in MidiNet architecture
* Musical Genre or instrument in WaveNet architecture
* Positional constrains in Ancticipation-RNN architecture

### 2.3.1 Example 1: WaveNet Audio Speech and Music Generation
WaveNet is a convolutional feedforward network that generates raw audio waveforms. Uses conditioning to guide the generation. There are two options, global or local conditioning depending on how the conditioning is applied (to all time steps or specific time steps). 

### 2.3.2 Example 2: Anticipation-RNN Bach Melody Generation
Uses conditioning to anticipate what the coming notes will be and guiding the RNN to sample from those notes. 

## 2.4 Input Manipulation
Input content is incrementally manipulated in order to match a target property. 

### 2.4.1 Example 1: DeepHear Ragtime Melody Accompaniment Generation
DeepHear architecture is aimed at generating ragtime jazz melodies. Architecture is 4-layer stacked autoencoders. Architecture is also used to generate a harmonization over a melody using the same architecture as well as what has already been learnt. 