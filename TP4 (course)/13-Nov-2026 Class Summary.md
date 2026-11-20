# Learning Notes

**Date:** 13/11/2026

## 1. Exact Match (EM)

### Definition

Exact Match (EM) is a metric that checks whether the model gives exactly
the same answer as the correct reference answer.

-   It is often used for question-answering, multiple-choice questions,
    and math problems.
-   If the predicted answer is exactly the same as the reference, the
    score is 1. If it is different, the score is 0.

**Formula:**

\[ EM = `\frac{1}{N}`{=tex}`\sum`{=tex}\_{i=1}\^{N} score_i \]

Where: - (N) = Total number of questions. - (score_i = 1) when the
prediction matches the reference exactly. - (score_i = 0) when the
prediction does not match.

### Normalized Exact Match

Since EM requires an exact match, some evaluations clean the text before
comparing it. This is called normalization.

Common steps are: - Change all letters to lowercase. - Remove
punctuation marks. - Remove extra spaces. - Remove articles such as "a",
"an", and "the", depending on the task.

**Advantages:** - Easy to calculate and understand. - Gives a clear
result for exact answers. - Works well for short and factual answers.

**Limitations:** - It is too strict for long or natural-language
answers. - Two answers can have the same meaning but get different
scores because they use different words. - Incorrect normalization can
remove important differences.

------------------------------------------------------------------------

## 2. Accuracy

### Definition

Accuracy shows the percentage or proportion of all predictions that the
model gets correct.

**Formula:**

\[ Accuracy = `\frac{TP + TN}{TP + TN + FP + FN}`{=tex} \]

Where: - TP (True Positive): The model correctly predicts a positive
case. - TN (True Negative): The model correctly predicts a negative
case. - FP (False Positive): The model predicts positive when the actual
result is negative. - FN (False Negative): The model predicts negative
when the actual result is positive.

**Advantages:** - Simple to calculate and understand. - Gives an overall
view of how well a classification model performs. - Useful when the
classes in the dataset are balanced.

**Limitations:** - It may give a misleading result when the dataset has
imbalanced classes. - It does not show the types of errors made by the
model. - A model may have high accuracy but still perform badly on a
minority class.

------------------------------------------------------------------------

## 3. Precision, Recall, and F1-Score

These three metrics help us understand a classification model's
performance in more detail. They are especially useful when the dataset
is imbalanced.

### Precision

Precision tells us how many of the cases predicted as positive are
actually positive.

\[ Precision = `\frac{TP}{TP + FP}`{=tex} \]

### Recall

Recall measures how many of the actual positive cases the model can
correctly find.

\[ Recall = `\frac{TP}{TP + FN}`{=tex} \]

### F1-Score

F1-Score combines Precision and Recall by calculating their harmonic
mean. It gives a balance between the two metrics.

\[ F1 = 2
`\times `{=tex}`\frac{Precision \times Recall}{Precision + Recall}`{=tex}
\]

**Advantages:** - Gives more information about model performance than
accuracy alone. - Helpful when the dataset contains imbalanced
classes. - F1-Score considers both Precision and Recall.

**Limitations:** - One overall F1-Score may hide how well the model
performs on each class. - The results depend on having correct
ground-truth labels. - It does not consider that some types of errors
may have a higher cost than others.

------------------------------------------------------------------------

## 4. BLEU Score (Bilingual Evaluation Understudy)

### Definition

BLEU is a metric first created to evaluate machine translation. It
checks how many word sequences in the generated text also appear in the
reference text. This comparison is based on n-gram precision.

An n-gram means a group of N consecutive words.

For example: - Unigram: "I" - Bigram: "I love" - Trigram: "I love AI"

### Evaluation Process

1.  Compare the generated text with the reference text.
2.  Count the n-grams that appear in both texts.
3.  Clip the matching counts so repeated words do not get extra credit.
4.  Calculate the modified n-gram precision.
5.  Apply a brevity penalty when the generated text is too short.

### Formula

**Brevity Penalty (BP):**

\[ BP =
```{=tex}
\begin{cases}
1 & \text{if } c \geq r\\
e^{(1-r/c)} & \text{if } c < r
\end{cases}
```
\]

Where: - (c) = Length of the generated text. - (r) = Effective length of
the reference text.

**BLEU Score:**

\[ BLEU = BP
`\times `{=tex}`\exp`{=tex}`\left`{=tex}(`\sum`{=tex}\_{n=1}\^{N}w_n`\ln `{=tex}p_n`\right`{=tex})
\]

