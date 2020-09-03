---
title: "An Assessment of Learned Score Features for Modeling Expressive Dynamics in Music"
date: 2020-06-01T20:37:46-06:00
draft: false
---

* [Google Scholar Link](https://scholar.google.com/scholar?hl=en&as_sdt=0%2C45&q=An+Assessment+of+Learned+Score+Features+for+Modeling+Expressive+Dynamics+in+Music&btnG=)
* [Content Link](https://ieeexplore-ieee-org.ezproxy.lib.utah.edu/stamp/stamp.jsp?tp=&arnumber=6762927)

# Abstract
The study of musical expression is an ongoing and
increasingly data-intensive endeavor, in which machine learning
techniques can play an important role. The purpose of this paper
is to evaluate the utility of unsupervised feature learning in the
context of modeling expressive dynamics, in particular note
intensities of performed music. We use a note centric representation of musical contexts, which avoids shortcomings of existing
musical representations. With that representation, we perform
experiments in which learned features are used to predict note
intensities. The experiments are done using a data set comprising
professional performances of Chopin’s complete piano repertoire.
For feature learning we use Restricted Boltzmann machines, and
contrast this with features learned using matrix decomposition
methods. We evaluate the results both quantitatively and qualitatively, identifying salient learned features, and discussing their
musical relevance

# Notes by Section

## 1. Introduction
* Music Expressiveness has previously been limited to musicology or psychology. Recent efforts are moving to data mining and machine learning 
* Past models have heavy focus on hand-designed features for score representation
* Limited to note intensities in classical piano performances

## 2. Related Work
* Application of unsupervised feature learning in music is new but is gaining popularity. I think paper was written in 2014? Not sure how true this is today

## 3. Feature Learning
### A. Data Representation
* Use piano roll for the input data to look at Chopin's full set of music. Not entirely sure how this data is represented digitally. Need to look at the dataset being used
### B. Principal Component Analysis
### C. Nonnegative Matrix Factorization
### D. Restricted Boltzmann Machines
### E. Stacked Restricted Boltzmann Machines
### F. Features and Basis Images
* All of the above mentioned methods are quite different for learning the features. 
* In common, they map data from input space to a new learned space. 
* Dimensions of new space are the features
* Each feature has basis image, which is dimensionality of original space. 

## 4. Methodology
### A. Data 
* Using Magalof Corpus. Need to look at dataset, not sure how exaclty it is represented. 
    * Just found the paper and the score information is represented in MusicXML and the performance is in MIDI. I am not sure why this paper uses piano roll as the representation. 
### B. Prediction of Note Intensities with Learned Features
* They use linear regression to predict note intensities given the learned feature representation. 
* The note intensity is represented as midi velocity 
* Goal is to predict that intensity. 
### C. Prediction Measure
* Prediction Measure is R^2


# Thoughts
I didn't finish the whole paper where he goes to talk about the results. The short of it is the the RBM method works the best for learning the features. One of the interesting things about this paper is that he uses a few different versions of the piano roll representation for the input score data and I am not sure exactly how he is representing the score in this way. One of my biggest problems right now is in understanding how to represent the data and what the output of my model is going to be. I am gaining just a little bit more clarification the more papers I read but I am still very confused on how to represent the data, especially in a musical context. I think that one of the things that is becoming somewhat clear to me however is that I will follow a similar approach to what he is doing in this paper. 

That approach is probably going to involve getting score data in the form of MusicXML for either all of the MAESTRO dataset or at least a significatn chunk of it, and making sure that the dataset is good and makes sense. The next thing will be to take the score data in the form of MusicXML and create some sort of feature learning model to output a feature space over the input data. Then I can use a normal model (in the case of this paper he uses linear regression) to predict the expressiveness of the piece and use the midi data as a comparison. 

There are all sorts of questions surrounding how to represent the input data, what type of model to use, and what type of expressive parameters that I am trying to model in the MIDI data. The other question might be, how do we tell a user of the system or model that their generated performance does not match up to what we want it to be? That might be question that is outside the scope of the thesis, but one that I will want to eventually explore. 