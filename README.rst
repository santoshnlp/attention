##################
Table of Contents
##################
.. contents::
  :local:
  :depth: 4

***************
Data Preparation
***************
.. image:: https://github.com/santoshnlp/attention/blob/main/LSTM-Input.png
      :target: https://twitter.com/amirsinatorfi
      
***************
Embedding Layer
***************

***************
LSTM cell
***************
.. image:: https://www.researchgate.net/profile/Xuan_Hien_Le2/publication/334268507/figure/fig8/AS:788364231987201@1564972088814/The-structure-of-the-Long-Short-Term-Memory-LSTM-neural-network-Reproduced-from-Yan.png

In this project LSTM cell is used in encoder and decoder.   Here I will briefly describe the inputs and outputs of a LSTM cell.

========================
Inputs to a LSTM cell
========================

LSTM cell expects three inputs:
     1. Cell state
     2. Hidden state
     3. Input
     
     Cell state and Hidden state are of same dimensions.  The Input dimension depends on the embedding vector.  
     
========================
Outputs from a LSTM cell
========================

LSTM cell provides three outputs:
     1. Cell state
     2. Hidden state
     3. Output
     
     Output is of same dimension as Hidden state.
     
***************
Encoder
***************

***************
Attention mechanism
***************

.. image:: https://github.com/santoshnlp/attention/blob/main/Attention.png

=================
STEP-1
=================

In the decoder part the input word embedding (output language) is obtained.  In the first time step it is SOS_token.  In the subsequent time steps it is same as the the word predicted in previous time step. 


=================
STEP-2
=================

The input word embedding (output language) is concatenated with decoder hidden state. 
At the beginning the input word to decoder is SOS token and the hidden state is the last hidden state obtained through encoder.



=================
STEP-3
=================

The concated vector in STEP-2 is passed through a FC layer.

--------------------
Input layer size
--------------------

Clearly the input layer size = Word embedding size + Decoder hidden size.

In our case both are 256. Therefore input layer size = 256+256 = 512.

--------------------
Output layer size
--------------------

The purpose of this layer is to tell on which word or encoder outputs more weightage should be given.

The number of encoder outputs for a given input sentence depends on number of tokens in the input sentence.

We have already seen that the maximum number of words for a given sentence in input language is equal to 10.

So the output layer size should be 10. This way all the sentences will be handled.






***************
Decoder
***************

