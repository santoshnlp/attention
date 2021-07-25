##################
Table of Contents
##################
.. contents::
  :local:
  :depth: 4


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


=================
STEP-1
=================

As discussed in LSTM section, the cell state and hidden stae are intialized with zeros. The index of first word of sentence is
passed to embedding layer to get the embedding vector. This embedding vector is used as input to LSTM.

The LSTM cells gives 3 outputs. Cell state and hidden state are used by LSTM in next time step.  The output is saved to a list (tensor) . 

.. image:: https://github.com/santoshnlp/attention/blob/main/Encoder-Time-Step-0.png


=================
STEP-2
=================

Now the cell state and hidden stae are taken from previous time step. The index of second word of sentence is
passed to embedding layer to get the embedding vector. This embedding vector is used as input to LSTM.

The LSTM cells gives 3 outputs. Cell state and hidden state are used by LSTM in next time step.  The output is saved to a list (tensor) . 

.. image:: https://github.com/santoshnlp/attention/blob/main/Encode-time-step-1.png


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


This is the sample output of attention vector.

.. code-block:: python

 tensor([[ 0.6701,  0.5469, -0.0666, -0.2150, -0.2235,  0.6324,  0.0358, -0.2763,
          0.0725,  0.3550]], grad_fn=<AddmmBackward>)
          

=================
STEP-4
=================

Apply softmax to the output of Step-3

sample output

.. code-block:: python

 tensor([[0.1576, 0.1393, 0.0754, 0.0650, 0.0645, 0.1518, 0.0836, 0.0612, 0.0867,
         0.1150]], grad_fn=<SoftmaxBackward>)


=====================
STEP-5
=====================

Now we have the attention weights. These weights are basically telling how much focus we should lay on each of the the encoded vector ( There are 10 encoded vectors ). Lets use attention weights and encoded vectors to extract focus state.

====================
STEP-6
====================

From STEP-5 we got a vector rich in context. This vector carries the context information as it has components of relevant words. Now lets concatenate this vector to word embedding.


====================
STEP-7
====================

The vector obtained in STEP-6 has 256*2 dimension. We need to convert to 256.

This could be achieved through a FC network.

.. code-block:: python

  input_to_lstm_layer = nn.Linear(256 * 2, 256).to(device)
  
  
The output of this linear layer becomes input to LSTM cell.


***************
Decoder
***************

=================
STEP-1
=================

Here last outputs of encoder   i.e. cell state and hidden state are given as input to decoder.
Starting word is used as SOS token of output language. The word embedding and encoder states are used in attention mechanism as described in attention section.  The output of attention mechanism is used as input to the decoder.

.. image:: https://github.com/santoshnlp/attention/blob/main/Decoder-time-step-0.png

=================
STEP-2
=================

Now last outputs of decoder   i.e. cell state and hidden state are given as input to decoder.
The output from previous time step is used to get the next word. Rest is same as in time step 0.

.. image:: https://github.com/santoshnlp/attention/blob/main/Decoder-time-step-2.png



