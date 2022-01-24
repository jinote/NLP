## Data Cleaning & Text Pre-processing in Python 
### Steps

1. Question
- what makes Ali Wong's comedy routine stand out?

2. Data Gathering + Cleaning
- Input: the question we have in our head, "how is Ali Wong different?"
- Output: clean, organized data in a standard format that looks like?

    - where are we going to get this data?
    - how much data should we get? which comedians? what time range?
    
**Data Gathering**
- this is where you are going to need to define the scope of your project based on your domain expertise
- here is how
    - stand up comedy specials from the past 5 years
    - at least a 7.5 rating with 2000+ votes on IMDB
    - If a comedian has multiple specials, I keep the one with the highest rating
    
**Data Cleaning with text data**
- Remove punctuation
- Lowercase letters
- Remove numbers
        - re: Python library for regular expressions basically a way to search for patterns
        
**Tokenized**<br>
<all, right, petunia, wish, me, luck, out, there, you, will, die, on, august>
- Tokenization: split text into smaller pieces aka a token. The most common token size is a word. It can also be a sentence
- Now that every word is its own token, you can filter out words that have very little meaning (these are called STOP WORDS - a, the, you, will, there, on, out)
- the representation of the text is called a bag of words model. It's a simple format that ignores order (right, petunia, wish, luck, die, august)
    
**Put into a matrix**
- the reason we need to put the data in a matrix is because we need to store this information for multiple documents
- Document-Term Matrix
    - each row is a different document (or a different transcript in our case)
    - each column is a different term (usually words, but can also be bi-grams like "thank you") 
    - the value are word counts
        - scikit-learn: Python library for ML
        - Count Vectorizer: sklearn way to make a DTM