Where: - (p_n) = Modified precision for each n-gram. - (w_n) = Weight
given to each n-gram level. - (N) = Maximum n-gram level, usually 4.

When all n-gram levels have equal weights, (w_n = 1/N).

**Advantages:** - Quick and low-cost to calculate. - Produces repeatable
results. - Commonly used to compare machine translation systems.

**Limitations:** - It does not directly check whether the generated text
is factually correct. - It may give a low score to a correct answer that
uses different wording. - It may not work reliably with very short
sentences.

------------------------------------------------------------------------

## 5. ROUGE Score (Recall-Oriented Understudy for Gisting Evaluation)

### Definition

ROUGE is mainly used to evaluate text summarization and other
text-generation tasks. It checks how much of the important information
in the reference text is also included in the generated text.

### Main Types of ROUGE

1.  **ROUGE-N (N-gram Overlap):** Counts the matching groups of N
    consecutive tokens between the generated text and the reference.
2.  **ROUGE-L (Longest Common Subsequence):** Finds the longest sequence
    of matching tokens that appear in the same order. The matching
    tokens do not have to be next to each other.
3.  **ROUGE-Lsum (Summary-level LCS):** Applies sentence-level matching
    and combines the matched reference-token positions when evaluating
    summaries.
4.  **ROUGE-W (Weighted Longest Common Subsequence):** Similar to
    ROUGE-L, but gives more credit to matching words that appear
    continuously.
5.  **ROUGE-S (Skip-bigram Overlap):** Checks matching pairs of words in
    the same order, even when other words appear between them.
6.  **ROUGE-SU (Skip-bigram plus Unigram):** Combines skip-bigram
    matching with individual-word matching. It can still give credit
    when there are shared words but no matching word pairs.

**Advantages:** - Suitable for checking the quality of text summaries. -
Offers several ways to compare generated text with reference text. -
Helps measure how much reference information is kept in the output.

**Limitations:** - It has limited ability to understand the meaning of
words. - It may penalize correct paraphrased sentences. - The result can
change depending on the language preprocessing and tokenization. - A
high ROUGE score does not always mean the summary is factually correct.

------------------------------------------------------------------------

## 6. METEOR Score (Metric for Evaluation of Translation with Explicit ORdering)

### Definition

METEOR is a metric that compares generated text with reference text. It
looks at matching words, their order, and words that have similar forms
or meanings.

### Evaluation Process

1.  Compare the generated text with the reference text.
2.  Find and align the words that match.
3.  Calculate Precision and Recall.
4.  Check the order of the matched words.
5.  Apply a penalty when the matching words are split into separate
    groups.
6.  Calculate the final METEOR score.

### Word Alignment

METEOR can match words in several ways:

-   **Exact match:** The words are exactly the same.
-   **Stem match:** The words have the same root or stem.
-   **Synonym match:** The words have similar meanings based on lexical
    resources.

### Formulas

**Precision:**

\[ P = `\frac{m}{\text{Number of candidate words}}`{=tex} \]

**Recall:**

\[ R = `\frac{m}{\text{Number of reference words}}`{=tex} \]

Where (m) is the number of words that are successfully aligned.

**Weighted F-Mean:**

\[ F\_{mean} = `\frac{10PR}{R+9P}`{=tex} \]

**Fragmentation Penalty:**

\[ Penalty = 0.5
`\times `{=tex}`\left`{=tex}(`\frac{chunks}{m}`{=tex}`\right`{=tex})\^3
\]

Where: - (chunks) = Number of separate groups of matched words. - (m) =
Total number of aligned word matches.

**Final METEOR Score:**

\[ METEOR = F\_{mean} `\times `{=tex}(1-Penalty) \]

**Advantages:** - Uses both Precision and Recall. - Can match words
through stemming and synonyms. - Considers the order of words. - More
flexible than metrics that only check exact n-gram matches.

**Limitations:** - It cannot confirm whether the generated answer is
factually correct. - It depends on language resources, such as stemmers
and synonym dictionaries. - It may not identify every possible
paraphrase.

------------------------------------------------------------------------

## 7. BERTScore

### Definition

BERTScore evaluates generated text by comparing the meaning of words
instead of only checking whether the exact same words are used.

It uses contextual embeddings from pretrained language models, such as
BERT, to compare words in the generated text and the reference text.

### Evaluation Process

1.  **Input:** Give the generated text and reference text to the metric.
2.  **Embedding:** A pretrained language model changes each token into a
    contextual embedding.
3.  **Similarity Calculation:** Calculate cosine similarity between the
    token embeddings.
