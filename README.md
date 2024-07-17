# Using Deep learning to perform summarization on long text

In this project, we want to consider various approaches that can deal efficiently with long text and try to compare the efficient of each approach based on evaluating on the specific long document dataset. In particular, we try to 2 approaches: **End-To-End efficient attention** and **Retrieve-Then-Summarize**.

## Approaches

### 1. End-To-End efficient attention
We try to various options to design: **Sliding Window**, **Dilated Sliding Window**, **Global Attention** help to self-attention will scale linearly with input sequences.

![image](https://github.com/user-attachments/assets/e8cb13a8-cdba-4156-9c63-ae42a6be5e6a)

By applying those options, we use the **Longformer Encoder Decoder** model which help us to cope with the long text better.

References: Iz Beltagy, Matthew E. Peters, Arman Cohan(2020): Longformer: The Long-Document Transformer (https://arxiv.org/abs/2004.05150)

### 2. Retrieve-Then-Summarize

Based by the paper **Long-Span Summarization via Local Attention and Content Selection**, we will combine **Ground-truth based(ORACLE)** and **Model based** retrieve the content efficiently in the training and using **Multitask Content Selection** in the inferencing phases.

![image](https://github.com/user-attachments/assets/6ba88d6f-2371-4920-8439-2ad5631b353b)

For details, you can read our reports.

## Experiments
We try those approaches with BART model (for comparing) to perform summarization on the **PubMed dataset** and use family of **ROUGE** score to evaluate.

Here is our results: 

| Model        | R1          | R2  | RL| RL-Sum|
| ------------- |:-------------:| -----:|-----:|-----:|
BART- 1024 | 33.58 | 11.37 |18.96| 30.21
BART-1024-CS |35.67 |12.72 |19.96 |32.20
LED - 4096 |42.72 |13.86 |21.06 |37.39
LED - 4096 - CS |43.68 |14.25 |21.42| 38.14
**LED - 8192** | **44.67** | **15.49** | **22.56** | **39.30**

## Installation and usage

First, clone this repository 

<!-- start:code block -->
### 1. Clone this repository
git clone 
cd papermark

### 2. Install dependencies
pip install gradio

pip install transformers

### 3. Run 
Run the **Inference NLP.ipynb** file code and try the demo in the **Gradio** section in file.






