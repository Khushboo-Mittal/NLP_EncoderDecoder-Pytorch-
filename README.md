# NLP_EncoderDecoder-Pytorch-
This project implements a sequence-to-sequence (Seq2Seq) model using an Encoder-Decoder architecture to perform sentiment analysis on a Twitter sentiment dataset. The model is built in PyTorch, utilizing GRU (Gated Recurrent Unit) layers to handle text input. The goal of this project is to classify tweets into different sentiment categories (positive, negative, neutral, and irrelevant).

# Table of Contents

- Project Overview
- Dataset
- Installation
- Key Concepts
- Data Preparation
- Training and Evaluation
- Getting Started 
- Model Architecture
- Requirements

# Project Overview

The Encoder-Decoder model is commonly used in natural language processing tasks like machine translation and text generation. Here, we adapt it to perform a classification task—predicting the sentiment of a tweet. This README includes the necessary background, setup, and detailed descriptions of key components.

## Dataset
The dataset consists of tweets with the following columns:
- `tweetID`: Unique identifier for each tweet.
- `sentiment`: Sentiment labels (Positive, Negative, Neutral, Irrelevant).
- `tweet_content`: The content of the tweet.

## Installation
Make sure to have the following libraries installed:
```bash
`pip install pandas scikit-learn torch torchtext`

# Key Concepts

**1. Tokenization**
Tokenization is the process of splitting text into individual words or tokens. Tokenization allows us to represent each word as an input to the model. Here, we use the "basic_english" tokenizer from PyTorch.

**2. Vocabulary**
The vocabulary is the set of unique tokens or words that the model will recognize. We build our vocabulary using the tokenized dataset, and it includes special tokens for unknown words ("<unk>") and padding ("<pad>") to handle varying sentence lengths.

**3. Embeddings**
Word embeddings are dense vector representations of words, mapping words into a continuous vector space where similar words have similar embeddings. This project uses embeddings in both the Encoder and Decoder models to represent input text in a form that the model can process effectively.

**4. Encoder**
The Encoder processes the input text sequence and generates a context or hidden state that represents the entire input. This hidden state is then passed to the Decoder. In this project, the Encoder uses:

Embedding layer: Converts each word into a dense vector.
GRU layer: Processes the sequence of embeddings to generate the hidden state.

**5. Decoder**
The Decoder generates the final output (sentiment classification) based on the hidden state provided by the Encoder. The Decoder also has:

Embedding layer: Transforms input into dense vectors.
GRU layer: Processes the sequence to produce hidden states.
Fully connected (Linear) layer: Maps the hidden state to the output classes.

**6. Loss Function**
We use Cross-Entropy Loss for classification tasks, which calculates the difference between the predicted class probabilities and the actual labels.

**7. Backpropagation**
Backpropagation is the process of adjusting model weights based on the error between predicted and actual values. Gradients are calculated using the chain rule and are used to update weights to minimize the loss function.

**8. Optimization**
The Adam optimizer is used to update model parameters. It combines the advantages of both momentum and adaptive learning rates for efficient training.

# Data Preparation

- Load Dataset: The Twitter sentiment dataset is loaded and preprocessed.
- Preprocessing:
Remove stopwords, punctuation, and lowercase all text.
Perform tokenization, stemming, and lemmatization.
- Encoding Sentiment Labels: Encode the sentiment labels into integers:
Positive = 1
Negative = 0
Neutral = 2
Irrelevant = 3
- Vectorization: TF-IDF and Word2Vec embeddings are used to represent the text for training.

# Training and Evaluation

- Training Loop:
Define the number of epochs and set the model to training mode.
- Use Cross-Entropy Loss and the Adam optimizer.
For each batch, calculate loss, perform backpropagation, and update weights.
- Evaluation:
The evaluation function calculates the model’s accuracy and classification report on the validation and test sets.
python

# Getting Started

To get started with this project:

- Load your Twitter dataset (`twitter_sentiment_analysis.csv`), ensuring it contains columns such as `tweetID`, `sentiment`, and `tweet_content`.
- Preprocess the data: The script automatically encodes sentiments and tokenizes the tweet content using a basic English tokenizer.
- Create a Vocabulary: Use `build_vocab_from_iterator` to construct a vocabulary from the tokenized tweets, handling unknown tokens appropriately.
- Prepare the DataLoader: Create `DataLoader` instances for training, validation, and test datasets to facilitate batching during training.
- Define the Model: Implement the Encoder, Decoder, and Seq2Seq classes for the sentiment analysis model.
- Train the Model: Run the training loop to optimize the model's parameters using the training DataLoader and monitor the loss over epochs.
- Evaluate the Model: Use the evaluation function to assess model performance on the validation and test datasets, generating accuracy metrics and classification reports.

# Model Architecture

The architecture of this project consists of a sequence-to-sequence (Seq2Seq) model, which is structured as follows:

1. **Encoder**:
   - **Embedding Layer**: Converts input tokens (words) into dense vectors of specified dimensions.
   - **GRU Layer**: A Gated Recurrent Unit (GRU) processes the embedded input sequences, capturing contextual information and producing a hidden state that summarizes the input.

2. **Decoder**:
   - **Embedding Layer**: Similar to the encoder, this layer converts output token indices (sentiment labels) into dense vectors.
   - **GRU Layer**: Processes the embedded inputs along with the hidden state from the encoder to generate predictions for each time step.
   - **Fully Connected Layer**: Maps the GRU output to the output vocabulary size, producing logits for each sentiment class.

3. **Seq2Seq Model**:
   - Combines the encoder and decoder into a cohesive unit that takes input sequences (tweets) and generates sentiment predictions.

The model is trained using cross-entropy loss, optimized with Adam, and evaluated on accuracy metrics. This architecture effectively learns to predict sentiment from input text by leveraging the relationships between tokens through their embeddings and recurrent processing.

# Requirements

To run this project, you will need the following Python packages:

- **pandas**: For data manipulation and analysis.
- **torch**: The core library for building and training neural networks (PyTorch).
- **torchtext**: For handling text data and pre-processing.
- **scikit-learn**: For machine learning tools, including metrics for evaluation.
- **numpy**: For numerical operations.

# Results

The Encoder-Decoder model, trained on the Twitter sentiment dataset, demonstrates strong performance across both the validation and test sets, indicating effective generalization and accurate sentiment classification.

Validation Accuracy: 90.67%
Test Accuracy: 93.42%

# Contributor	              Role/Responsibilities

## Contributors

| Contributor      | Role/Responsibilities                                       |
|------------------|-------------------------------------------------------------|
| **Khushboo Mittal**       | Data preprocessing, Tokenization |
| **Prachi Tavse**                |Encoder (Embedding, GRU for Hidden State Generation) |
| **Harshita Jangde**                |Decoder (Embedding, GRU, FC Output) and Seq2Seq (Encoder-Decoder Integration) |
| **Tanisha Priya**                | Initialize Model, Train, and Evaluate Accuracy with Classification Report |
