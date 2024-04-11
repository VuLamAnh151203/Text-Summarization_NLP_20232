# Using Deep learning to perform text summarization task

## I. Introduction to Text Summarization

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
  2) **Semantic Understanding**:
     - Use the neural network to recognize and represent the deep semantics of the input text.
     - This process occurs in the vector space and output the fusion vector that represent whole thing.
  3) **Summary Generating:**
     - Maps the fusion vector to the vocabulary to generate summary works.

## II. BART model:

1. Definition:
Bart model is the model which pre-trains a model combining Bidirectional and Auto-Regressive Transformers. It uses the standard sequence-to-sequence Transformer architecture from (Vaswani et al., 2017), except, following GPT, that we modify ReLU activation functions to GeLUs (Hendrycks & Gimpel, 2016) and initialise parameters from N(0,0.02). It pre-trained the task of reconstructing the denoising text go back to the original text.

![image](https://github.com/VuLamAnh151203/Text-Summarization_NLP_20232/assets/131300862/cfe51dc6-fe63-450e-ad16-803d66e52990)

(Source : BART: Denoising Sequence-to-Sequence Pre-training for Natural Language Generation, Translation, and Comprehension Mike Lewis*, Yinhan Liu*, Naman Goyal*, Marjan Ghazvininejad,Abdelrahman Mohamed, Omer Levy, Ves Stoyanov, Luke Zettlemoyer )

2. Pre-training stage:
   2.1) Text is corrupted with an arbitrary noising function.
   2.2) Use seq2seq model to recontruct the original text.

3. Why we choose Bart model for Text summarization:
   Since bart model has autoregressive decoder, it can be directly fine-tuned for text generation task such as text summarization. Moreover, with the task of the summarization, we cank think the input text as the corrupted outout text, so we need to reconstruct original output text, then it's very similar to the pre-trained task in bart.

## III. Fine-tune model:

1. Pre-trained model:

   I choose the pre-trained model: sshleifer/distilbart-xsum-12-3. This model is light-weight bart model fine-tune in the Extreme Summarization dataset (Originated in: Don't Give Me the Details, Just the Summary! Topic-Aware Convolutional Neural Networks for Extreme Summarization Paper https://arxiv.org/pdf/1808.08745v1.pdf).

2. Datasets:
   The dataset I choose to fine-tune model, also illustrate and evalute the summarization model: NEWS-SUMMARY (https://www.kaggle.com/datasets/sunnysai12345/news-summary). It contains the summarized news from Inshorts and only scraped the news articles from Hindu, Indian times and Guardian. Time period ranges from febrauary to august 2017.

3. Implementation:
   - Strategy: I use first 1000 pairs of document-summary for evaluation and the rest for training.
   
   - I use the ***transformer hugging face** library to get the pre-trained model, fine-tuning, inference, evaluation task.

   - I also evaluate the model with **rouge** score through **evalute*** library and ***BertScore*** through ***bert_score*** library.

5. Result:

   4.1 Evaluation metrics:
   
   - Loss: 3.1426
    - Rouge1: 51.2701
    - Rouge2: 28.3575
    - Rougel: 37.9263
    - Rougelsum: 45.8934

   4.2 Some example of actual result:
   
   - **The original text:** (source: https://e.vnexpress.net/news/football/ronaldo-threatens-to-punch-referee-after-getting-sent-off-4732175.html)
   
<sub>
    
       In the 86th minute of the game on Monday night, when Al Nassr were trailing 0-2 to Al Hilal, Ronaldo and defender Ali Al-Bulaihi went for the ball for a throw-in. Ronaldo got the ball and intended to make a quick throw, but the Saudi Arabian player rushed forward to take it because he thought the throw-in belonged to Al Hilal. But Ronaldo, captain of Al Nassr gritted his teeth and put his elbow out to prevent Al-Bulaihi from stealing the ball. Just as Bulaihi rushed forward, Ronaldo's elbow hit the 35-year-old defender’s neck and he fell down in pain.
    
    Referee Mohammed Al-Hoaish immediately gave Ronaldo a red card and sent him off. The Portuguese superstar was surprised, raised his fist towards Al-Hoaish and intended to punch him. At that time, the referee turned away and did not see Ronaldo's threatening action.
    
    This is the 12th red card in Ronaldo's career and the first time he has been sent off since 2018. On his way out, Ronaldo pointed at the referee, clapped mockingly and gave him a thumbs up. The 39-year-old striker is set to face suspension for this series of actions.
    
    Al-Bulaihi has repeatedly provoked Ronaldo in the Saudi derby games between Al Nassr and Al Hilal. One time he dived then stood up and Ronaldo ran after him and applauded. Al-Bulaihi also provoked Lionel Messi several times, when Saudi Arabia unexpectedly beat Argentina 2-1 in the opening match of the 2022 World Cup.
    
    Ronaldo lacked restraint when he encountered many difficulties against the Al Hilal, the team that hold the world record of winning 33 consecutive games in all competitions. He missed a relevant chance in the 17th minute, with a shot that went over the bar. According to Sofascore statistics, Ronaldo only had 33 touches on the ball in 86 minutes of play, missed six shots, had six wrong passes and lost the ball nine times.
    
    Al Hilal are the team with the richest tradition in Asia with 66 official titles, including title records in the AFC Champions League and Saudi Pro League. Coach Jorge Jesus's team are ranked 39th in the world, above Marseille, Villarreal or Wolverhampton, according to the power index of Opta. Meanwhile, Al Nassr are 89th, behind Nottingham Forest.
    
    The defeat against Al Hilal left Al Nassr with an only chance to get a title this season, which is the King Cup, a tournament similar to England's FA Cup. Al Nassr reached the semifinals and will meet Al Ittihad on April 30. Meanwhile, Al Hilal reached the final of the Saudi Super Cup and will play Al Ittihad on April 11."""
</sub>

- **The summary text:**

<sub>
    
     Portuguese striker Cristiano Ronaldo was sent off for the 12th time in his career after his elbow hit Al Nassr's defender Ali Al-Bulaihi's neck in the 86th minute of the Saudi Super Cup on Monday night. Ronaldo raised his fist towards referee Mohammed Al-Hoaish and intended to punch him. The referee gave him a red card and sent him off.

 </sub>