4.  **Greedy Matching:** Match each token with the most similar token in
    the other text.
5.  **Calculate:** Use the matching results to calculate Precision,
    Recall, and F1-Score.

### Cosine Similarity Formula

\[ S\_{ij} = `\frac{x_i^T y_j}{\|x_i\|\|y_j\|}`{=tex} \]

Where: - (x_i) = Embedding of token (i) in the generated text. - (y_j) =
Embedding of token (j) in the reference text. - (S\_{ij}) = Cosine
similarity between the two token embeddings.

### BERTScore Formulas

**Precision:**

\[ P = `\frac{1}{|C|}`{=tex}`\sum`{=tex}*{x_i
`\in `{=tex}C}`\max`{=tex}*{y_j `\in `{=tex}R}S\_{ij} \]

**Recall:**

\[ R = `\frac{1}{|R|}`{=tex}`\sum`{=tex}*{y_j
`\in `{=tex}R}`\max`{=tex}*{x_i `\in `{=tex}C}S\_{ij} \]

**F1-Score:**

\[ F1 = `\frac{2PR}{P+R}`{=tex} \]

Where: - (C) = Tokens in the generated text. - (R) = Tokens in the
reference text.

**Advantages:** - Compares the meaning of text, not only the exact
words. - Can recognize some paraphrases and different words with similar
meanings. - Uses the context provided by pretrained language models.

**Limitations:** - Needs more computing resources than simple
text-overlap metrics. - The result depends on the selected pretrained
model and its settings. - Similar meaning does not always mean the
statement is factually correct. - It may give a high similarity score to
sentences that look similar but have different meanings.

------------------------------------------------------------------------

## 8. Word Error Rate (WER)

### Definition

Word Error Rate (WER) is commonly used in Automatic Speech Recognition
(ASR) to measure the number of word errors in a predicted transcription
compared with the correct reference transcription.

It counts how many words need to be replaced, removed, or added to make
the predicted transcription match the reference.

### Three Types of Errors

1.  **Substitution (S):** A correct word is replaced by a different
    word.
    -   Reference: "I like AI."
    -   Candidate: "I love AI."
    -   Error: "like" is replaced with "love".
2.  **Deletion (D):** A word from the reference is missing in the
    predicted text.
    -   Reference: "I like AI."
    -   Candidate: "I AI."
    -   Error: The word "like" is missing.
3.  **Insertion (I):** The predicted text contains an extra word.
    -   Reference: "I like AI."
    -   Candidate: "I really like AI."
    -   Error: The word "really" is added.

### Formula

\[ WER = `\frac{S+D+I}{N}`{=tex} \]

Where: - (S) = Number of substituted words. - (D) = Number of deleted
words. - (I) = Number of inserted words. - (N) = Total number of words
in the reference transcription.

### Evaluation Process

1.  Compare the reference transcription with the predicted
    transcription.
2.  Match the words using minimum edit distance.
3.  Count the substitutions, deletions, and insertions.
4.  Divide the total number of errors by the number of words in the
    reference.

**Advantages:** - Easy to understand and calculate. - Widely used for
evaluating speech recognition systems. - Shows the different kinds of
word errors.

**Limitations:** - Does not compare the meaning of sentences. - Even a
small word change can count as an error although the meaning stays the
same. - The result depends on consistent text normalization and
tokenization. - WER can be higher than 100% if there are many inserted
words.

**Important:** A lower WER means better transcription performance. A WER
of 0 means there are no word-level errors.

------------------------------------------------------------------------

## 9. Character Error Rate (CER)

### Definition

Character Error Rate (CER) works in a similar way to WER, but it
compares individual characters instead of complete words.

It is often used in OCR (Optical Character Recognition), handwriting
recognition, and speech recognition, especially when checking text at
the character level is useful.

### Three Types of Errors

-   **Substitution (S):** A correct character is changed to another
    character.
-   **Deletion (D):** A character from the reference text is missing.
-   **Insertion (I):** An additional character appears in the predicted
    text.

### Formula

\[ CER = `\frac{S+D+I}{N}`{=tex} \]

Where: - (S) = Number of substituted characters. - (D) = Number of
deleted characters. - (I) = Number of inserted characters. - (N) = Total
number of characters in the reference text.

### Example

-   Reference: "CAT"
-   Candidate: "CUT"

There is one incorrect character because "A" is replaced with "U".

\[ CER = `\frac{1}{3}`{=tex} = 0.3333 \]

Therefore, the CER is approximately 33.33%.

