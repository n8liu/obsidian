# Lecture 1 (1/20)
NPL is interdisciplinary → used in many majors

Turing Test → human vs computer can tell difference who wrote it

LLM → mainly performs well on trained data or sentiment analysis![[Screenshot 2026-01-28 at 3.08.49 PM.png]]![[Screenshot 2026-01-28 at 3.11.12 PM.png]]


# Lecture 2 (1/22)
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

# Lecture 3 (1/27)
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

## QUIZ 1 (1/29)
- 

# Lecture 4 (1/29)
Classification → x is all text and y is what to find
- supervised learning → given x find y
Text Categorization → 

| task                 | x      | y                                |
| -------------------- | ------ | -------------------------------- |
| language ID          | text   | [english, mandarin, greek, …]    |
| spam classification  | emails | [spam, no spam]                  |
| genre classification | novel  | [detective, romance, gothic, …]  |
| sentiment analysis   | text   | [positive, negative, neutral, …] |
|                      |        |                                  |
Sentiment Analysis → is the entire text positive or negative or both with respect to the implicit target?

Bago of Words →

Binary Logistic Regression →![[Screenshot 2026-01-29 at 4.12.13 PM.png]]

Conditional Likelihood →

Stochastic Gradient Descent → ![[Screenshot 2026-01-29 at 4.24.27 PM.png]]

L2 Regularization →![[Screenshot 2026-01-29 at 4.25.19 PM.png]]

L1 Regularization →![[Screenshot 2026-01-29 at 4.25.28 PM.png]]
- encourages coefficients to be exactly 0.

Multiclass Logistic Regression →

Accuracy → 

Precision →

Recall →

F score →![[Screenshot 2026-01-29 at 4.38.30 PM.png]]