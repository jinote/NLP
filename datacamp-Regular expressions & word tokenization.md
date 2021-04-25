## Introduction to regular expressions

what is NLP?

- Field of study focused on making sense of language
    - using statistics and computers
- The basics of NLP
    - Topic identification
    - Text classification
- NLP applications include:
    - Chatbots
    - Translation
    - Sentiment analysis
    - etc

What exactly are regular expressions?

- Strings with a special syntax - Find all web links in a doc
- Allow us to match patterns in other strings - Parse eamil addrss
- Applications of regular expressions - remove/replace unwanted characters

```python
import re

re.match('abc', 'abcdef')

word_regex = '\w+'
re.match(word_regex, 'hi there!')
```

[Common regex patterns](https://www.notion.so/f0331c66cd344661b1eceedb9675bb98)

Python's module

```python
re # module
split # split a string on regex
findall # find all patterns in a string
search # search for a pattern
match # match an entire string or substring based on a pattern

# pattern first, and the string second
# may return an iterator, string, or match object

# for example
re.split('\s+', 'Split on spaces.')
```

## Introduction to tokenization

## Tokenization

모바일 결제 시스템에서 신용카드와 같은 개인 정보를 보호하기 위해 관련 정보를 토큰으로 변환하여 사용하는 방식. 금융 보안 분야에서 개인 정보를 보호하기위해 보호되어야 할 신용카드나 개인 정보를 토큰화하여 결제 시 원본 데이터 대신 토큰 데이터를 사용한다. 

What is tokenism 

- Turning a string or document into tokens (smaller chunks)
- One step in preparing a text for NLP
- Many different theories and rules
- You can create your own rules using regular expressions
- examples:
    - Breaking out words or sentences
    - Separating punctuation
    - Separating all hashtags in a tweet

Librareies

- nltk: natural language toolkit

```python
from nltk.tokenize import word_tokenize
word_tokenize("Hi there!")

# ["Hi", "there", "!"]
```

why tokenize?

- easier to map part of speech
- matching common words
- removing unwanted tokens
- "I don't like Sam's shoes."
- "I", "do", "n't", "like", "Sam", "s", "shoes", "."

Other nltk tokenizers

```python
sent_tokenize # tokenize a document # sent = sentences

regexp_tokenize # tokenize a string or document based on a regular expression pattern

TweetTokenizer # special class just for tweet tokenization, allowing you to separate hashtags, mentions and lots of exclamation points!
```

More regex practice

- Different between re.search() and re.match()

```python
import re 
re.match('abc', 'abcde')
# span = (0,3), match = 'abc'

re.search('abc', 'abcde')
# span = (0,3), match = 'abc'

re.match('cd', 'abcde')
re.search('cd', 'abcde')
# span = (2,4), match = 'cd'
```

## Advanced tokenization with regex

Regex groups using or "|"

- OR is represented using |
- You can define a group using ()
- You can define explicit character ranges using []

```python
import re
match_digits_and_words = ('(\d+|\w+)')
re.findall(match_digits_and_words, 'He has 11 cats.')

# ['He', 'has', '11', 'cats']
```

[Regex ranges and groups](https://www.notion.so/0af99964c01b43ed99700568965befda)

## Character range with 're.match()'

```python
import re
my_str = 'match lowercase spaces nums like 12, but no commas'

re.match('[a-z0-9 ]+', my_str)

# span = (0,42) match = 'match lowercase spaces nums like 12'
```

## Charting word length with nltk

```python
from matplotlib import pyplot as plt
from nltk.tokenize import word_tokenize
words = word_tokenize("This is a pretty cool tool!")
word_lengths = [len(w) for w in words]
plt.hist(word_lengths)

```
