---
layout: post
title: Named Entity Recognition
date: 2019-06-19
---

*Author's note: This is a badly written summary of Named Entity Recognition which I have pieced together while reading up on it.*

## What is NER?

Named Entity Recognition seeks to locate and classify named entity mentions in unstructured text into pre defined categories.

E.g. in a sentence “Barack Obama was the 44th president of the United States of America”, we would recognize “Barack Obama” as Person and “United States of America” as Country.

## How is NER performed?

There are two main ways to perform named entity recognition: linguistic grammar-based techniques and statistical techniques.
    
Linguistic grammar-based techniques use handcrafted rules, painstakingly created by a domain expert. An example of handcrafted rules could be: (a) if numbers are 16 digits long, beginning with 4, it’s a Visa card number (b) a list of all professional tennis players. This is used when no training data is available.

Statistical techniques usually require a large amount of manually annotated training data. It is used when you cannot exhaustively list all entities. Conditional Random Fields (CRF) is a commonly used named entity recognition method.

## More about statistical NER techniques

### What is CRF?

A discrete classifier predicts a label for a single sample without considering neighbouring samples, whereas a linear chain CRF can predict sequences of labels for sequences of input samples. 

Let **x = (x1, x2, …, xm)** be the words in a sentence (inputs).

Let **s = (s1, s2, …, sm)** be the named entity tags (outputs).

**p \(s1, …, sm \| x1, …, xm\)** is the probability of the sequence of named entity tags given the sequence of words. 

We can model **p \(s \| x, w\)** by a log-linear model, where **w** is a parameter vector. We find the optimum **w** which maximises the log likelihood function **L** with regularization.

With the optimum **w**, we then find the maximum sequence **s** which maximises **p \(s \| x, w\*\)**.

CRF allows us to find the sequence of named entity tags which is most likely, given the words in the sentence.

This is a very good article to learn more about CRF: [https://www.depends-on-the-definition.com/named-entity-recognition-conditional-random-fields-python/](https://www.depends-on-the-definition.com/named-entity-recognition-conditional-random-fields-python/).

Long Short Term Memory (LSTM) is another statistical method that is used for named entity recognition. It is often used to supplement the CRF model.

### What is LSTM?

A neural network is a set of algorithms that are loosely modelled after the human brain.

A traditional neural network just has input data **x** passed through it to generate output data **y**. Whereas a recurrent neural network has input data **x_(t-1)** passed through it, output data **y_(t-1)** generated, input data **x_(t)** and output data **y_(t-1)** passed through it, output data **y_(t)** generated, and so on, in a loop. This allows the model to have persistence, i.e. using knowledge of events in the past to inform current decision.

Using knowledge of past events is helpful in many cases, such as in NLP, where earlier words in the sentence can be used to guess the current word correctly, in video analytics where previous video frames can be used to understand the present frame better.

At times a lot of previous knowledge is required (e.g. predicting the next word requires the whole sentence: In France, most people speak \<FRENCH\>), at times very little previous knowledge is required (e.g. predicting the next word only requires the few words before: there are clouds in the \<SKY\>). Although theoretically sound, RNNs actually don’t do very well when too much previous knowledge is required.

LSTM solves this problem. It is a special kind of RNN that is capable of learning long-term dependencies. They are good at remembering information for a long period of time.

This is because, instead of a single neural network layer in each repeating module, it has four neural network layers interacting in a special way that enables it to remember information for a long period of time.

This is a good article to learn more about LSTM: [http://colah.github.io/posts/2015-08-Understanding-LSTMs/](http://colah.github.io/posts/2015-08-Understanding-LSTMs/)

LSTM would be good for named entity recognition because it can use the previous entities to make better decision about what the current entity should be.

There are several named entity recognition models proposed which uses LSTM, CRF or a combination of both.
