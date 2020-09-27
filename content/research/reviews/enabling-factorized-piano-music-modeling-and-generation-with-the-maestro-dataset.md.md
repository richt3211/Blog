---
title: "Enabling factorized piano music modeling and generation with the MAESTRO dataset"
date: 2020-05-14T17:15:37-06:00
draft: false
---
* [Google Scholar Link](https://scholar.google.com/scholar?hl=en&as_sdt=0%2C45&q=Enabling+Factorized+Piano+Music+Modeling+and+Generation+with+the+MAESTRO+Dataset&btnG=)
* [Content Link](https://arxiv.org/pdf/1810.12247.pdf)

# Quick Notes
* They provide a 3 part process as part of a Bayesian framework for generating new audio samples. 
* To generate $P(audio) = E_notes[P(audio|notes)]$
    * 1. Encoder, $P(notes|audio)$: An [Onsets and Frames transciption model]({{<ref "/research/reviews/onsets-and-frames-dual-objective-piano-transcription.md">}})
    * 2. Prior, $P(notes)$: [A self-attention Transformer Model]({{<ref "/research/reviews/music-transformer-generating-music-with-long-term-structure.md">}})
    * 3. Decoder, P(audio|notes): Using the [WaveNet architecture]({{<ref "/research/references#music-synthesistranscription">}})
* They introduce the MAESTRO dataset. 
* One useful part of the architecture is it's modularity and the ability to switch out different models at each of the steps. 
* Other data sets used for comparison with the MAESTRO dataset
    * MusicNet: Paired audio and MIDI from different sources. Has other instruments than piano
    * MAPS: Synthesized audio with MIDI
    * Saarland Music Data (SMD). Similar to MAESTRO but much smaller. 
* They performed an automatic alignment between the audio and MIDI files. Something that I was not expecting but is impressive and makes me trust the dataset more. 
* MAESTRO datasets provides opportunity for state of the art transcription model. They use the Onsets and Frames transcription model with modificiations. 
* For transcription, the best ways to get higher performance with a larger dataset were to make the model large and simpler. 
* For the transformer training they used two versions of MAESTRO MIDI in tandem with each other. One is the actual MIDI that comes from the dataset, and the other is the MIDI that comes as a result of using the Transcription model. They call the second dataset MAESTRO-T. 