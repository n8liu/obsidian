# Lecture 1 - Intro (1/20)
NPL is interdisciplinary → used in many majors

Turing Test → human vs computer can tell difference who wrote it

LLM → mainly performs well on trained data or sentiment analysis![[Screenshot 2026-01-28 at 3.08.49 PM.png]]![[Screenshot 2026-01-28 at 3.11.12 PM.png]]


# Lecture 2 - Word (1/22)
Tokenization → break down sentences or words into basic units

Subtokenization → breaking words into smaller units (prefixes, suffixes, etc)
Word Types: number of **distinct words** in a vocabulary
Word Instances: total number of running words in a text (in other words **tokens**)
Byte-Pair Encoding: algorithm that breaks down text into tokens
- letter statistics → common letters pairings to predict the next letter
- tokenized → add most frequent pairs (including spaces)
Morphemes → the minimal meaning-bearing units in a language
Types → unique instances
Tokens → breakdown of sentences into word breaks
Chi-Squared Test → compare corpus A vs corpus B
Herdan’s/Heap’s Law → relationship between vocabulary size grows indefinitely with corpus size

## Reading Unit 2

1. What is the difference between word types and word instances? You should be able to correctly count the number of word types and instances in a passage of text.
	- word types are total distinct or unique words and word instances are tokens

2. What are some examples of how defining what counts as a “word” is difficult, even in English? What makes tokenization in languages like Chinese and Japanese difficult?
	- words in english are difficult mainly due to words that are multiple words like “New York”, in other languages their is usually no breaks in sentences like spaces which incurs lots of ambiguity

3. What is a function word?
	- words like “the”, “a”, “to”

4. What is a subword, and how is it different from a "word"?
	- a unit smaller than word → in subword tokenization which breaks down words into smaller words if in the dataset but if in test set would break the unknown word into known words

5. You should be able to use your recollection of the BPE algorithm to generate a BPE vocabulary given an input corpus (see algorithm in figure 2.6, along with discussion around it).
	- BPE → merges frequent pairs by merging, merge frequent pairs then update corpus with new pairs

6. Regular expressions: you should be able to use regular expressions to match a pattern in an input text, including character disjunctions, optionality, wildcards and capturing groups.
	- [abc] ← stands for must match one character
	- ? ← one or none
	- + one or many
	- * ← none or many

7. How are regular expressions relevant to tokenization?
	- used to split text by punctuation or whitespace or contractions apart. mainly used for cleaning, splitting, and standardizing text

# Lecture 3 - Lexical Semantics (1/27)
Cosine Similarity → frequency correlation between two vector words where 1 is upper bound (high correlation) and 0 is lower bound (low correlation)
	- equation:![[Screenshot 2026-01-29 at 10.40.47 AM.png]]
TF-IDF (Term Frequency-Inverse Document Frequency)→ the row count divide by total row count times log, if every row contains at least one count of the word
- IDF Score equation: every row count divide by total rows times log, if every row contains the then log(5/5) 
Point Mutual Information → how two variables rely on one another, how word x relates/would have word y nearby
Positive PMI → log(0) is negative infinite, but we only want minimum 0 so we use PPMI
- equation:
	- PMI (w = sword, c = stab) = log(P(w = sword, c = stab)/P(w = sword) * P(c = stab)) → log((8/785) / (202/785 * 21/785))
Word2Vec → generate a probability that another word will be observed in context (window area)
Dot Product: x^Ty or sum xi * yi 
Sigmoid Function: 1/(1+exp(-x))
Dimensionality Reduction: negative of uncommon words and positive common words, basically changing weights
SemAxis: one axis that are two opposite ends, then match words based on the axis
- poor ←→ rich axis and a bunch of words connected to the axis
## Reading Unit 5
Distributional Hypothesis → words in similar environments tend to have similar meanings
Lemma → citation form of a word (like sing) and Wordforms → are different forms (like sung or sang)
Synonyms → different forms provide different meanings, defined as not True Synonyms
Similarity → related by association like cat and dog
Connotation → words that carry meaning on emotion of sentiment
Embedding is relating similar words in similar context to one another
Dense Vectors are generalize to be better because fewer parameters to learn and capture synonyms better than sparse vectors

1. Given two vectors, how do we calculate the cosine similarity between them? What are the upper and lower bounds of cosine similarity? Geometrically, what does this quantity represent?
	- equation which is the sum of x and y divide by square root of the sum of x squared times the square root of the sum of y squared. with an upper bound of one and a lower bund of 0. upper bound of one is more correlated and a lower bound of 0 meaning no correlation

2. In your own words, describe the distributional hypothesis as a way of thinking about word meanings
	- word meanings are defined by words around it or sentences it is involved in share similar meaning

