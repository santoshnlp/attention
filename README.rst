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
***************
Decoder
***************

