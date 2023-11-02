# ChatBOT

## Overview

This README provides an overview of creating a chatbot using a Transformer-based model. A chatbot is a type of software that can help humans by automating conversations and interacting with them through messaging platforms or it’s just a form of artificial intelligence (AI) that interact with humans. It can be used for customer service, request routing, information gathering, and simple chit-chat. There are several gadgets in the market specially designed for Virtual assistance like Alexa, Google home, etc and some may find that virtual assistance on any online service providing website and telling the difference whether the replies generated from the machine or a human might not be easy, ever wondered how they work? let’s build our own chatbot completely from scratch using TensorFlow without using any kind of predefined APIs.

### Table of contents:-
1. Prerequisites
2. Setup
3. Training the Chatbot
4. Results
5. Deploying the Chatbot
6. Future Improvements

### 1. Prerequisites
   
Before you begin, ensure you have the following prerequisites:

1. Python (version 3.6 or higher)
2. TensorFlow (for implementing the Transformer model)
3. GPU (recommended for faster training)
4. A large dataset of conversations (e.g., dialogue datasets)
5. A basic understanding of machine learning and neural networks

### 2. Setup

####  2.1 Install Dependencies

You will need to install the necessary libraries. You can use 'pip' to install these packages:

####  2.2 Data Preparation

We have provided the Cornell Movie-Dialogs Corpus dataset and It contains more than 130 thousand refined replicas from 617 films, actually, there were 220K dialogue pairs but they cleaned the data i.e. too long dialogues had been removed, provided 7 features-

1. id: serial number
2. question: a string representing questions
3. answer: a string representing answers
4. question_as_int: tokenized question
5. answer_as_int: tokenized answer
6. question_len: no. of words in question
7. answer_len: no. of words in answer

Our features of concern are ‘question’ and ‘answer’.

### 3. Training the Chatbot by using TRANSFORMER

 1. Data Preprocessing:

    We have given a CSV file, we have converted it into a pandas data frame and took only two columns ‘question’ and 
    ‘answer’, and then cleaned it i.e. removal of special characters, decontraction, etc, then divided it into 
    train/validation data frames. As neural network doesn’t understand English, all they want is the numerical 
    representations, so to convert each word into a numerical number we need tokenization, We’ve used subword 
    tokenization.
   
2. Positional Encoding and Masking (Pad Mask and Lookahead Mask):

   To preserve sequence information and relative positions of the words, we do the positional encoding. This is done 
   after representing each token into its embedding vector i.e. if we have {23, 38, 1, 0, 0} as tokens then after 
   passing it to the embedding layer this tokenized sentence will convert into a 5X100 dimn matrix, 100 is embedding 
   vector length.
   
   Masking is a way to tell sequence-processing layers that certain timesteps in an input are missing, and thus 
   should be skipped when processing the data.
   
   Padding is a special form of masking where the masked steps are at the start or the end of a sequence. Padding 
   comes from the need to encode sequence data into contiguous batches: in order to make all sequences in a batch 
   fit a given standard length, it is necessary to pad or truncate some sequences.
   
   Lookahead masking is only for the decoder part, as we will be generating/predicting words one by one i.e. if we are
   generating the first word then we will not be calculating ‘self-attention’ for the second word which has not been 
   generated yet, if have predicted 3 words then masking will be done for the remaining words which are going to be 
   predicted.

   
3. Self-Attention and Multi-Head Attention:

   Self Attention allows transformer models to attend to different parts of the input or output sequences when making predictions.The self-attention mechanism is the heart of the transformer, allowing the model to weigh the importance of different words in a sentence based on their affinity with each other. These mechanisms are crucial for the performance of transformer models in tasks such as language translation, text summarization, and sentiment analysis, where the model needs to understand the relationships between different words or phrases in the input and output sequences.
   
   Multi head Attention is nothing but the calculation of ‘self-attention’ multiple times to extract multiple types of attention for each word in a sentence.

5. Encoder and Decoder:

   The transformer architecture is composed of an encoder and a decoder, each of which is made up of multiple layers of self-attention and feedforward neural networks.

   The encoder takes in the input sentence and produces a fixed-size vector representation of it, which is then fed into the decoder to generate the output sentence.

   The decoder uses both self-attention and cross-attention, where the attention mechanism is applied to the output of the encoder and the input of the decoder.

7. Transformer:

   Encoder call --> decoder call --> dense layer --> word tokens, the final dense layer will of ‘answer’ vocab size, 128 X 10 X 512 shaped tensor as the decoder output passed through a final dense layer having ‘answer’ vocab_size number of dense units, so final dense layer output tensor will be of shape 128 X 10 X 27360 (tokenizer_a.vocab_size +2), where ‘128’:batch_size, ‘10’: answer input seq length.

### 5. Results-

Train the model by adjusting hyperparameters and no. of epochs. More the no. of epochs trained better will be responses/answers by our Chatbot.

### 6. Deploying the Chatbot

There are several ways to deploy your chatbot:

1. Web Application: Create a web-based chatbot using frameworks like Flask, Django, or FastAPI.
2. Messaging Platform: Integrate your chatbot with messaging platforms like Facebook Messenger, Slack, or WhatsApp.
3. Command Line Interface: Build a command-line interface for local usage.

In our case we have deployed it using Web Application.

### 7. Future Improvements

To enhance our chatbot, you can consider the following improvements:

1. Improve training data quality and quantity.Collect more data, increase embedding vector size, increase repetition of encoder and decoder layer, and change the number of multi-heads.
2. Experiment with different Transformer architectures (e.g., GPT-3, BERT).



   