3. What is a dense vs sparse vector? Give an example of a dense and sparse vector in the context of the different methods of representing word meanings. 
	- sparse vector: very long dimensionality equal to the vocabulary, but being sparse because most of the values in the vector are zero. better when dealing with more diverse vocabulary, more inefficient and expensive
		- [0, … , 0, 442, 8, 2, …, 0, 0] ← where the entire vector is zero but words in the window are values
		- TF-IDF (Term Frequency-Inverse Document Frequency)→ the row count divide by total row count times log, if every row contains at least one count of the word
	- dense vector (or embedding vector): shorter dimensionality and contain mostly real-valued numbers
		- Word2Vec → vector area is smaller and many values do not correspond to the word by being negative
 
4. Why is it useful to represent words as dense vectors in a latent semantic space? Describe some applications of these vectors (word embeddings).
	- dense vectors outperforms sparse vectors in latent semantic space. dense vectors have fewer weights and the smaller vector/parameter space helps reduce overfitting. applications include: 
		- sentiment analysis: good at adding unknown (training data) words to the embedding space
		- analogical reasoning: vector arithmetic → king - man + woman → queen
		- historical semantics: word association over history
		- information retrieval: word similarities that do not share the same keywords

5. What is self-supervised learning, and why is it useful? How is word2vec an example of self-supervised learning?
	- representing learning where the training data generates its own supervision signal, where humans are needed to label. Word2Vec is a prime example because it utilized running text documents to train a classifier based on neighboring context words as positive neighbors and unconnected words as negative neighbors, labeling its own raw data

6. You should be able to step through the word2vec (skip-gram) algorithm (sections 5.5.1 and 5.5.2) to explain the prediction task, how the negative sampling works, and how the loss is calculated and the weights are updated. 
	- Prediction Task: compute probability that c is a real context word for target word w (P(+ | w, c)), which is calculated using the sigmoid function.
	- Negative Sampling: using both positive and negative examples so that positive examples would not have only positive examples. negative examples were labeled as “noise words”, chosen on weighted frequency to give rare words slighty higher probability.
	- Calculated Loss: ![[Screenshot 2026-01-29 at 12.37.19 PM.png]]
	- Updating Weights: Stochastic Gradient Descent (SGD) used to minimize loss
		1. moves the target embedding w closer to context embedding c_pos
		2. moves the target embedding w further away from the noise embedding c_neg
		3. updates the context embedding (c_pos and c_neg) correspondingly

7. How might “bias” be encoded in word embeddings? How can we measure or represent this bias?
	- based on training text and where sources come from, the vector represent based on trained text. 
	- analogy tests: father is to doctor as mother is to X, biased in gender
	- cosine similarity: similarity between two vectors between 1 and 0
	- historical analysis: training embedding on text from different decades, how bias shifts overtime

8. How are word embeddings evaluated for quality?
	- Extrinsic Evaluation: using vectors and adding vectors improves or worsens performance of a task
	- Intrinsic Evaluation: the test the quality of the vectors directly using specific datasets like WordSim-353 and SimLex-999:
		- similarity correlation using cosine similarity
		- analogy tasks: a is to b as c is to d
		- contextual similarity: using SCWS or WiC for similarity judgement

## QUIZ 1
- 1/27 Reading + Lecture

# Lecture 4  - Classification (1/29)
Classification → x is all text and y is what to find
- supervised learning → given training data of x find y pairs by learning ĥ(x)
- categorical, enumerable (countable) categories
Text Categorization

| task                 | x      | y                                |
| -------------------- | ------ | -------------------------------- |
| language ID          | text   | [english, mandarin, greek, …]    |
| spam classification  | emails | [spam, no spam]                  |
| genre classification | novel  | [detective, romance, gothic, …]  |
| sentiment analysis   | text   | [positive, negative, neutral, …] |
|                      |        |                                  |
Sentiment Analysis → is the entire text positive or negative or neutral with respect to the implicit target?
- the use of positive/negative tone
- Sentiment Dictionaries → choice of words and comparing positive vs negative
- sentiment analysis is hard because many times it requires deep world + contextual knowledge
ĥ(x) → classification function
- formal structure of learning; logistic regression or convolutional neural network
- the representation of data

Bag of Words → unordered frequency count of words

Binary Logistic Regression →![[Screenshot 2026-01-29 at 4.12.13 PM.png]]

Conditional Likelihood → dot product → exp → binary logistic regression (sigmoid) → we want the probability ot be high
- gradient ascent → maximize conditional log likelihood
- gradient descent → minimize conditional log likelihood
![[Screenshot 2026-02-05 at 11.43.50 AM.png]]
![[Screenshot 2026-02-05 at 11.47.45 AM.png]]

