---
title: "Thoughts on Goals"
date: 2020-05-15T12:24:59-06:00
draft: false
---
One of the deadlines for the project is send the undergraduate research advisor a list of goals for the researcha project and a definition of what success in the project is. This is due next Monday, the 18th of May. At this point I don't feel that I am fully ready to make such a list, but given the deadline it is something that I need to do. I have only had one meeting with my research advisor and the general take away from that meeting was to look into adapting NLP based Transformer models to music. He had me look at some articles talking about what the Transformer model is in general and some specific applications of that model, namely [BERT](https://ai.googleblog.com/2018/11/open-sourcing-bert-state-of-art-pre.html) and [GPT-2](https://openai.com/blog/better-language-models/). I'm not as familiar with either of these models as I should be, but from my understanding, there are extremely large unsupervised NLP models using the massive amount of unlabeled text available on the web. GPT-2 is a generative language model that can be used to write long paragraphs (or essays) of text, whereas BERT is a question-answer based system that Google built and employed to improve Google Search. They are both based on a Transformer model which uses self-attention to learn and understand the relationships of words to each other in a given sequence. My advisor gave me three links that do a good job of explaning these models. 

* [Transformers](https://jalammar.github.io/illustrated-transformer/)
* [GPT-2](https://jalammar.github.io/illustrated-gpt2/)
* [BERT](https://jalammar.github.io/a-visual-guide-to-using-bert-for-the-first-time/)

One of the conclusions that me and my advisor came to after our first meeting was that a good direction for the project would be in exploring the application of the Transformer model to music. Because both of us are relatively uneducated on the topic, we weren't sure what what would work may have already been done in this area and to what extent it would be feasible. This caused me to go down quite the rabbit hole of paper reading this week and although there is a substantial amount of more research that I need to do, this is what I was able to find.  

### Music Generation with Transformers
Google and their [Magenta](https://magenta.tensorflow.org/research) research group have already done a fair amount of work in applying transformers to music generation. At the heart of their research is their initial [Music Transformer](https://magenta.tensorflow.org/music-transformer) model. This model uses a decoder only relative self-attention model that can compose music with long term structure. There are several variants and other applictions of the model which they use for different projects (the the Magent website). Given that Magenta has done quite a bit of exploration in this field, I am left wondering if the topic is worth exploring. Here are a few questions that I have after doing my initial research 
* What are the limitations of their current model and why do they exist?
* Would it be worth it to dive into the details of a Music Transformer with relative self-attention to try to build a newer model or architecture that can outperform their current model? 
* Can we build a large scale general purpose model like GPT-2 and BERT but with it's applicatin to music? What sort of data would be required to do this and where would we get it from?
* What are some applications of music generation with Transformers that have not been explored yet? Can we combine the Transformer with other architectures (as Magenta has already done) to create novel functionality for music generation?
* Is it possible to use their Transformer architecture as an application to understanding expressiveness?

### Musical Expresiveness and its Potential
The last question that I posed is only one of many that I have in regards to musical expressiveness. One of the difficult things about expressiveness as a research subject is that (at least to my eyes) it is not well defined. Most of the literature commonly refers to musical expressiveness as the timing and dynamics of an actual musical performance, but to me it seems that there are many other deeper dimensions to the problem that can be explored. The first thing that comes to mind is the "phrasing" of a musical piece and how it relates to the timing and dynamics. Most classical music scores (especially in piano) are chock full of phrasing markers in the music that indicate the emphasis that particular piece of the music should have. The most common "phrase" of a score is to emphasize the top voice in the right hand as the melody of the song. My question is, how would something like this be modeled from a computational perspective? It certainly seems possible to do (although not explicity) in the MIDI, or related, format. Related to the phrasing of a score is the articulation which a performer gives to certain notes in the performance of a piece. There are no doubt many other aspects of a score and performance of music that cannot simply be explained by "timing and dynamics". I don't have a good enough of an understanding of music and music theory to actually answer that question, but it is worth thinking about. Given all of this, there are a few questions that I would like to answer, some of which may serve as the overall goal of the thesis itself 
* How is the score of a piece of music represented computationally as opposed to the performance of a piece? It is certainly possible to represent the performance of a piece of music with MIDI, but how is the score of the music represented in relation to that? This is useful becuase the direct comparison of a score and a performance could be useful for answering a number of questions regarding the interpretation of a piece of music and what "expresiveness" is. 
* To what extent can musical expressiveness be analyzed in an unsupervised way? That is, given a dataset of performances of music (see the [MAESTRO](https://magenta.tensorflow.org/maestro-wave2midi2wave) dataset) what type of information can we learn about expressiveness without the score of the music. This is directly related to using Transformers for modeling music because they 'learn' the structure of the piece. Is it possible to differentiate between the structure of the music itself and the expressiveness with which it's played?


### Towards a feedback/tutor system for learning music
As of now the big picture for the thesis project is to work towards building the tools for an intelligent tutoring system for learning music. I have had a number of ideas that relate to this but am not entirely sure how the research that I've already done could apply. The first thing I want to do is list out my ideas for some of the tools that could be useful for such a system. All of the ideas have the piano as the instrument in mind, but could be easily adapted to other instruments. 
* A "spell-checker" for music playing both for drills (scales and arpeggios) and songs. This would mean listening to a performance of a piece (either through raw audio or recorded MIDI), checking it for errors and reporting them back to the player. It is important to note that systems like this already exist but they are focused almost soley on pitch and timing (meaning was the right note played at the right time). Such systems would benefit from an analysis of the *expressivety* of the piece of music. Was the phrasing correct (the melody receiving the focus it needs to in the right places)? Were the dynamics observed (crescendos and descendos)? Was the pedaling correct? There are several extensions to this that could be possible that include teaching the student when mistakes are observed. 
    * Suggesting the fingering for a specific part
    * Suggesting a specific practice drill for a common type of mistake. 
    * Playing the music "correctly" so that the student can hear. Would be more useful if the audio is synthesized in such a way that it sounds near identical to the students piano setup. 
    * Slowing the piece of music down and speeding back up again when a mistake is corrected. 
* A drill and song generator for practice. This could build off of the spell-checker by recognizing common mistakes in the song and generating a drill that specifically addresses a certain weakness. It could also just exist as a useful practice tool, allowing a user to specify novel drills in a specific key to prevent pure memorization of music. Could be useful for site reading exercises. 
* A style analysis tool that can compare a performance of a piece to others. 
* An intepretation guidance tool that can make suggestions for how to play a certain part of a song
* Analyzing the physical posture and/or fingerings of the student performance (would involve sophisticated computer vision). 
* A composition guide that provides suggestions for writing during the creative process. Systems like this already exist but it would be useful if they were more interactive with the user. The first use case I can think of is "playing with" the user as they are sitting at their instrument, as opposed to using a pure GUI. 

I'm sure that there are more ideas that I have had before that are not coming to mind. The point is that there is a lot of opportunity for advancement in the area. The question then becomes, how do I connect the modeling and problem framing that I identified earlier in the post with a specific tool or application just mentioned? I think this is the million dollar question, and one that I will answer as I do further exploration. 

### Updates to My Goals
Because the goals and success definition are due on Monday I'll need to prepare something. I think that I will just build on what I have now with feedback from my advisor. I'll bring up some of the concerns that I have with my advisor to see if he thinks they are worth addressing in these goals and maybe I can address some of them before Monday. If not, they will have to stand as they are, with the understanding that there might be large modifications further down the road. 