### Evaluation Process

1.  Compare the reference text with the predicted text.
2.  Align the characters using minimum edit distance.
3.  Count the substitutions, deletions, and insertions.
4.  Divide the total character errors by the number of characters in the
    reference.

**Advantages:** - Useful for evaluating text character by character. -
Can detect small spelling and recognition mistakes. - Helpful for OCR
and languages that do not have clear spaces between words.

**Limitations:** - Does not evaluate the meaning of the text. - Even a
small spelling mistake can increase the error rate. - The result depends
on text normalization, including spaces, punctuation, and Unicode
handling.

**Important:** A lower CER means better performance. A CER of 0 means
the predicted text and reference text have no character-level
differences.

------------------------------------------------------------------------

## 10. Comparing Different LLM Evaluation Metrics

Each evaluation metric focuses on a different part of model performance.
Therefore, one metric alone cannot fully evaluate every type of LLM
output.

### Comparison Table

  -----------------------------------------------------------------------
  Metric            What It Measures  Common            Better Result
                                      Applications      
  ----------------- ----------------- ----------------- -----------------
  Exact Match (EM)  Whether the       QA, MCQ,          Higher
                    answer matches    mathematics       
                    exactly                             

  Accuracy          Overall number of Classification    Higher
                    correct                             
                    predictions                         

  Precision         How many positive Classification    Higher
                    predictions are                     
                    correct                             

  Recall            How many actual   Classification    Higher
                    positive cases                      
                    are identified                      

  F1-Score          Balance between   Classification    Higher
                    Precision and                       
                    Recall                              

  BLEU              Overlap of        Machine           Higher
                    n-grams           translation       

  ROUGE             Amount of         Text              Higher
                    reference         summarization     
                    information                         
                    included                            

  METEOR            Word matching and Machine           Higher
                    word order        translation       

  BERTScore         Similarity in     Text generation,  Higher
                    meaning           summarization     

  WER               Errors at the     Speech            Lower
                    word level        recognition       

  CER               Errors at the     OCR, speech       Lower
                    character level   recognition       
  -----------------------------------------------------------------------

### Key Differences

**1. Exact Matching Metrics** - EM checks whether the predicted answer
is exactly the same as the reference. - Accuracy calculates the overall
proportion of correct classification results. - Precision, Recall, and
F1-Score give more detail about classification performance.

**2. Text Overlap Metrics** - BLEU mainly focuses on matching n-grams
and precision. - ROUGE focuses on how much information from the
reference text is included. - METEOR checks word matches, word stems,
synonyms, and word order.

**3. Semantic Similarity Metrics** - BERTScore uses contextual
embeddings to compare the meanings of words. - It can identify some
expressions with similar meanings even when they use different words.

**4. Error Rate Metrics** - WER counts errors based on complete words. -
CER counts errors based on individual characters. - Both use edit
distance and are commonly applied to transcription evaluation.

### Which Metric Should We Use?

  -----------------------------------------------------------------------
  Task                                Suitable Metrics
  ----------------------------------- -----------------------------------
  Multiple-choice questions           Exact Match, Accuracy

  Mathematical question-answering     Exact Match

  Classification                      Accuracy, Precision, Recall,
                                      F1-Score

  Machine translation                 BLEU, METEOR, BERTScore

  Text summarization                  ROUGE, BERTScore

  Open-ended question-answering       Exact Match (when suitable),
                                      BERTScore, human evaluation

  Speech recognition                  WER, CER

  OCR                                 CER, WER
  -----------------------------------------------------------------------

### Final Understanding

-   **EM:** Checks whether the answer is exactly the same as the
    reference.
-   **Accuracy:** Measures how many predictions are correct overall.
-   **Precision:** Shows how many predicted positive cases are correct.
-   **Recall:** Shows how many actual positive cases the model can find.
-   **F1-Score:** Combines Precision and Recall into one score.
-   **BLEU:** Measures the overlap of word sequences between generated
    and reference text.
-   **ROUGE:** Checks how much information from the reference is
    included in the generated text.
-   **METEOR:** Evaluates word matching, similar word forms, and word
    order.
-   **BERTScore:** Compares the meaning of generated text with the
    reference.
-   **WER:** Measures the number of word-level errors.
-   **CER:** Measures the number of character-level errors.

**Conclusion:** We should choose an evaluation metric based on the task
we want to measure. A high score does not always mean that an LLM gives
correct, useful, or reliable answers. For open-ended answers, it is
better to combine automatic evaluation metrics with human evaluation and
factuality checking.