Gradient Descent → derivative of the sum of log 0 and log 1 of binary logistic regression![[Screenshot 2026-02-05 at 11.49.59 AM.png]]

Batch Gradient Descent → updates every training point for every beta update, slower
Stochastic Gradient Descent → updates data points AFTER beta
![[Screenshot 2026-01-29 at 4.24.27 PM.png]]
![[Screenshot 2026-02-05 at 11.49.59 AM.png]]

L2 Regularization → shrinks all weights to small values
![[Screenshot 2026-01-29 at 4.25.19 PM.png]]

L1 Regularization → penalize large weights to exactly zero
![[Screenshot 2026-01-29 at 4.25.28 PM.png]]
- encourages coefficients to be exactly 0.

Multiclass Logistic Regression →
![[Screenshot 2026-02-05 at 12.50.54 PM.png]]
Confusion Matrix → 
![[Screenshot 2026-02-05 at 12.52.16 PM.png]]
Evaluation → A critical part of development new algorithms and methods and demonstrating that they work

Accuracy → diagonal of confusion matrix divide by number of N

Precision → sum of true divide by sum of total predicted. ex → 100/(100 + 30) is positive precision

Recall → sum fo true divide by sum of total true. ex → 100 / (100 + 2 + 15) is true positive

F score →![[Screenshot 2026-01-29 at 4.38.30 PM.png]]

## Reading Unit 4
Classification → the process of labeling an input, primary example is sentiment analysis
Logistic Regression → supervised machine learning algorithm
A probabilistic classifier consists of four main components:
1. Feature representation: A vector representing the input.
2. Classification function: Computes the estimated class probability (e.g., Sigmoid or Softmax).
3. Objective function: A loss function to minimize error (e.g., Cross-Entropy).
4. Optimization algorithm: A method to update parameters (e.g., Stochastic Gradient Descent).

# Lecture 5 - Annotation (2/3)
Dogmatism → without a doubt true without evidence

Literary Time → how fast to read a passage

Annotation Pipeline → 
![[Screenshot 2026-02-05 at 1.22.17 PM.png|[100x100]]
Annotation Guidelines → 

Adjudication → Adjudication is the process of deciding on a single annotation for a piece of text, using information about the independent annotations.

Cohen’s Kappa →
![[Screenshot 2026-02-05 at 1.38.41 PM.png]]
- good for two categories
- observed agreement rate: diagonal
	- 88/100 = 0.88
- expected agreement rate: rows * column of one feature + rows * column of second feature
	- 15/100 * 11/100 + 85/100 * 89/100 = 0.773

Fleiss’ Kappa → 
- good for 3+ categories
- Observed Agreement (Pˉ): You calculate the proportion of agreeing pairs for each subject, then average them.
- Expected Agreement (Pˉe​): You calculate the proportion of total assignments to each category (across all subjects) and square them.
![[Screenshot 2026-02-05 at 2.21.54 PM.png]]
Krippendorf’s Alpha 
- measures disagreement
- Do​ (Observed Disagreement): The weighted average of disagreements. If two raters disagree on a Nominal value (A vs B), the weight is 1. If they disagree on Ordinal data (Low vs High), the weight is higher than (Low vs Medium).
- De​ (Expected Disagreement): The disagreement expected by chance, essentially treating all observations as if they were thrown into a bucket and randomly paired.![[Screenshot 2026-02-05 at 2.23.12 PM.png]]
## Reading Unit 6 ← different book
- 

# Lecture 6 - Neural Classification (2/5)
Neural Networks
- Non-linear interactions of input features
- Multiple layers to capture hierarchical structure
- Tremendous flexibility on design choices (exchange feature
engineering for model engineering)
• Articulate model structure and use the chain rule to derive parameter
updates.

Feedforward Neural Network
- input to output needs at least one hidden layer

Activation Functions
- sigmoid function![[Screenshot 2026-02-05 at 4.00.46 PM.png]]
- tanh function![[Screenshot 2026-02-05 at 4.03.46 PM.png]]
- ReLU function![[Screenshot 2026-02-05 at 4.03.54 PM.png]]

Back-propagation → Given training samples of <x,y> pairs, we can use stochastic gradient descent to find the values of W and V that minimize the loss.

Convolutional Networks
- 2D Convolution → reduction in 2D
- 1D Convolution → a signal processing and neural network operation that slides a filter (kernel) along one dimension of data—typically time, text, or sensor sequences—to extract local feature
- Indicator Vector →

## QUIZ 2
- 1/29 and 2/3 Reading + Lecture

## Reading Unit 6
- 