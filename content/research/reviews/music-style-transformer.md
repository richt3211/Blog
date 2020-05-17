---
title: "Music Style Transformer"
date: 2020-05-14T15:17:01-06:00
draft: false
---

* [Google Scholar Link](https://scholar.google.com/scholar?hl=en&as_sdt=0%2C45&q=Music+Style+Transformer&btnG=)
* [Content Link](https://csce.ucmss.com/cr/books/2019/LFS/CSREA2019/ICA7029.pdf)

# Quick Notes
* They use a dataset larger than MAESTRO and intend to make the datasets publicly available. 
* Uses framework for Music Generation but that could probably be applied to any computer music application in general. This framework is outlined in the Wave2Midi2Wave paper from Magenta. 
    * Encoder P(notes|audio). Transcription. Taking raw audio in WAV format and outputs a MIDI transcription of raw audio signal, modeled for piano. 
    * Prior, P(notes): Generative model which uses relative self-attention to take as input the generated MIDI and produces a generated MIDI as output. 
    * Decoder, P(audio|notes). 
* For transcription they use the 