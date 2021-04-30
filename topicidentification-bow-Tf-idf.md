## Word counts with bag-of-words

What is a bag of words in NLP? 

- Bag of words is a NLP technique of text modeling. In technical terms, we can say that it is a method of feature extraction of text data. This approach is a simple and flexible way of extracting features from documents.

- Basic method for finding topics in a text
- Need to first create tokens using tokenization
- .... and then count up all the tokens
- The more frequent a word, the more important it might be
- Can be a great way to determine the significant words in a text

For example:

- Text: "The cat is in the box. The cat likes the box. The box is over the cat."
- Bag of words (stripped punctuation):
    - "The": 3, "box": 3
    - "cat": 3, "the": 3
    - "is": 2
    - "in": 1, "likes": 1, "over": 1

```python
from nltk.tokenize import word_tokenize
from collections import Counter
Counter(word_tokenize("""The cat is in the box. The cat likes the box. The box is over the cat.""")
 
# Counter({'.':3, 'The':3, 'box':3, 'cat':3, 'in':1, 'the':3}counter
```

```python
Counter.most_common(2)

# [('The', 3), ('box', 3)]
```

Building a Counter with bag-of-words using a Wikipeida article 

```python
from nltk.tokenize import word_tokenize
from collections import Counter

# tokenize the article: tokens
tokens = word_tokenize(article)

# convert the tokens into lowercase: lower_tokens
lower_tokens = [t.lower() for t in tokens]

# create a Counter with the lowercase tokens: bow_simple
bow_simple = Counter(lower_tokens)

# Print the 10 most common tokens
print(bow_simple.most_common(10))
```

## Simple text preprocessing

- Helps make for better input data
    - When performing machine learning or other statistical methods
- Examples:
    - Tokenization to create a bag of words
    - Lowercasing word
- Lemmatization/Stemming
    - Shorten words to their root stems
- Removing stop words, punctuation, or unwanted tokens
- Good to experiment with different

what is stop words?

- In computing, stop words are words that are filtered out before or after the nlp data(text) are processed. While "stop words" refers to the most common words in a language, all nlp tools don't use a single universal list of stop words.
- **stop words** = a, the, is, are

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/255b8ed1-fd1e-43b3-8560-4ac63b9b6113/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/255b8ed1-fd1e-43b3-8560-4ac63b9b6113/Untitled.png)

## Preprocessing example

- input text: cats, dogs and birds are common pets. So are fish
- - Output tokens: cat, dog, bird, common, pet, fish

## Text preprocessing with Python

```python
from ntlk.corpus import stopwords
text = """The cat is in the box. The cat likes the box. The box is over the cat."""

tokens = [w for w in word_tokenize(text.lower()) if w.isalpha()]

no_stops = [t for t in tokens if t not in stopwords.words('english')]

Counter(no_stops).most_common(2)

# [('cat',3), ('box',3)]
```

**Text preprocessing example**

Apply the techniques you've learned to help clean up text for better NLP results. 

- Need to remove stop words / non-alphabetic char
- Lemmatize (분류 정리하다) and perform a new bag-of-words on your cleaned text

```python
from nltk.stem import WrodNetLemmatizer
alpha_only = [t for t in lower_tokens if t.isalpha()]
no_stops = [t for t in alpha_only if t not in english_stops

wordnet_lemmatizer = WordNetLemmatizer()
lemmatized = [wordnet_lemmatizer.lemmatize(t) for t in no_stops]
bow = Counter(lemmatized)
print(bow.most_common(10))
```

## Introduction to gensim

**What is gensim?**

Gensim is an open source Python library for natural language processing, with a focus on topic modeling. It is billed as: topic modelling for humans. 

- Popular open-source NLP library
- Uses top academic models to perform complex tasks
    - Building document or word vectors
    - Performing topic identification and doc comparisom

Word vectors

- multi-dimensional mathematical representations of words created using deep learning methods. They give us insight into relationships between words in a corpus

```python
from gensim.corpora.dictionary import Dictionary
from nltk.tokenize import word_tokenize
my_documents = ['The movie was about a spaceship and aliens.',
'I really liked the movie!',
'Awesome action scenes, but boring characters.',
'The movie was awful! I hate alien films.',
'Space is cool! I liked the movie.',
'More space films, pleae!']
```

```python
tokenized_docs = [word_tokenize(doc.lower()) for doc in my_documents]
dictionary = Dictionary(tokenized_docs)
dictionary.token2id

# answer
'''{'!':11,
',':17,
'.':7,
'a':2,.....}'''

```

## Creating a genism corpus

```python
corpus = [dictionary.doc2bow(doc) for doc in tokenized_docs]
corpus

# [[(0,1), (1,1), (2,1).....]]
```

- Genism models can be easily saved, updated and reused
- Our dictionary can also be updated
- This more advanced and feature rich bag-of-words can be used in future exercises

what is corpus?

- A collection of linguistic data, either compiled as written texts or as a transcription of recorded speech.

what is dictionary.token2id?

- dictionary.token2id 속성을 이용하여 사전에서 생성된 각각의 단어(token)들의 id 를 알 수 있다.

what is dictionary.doc2bow?

- Dictionary 클래스에서 doc2bow 메소드를 이용해서 문서데이터를 수치화함
- bow is short for bow-of-words
- 여기서, 문서를 단어 id 와 빈도수로 수치화하는 것

## Tf-idf with genism

what is tf-idf?

- Term frequency - inverse document frequency
- Allows you to determine the most important words in each document
- Each corpus may have shared words beyond just stopwords
- These words should be down-weighted in importance
- Example from astronomy "Sky"
- Ensures most common words don't show up as key words
- Keeps document specific frequent words weighted high

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/93970270-242e-4182-813e-824b3804db1a/Screen_Shot_2021-04-30_at_6.12.05_PM.jpg](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/93970270-242e-4182-813e-824b3804db1a/Screen_Shot_2021-04-30_at_6.12.05_PM.jpg)

```python
from genism.models.tfidfmodel import TfidModel
tfidf = TfidModel(corpus)
tfidfcorpus[1]]

# [(0, 0.174629),
#	(1, 0.1746),
#	(9, 0.2985),
#	(10, 0.7716), - 10이 0.77로 수치가 가장 큼
#...]
```
