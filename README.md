Using Deep learning to perform text summarization task

**1) Definition:** Summarization is the task of producing the shorter version of document while preserving its important information

**2) Types:**

- Extractive summarization : Extract sentences or phrases from the original text.
    
- Abstractive summarization: Need to understand the global semantic of the original text and produce the new text.

In this project, I focus on the abstractive summarization.

**3) General method:**

- The Abstractive summarization is the intersection of 2 tasks: NLU (**Naltural Language Understanding**) and 
    NLG(**Natural Language Generation**).
    
- Based on that, the ABS model usually contructed as the encoder and decoder architecture.

  **Here is the image of general ABS model:**
  ![image](https://github.com/VuLamAnh151203/Text-Summarization_NLP_20232/assets/131300862/347a8ed3-ca5d-42d5-9447-52a50222c9ef)

  1) **Processing step**:
     - Linguistic technology to structure the input text(Sentence segmentation, word tokenization, stop-word removal,...)
  2) Semantic Understanding:
     - Use the neural network to recognize and represent the deep semantics of the input text.
     - This process occurs in the vector space and output the fusion vector that represent whole thing.
  3) **Summary Generating:**
     - Maps the fusion vector to the vocabulary to generate summary works.
    
**4) Difficulties in ABS:** 

  1) **Out-Of-Vocabulary Word:** In the input text has some words may be not exist in the vocabulary list.
  2) **Repeated Phrases or Sentences:** When dealing with the long text, there may have the cases where multiple identical sentences appeared in the summary.
  3) **Factual Error** : The information in the summary is not consistent with the information provided by the original text.
