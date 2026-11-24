# Pre-Lecture Lab: Text Mining and Unstructured Data

**Format:** Jupyter Notebook (Python 3)

---

## Why this lab?

The lecture follows an NLP pipeline:

```
Collecting Data → Preparing / Cleaning → Segmentation → Annotation → Language Models → Analysis / Prediction
```

This lab gives you hands-on experience of each stage **before** you see it in class, so the lecture builds on problems you have already run into. Don't worry if some results look strange or "wrong". Many tasks are designed to show where simple methods fail. Write down your observations: we will discuss them in the lecture.

### Learning outcomes

By the end of this lab you should be able to:

1. Load and explore a text corpus, and think critically about where it came from.
2. Explain Unicode code points, UTF-8 encoding, and *mojibake*, and fix broken text.
3. Use regular expressions to find and clean non-standard language (hashtags, mentions, URLs, emoticons).
4. Compare different tokenisation methods and explain why they give different results.
5. Recognise multiword expressions (MWEs) and find collocations in a corpus.
6. Explore lexical ambiguity with WordNet and try a simple Word Sense Disambiguation (WSD) algorithm.
7. Run Named Entity Recognition (NER) and read BIO tags.

### Deliverable

Submit your notebook with all code cells run, plus short written answers (2–4 sentences) to every question marked **✍️**. Bring your answers to the lecture.

---

## Task 0 – Setup (10 min)

Install the libraries and download the data:

```python
!pip install nltk ftfy spacy
!python -m spacy download en_core_web_sm
```

```python
import nltk
for pkg in ["punkt", "punkt_tab", "gutenberg", "wordnet", "omw-1.4", "stopwords"]:
    nltk.download(pkg)
```

```python
import re
import unicodedata
from collections import Counter

import nltk
import ftfy
import spacy
from nltk.corpus import gutenberg, stopwords, wordnet as wn
from nltk.tokenize import word_tokenize, TweetTokenizer, MWETokenizer
from nltk.collocations import BigramCollocationFinder, BigramAssocMeasures
from nltk.wsd import lesk
```

> 💡 If you are using Google Colab, everything above works as is. On your own machine, use a virtual environment.

---

## Part 1 – Corpus Data (20 min)

A **corpus** is a structured collection of texts used for linguistic or computational analysis. NLTK includes a small sample from **Project Gutenberg**, which is an example of a *data dump* source.

### Task 1.1 – Explore a corpus

```python
print(gutenberg.fileids())

raw = gutenberg.raw("austen-emma.txt")
print(len(raw))
print(raw[:500])
```

**TODO:**
1. Print the number of **characters**, **words** (`gutenberg.words(...)`) and **sentences** (`gutenberg.sents(...)`) for *every* file in the corpus. Show the results as a table (a `pandas.DataFrame` is fine).
2. Which text is the longest? Which has the longest average sentence length?

### Task 1.2 – Thinking about sources ✍️

Data can come from four main sources: **pre-prepared datasets, APIs, data dumps,** and **web scraping**.

**✍️ Q1.** For each source, give *one* real example you could use for a text-mining project about Vietnamese university students' opinions. For each one, give one advantage and one disadvantage.

**✍️ Q2.** The NLTK Gutenberg sample contains 18 texts. What is it *representative* of? Could you use it to make claims about "English" in general? Why or why not? (Look at the authors, dates, and genres.)

**✍️ Q3 (Ethics).** Suppose you scraped posts from a public Facebook group where people discuss their mental health. List **three** ethical problems this raises, even though the posts are "public". Would your answer change if some users were under 18?

**✍️ Q4.** A classmate says: *"I'll just use ChatGPT to generate 10,000 student reviews, then train my model on them."* Give two reasons why this is a problem for building a corpus.

---

## Part 2 – Cleaning and Character Encoding (20 min)

### Task 2.1 – Unicode code points

Every character has a unique **code point** in Unicode. UTF-8 is a way of storing those code points as bytes.

```python
s = "Xin chào"
for ch in s:
    print(ch, f"U+{ord(ch):04X}")
```

**TODO:**
1. Compare `len("chào")` with `len("chào".encode("utf-8"))`. Why are they different?
2. Print the code points and UTF-8 bytes for `"Việt Nam"` and for an emoji of your choice, e.g. `"😀"`. How many bytes does the emoji need?

### Task 2.2 – Mojibake and how to fix it

*Mojibake* happens when text encoded as UTF-8 is decoded with the wrong encoding.

```python
original = "cảm ơn"
broken = original.encode("utf-8").decode("latin-1")
print(broken)
print(ftfy.fix_text(broken))
```

**TODO:**
1. Run `ftfy.fix_text("cáº£m Æ¡n")`. What do you get?
2. Create your own mojibake from a Vietnamese sentence of your choice, then fix it with `ftfy`.

### Task 2.3 – Same text, different code points

Vietnamese characters can be stored in more than one way:

```python
a = "cà"
b = unicodedata.normalize("NFD", a)
print(a, b, a == b, len(a), len(b))
```

**✍️ Q5.** The two strings look identical but `a == b` is `False`. Explain why. What problem could this cause when you count word frequencies in a Vietnamese corpus? How would you fix it?

### Task 2.4 – Cleaning noisy social-media text

```python
post = ("OMG @linh_99 the new café menu is soooo good :-) thnx 4 the tip!! "
        "#foodie #Hanoi http://bit.ly/abc123 email me: linh@vinuni.edu.vn")
```

**TODO:** Write a regular expression for each item below and use `re.findall` to extract it from `post`:

| Item       | Expected result                  |
|------------|----------------------------------|
| Mentions   | `['@linh_99']`                   |
| Hashtags   | `['#foodie', '#Hanoi']`          |
| URLs       | `['http://bit.ly/abc123']`       |
| Emails     | `['linh@vinuni.edu.vn']`         |
| Emoticons  | `[':-)']`                        |

> ⚠️ **Check carefully:** does your mention pattern also match part of the email address? If so, fix it.

**TODO (continued):**
1. Write a function `reduce_elongation(text)` that shortens any character repeated 3+ times to 2 (`"soooo"` → `"soo"`). *Hint:* `re.sub(r"(\w)\1{2,}", r"\1\1", text)`.
2. Build a small dictionary to normalise abbreviations (`"thnx" → "thanks"`, `"4" → "for"`, `"omg" → "oh my god"`) and apply it.

**✍️ Q6.** Is it always a good idea to "clean" text like this? Give an example of a research question where removing emoticons, elongations, or spelling variation would **destroy** useful information.

---

## Part 3 – Tokenisation (20 min)

**Tokenisation** splits text into units (tokens) such as words, punctuation, and numbers. It sounds trivial. Let's test that.

```python
text = ("Usually lemon and sugar or icecream and chocolate sauce or rolled "
        "with jam/maple syrup.Mmmm.. can't wait!!")
```

### Task 3.1 – Predict first!

**✍️ Q7.** *Before running any code*, write down how many tokens **you** think this sentence contains. Which parts were hard to decide on?

### Task 3.2 – Compare four tokenisers

```python
methods = {
    "whitespace": text.split(" "),
    "regex":      re.findall(r"[a-zA-Z]+", text),
    "nltk":       word_tokenize(text),
    "tweet":      TweetTokenizer().tokenize(text),
}
```

**TODO:**
1. Print the number of tokens and the full token list for each method.
2. Make a table showing how each method handles `jam/maple`, `syrup.Mmmm..`, `can't`, and `wait!!`.
3. Which method do you think is "best" for this sentence? Justify your answer.

### Task 3.3 – Harder cases

Tokenise these with `word_tokenize` and look at the output carefully:

```python
examples = [
    "I'll use a state-of-the-art model in the U.S. for $3.50.",
    "Hà Nội là thủ đô của Việt Nam.",
    "Email me at linh@vinuni.edu.vn or tweet #DATA2010 :-)",
]
```

**✍️ Q8.** In Vietnamese, *Hà Nội*, *thủ đô* and *Việt Nam* are each a single word made of two syllables. What did the tokeniser do? Why is tokenisation harder for Vietnamese than for English, even though both use spaces?

---

## Part 4 – Multiword Expressions and Collocations (15 min)

A **multiword expression (MWE)** is a sequence of words that behaves as a single unit, e.g. *kick the bucket*, *give up*, *New York City*.

### Task 4.1 – Joining MWEs

```python
mwe = MWETokenizer([("give", "up"), ("New", "York", "City"), ("kick", "the", "bucket")],
                   separator="_")
print(mwe.tokenize(word_tokenize("He didn't give up until he moved to New York City.")))
```

**TODO:** Try `"He gave up"` and `"She kicked the bucket"`. Does the MWE tokeniser still find them? What does this tell you about the **variability** of MWEs?

### Task 4.2 – Finding collocations automatically

```python
words = [w.lower() for w in gutenberg.words("austen-emma.txt") if w.isalpha()]
finder = BigramCollocationFinder.from_words(words)
finder.apply_freq_filter(5)
measures = BigramAssocMeasures()

print(finder.nbest(measures.raw_freq, 15))
print(finder.nbest(measures.pmi, 15))
```

**✍️ Q9.** Compare the two lists. Which looks more like "real" MWEs, raw frequency or PMI? Why do you think raw frequency gives pairs like *of the*?

**TODO:** Change `apply_freq_filter(5)` to `apply_freq_filter(1)` and rerun PMI. What goes wrong?

---

## Part 5 – Corpus Linguistics Basics (10 min)

### Task 5.1 – Frequency list

**TODO:** Using `words` from Task 4.2, build the 20 most frequent words **with and without** stop words (`stopwords.words("english")`). What do the top content words tell you about the novel?

### Task 5.2 – Concordance

A **concordance** shows every occurrence of a word with its surrounding context (KWIC: Key Word In Context).

```python
emma = nltk.Text(gutenberg.words("austen-emma.txt"))
emma.concordance("spring", lines=14)
```

**✍️ Q10.** Read the concordance lines. Does *spring* always have the same meaning in *Emma*? This leads us into Part 6.

---

## Part 6 – Lexical Ambiguity and Word Sense Disambiguation (15 min)

### Task 6.1 – How many senses?

**✍️ Q11.** *Before running code:* how many different meanings of the word **spring** can you think of? Write them down.

```python
senses = wn.synsets("spring")
print(len(senses))
for s in senses:
    print(s.name(), s.pos(), "-", s.definition())
```

**TODO:** How many senses does WordNet list? How many are nouns and how many are verbs? Did you think of all of them?

### Task 6.2 – Simple WSD with the Lesk algorithm

The **Lesk algorithm** chooses the sense whose dictionary definition overlaps most with the words around the target word. This is a *knowledge-based* approach.

```python
sentences = [
    "I love walking in the park in spring when the flowers bloom",
    "The mattress has a broken spring inside",
    "We drank fresh water from the mountain spring",
]
for sent in sentences:
    sense = lesk(word_tokenize(sent), "spring")
    print(sent, "->", sense, "|", sense.definition())
```

**TODO:**
1. Check each answer. Is it correct?
2. For any wrong answer, try passing `pos="n"` to `lesk(...)`. Does that help?
3. Write two sentences of your own for other senses of *spring* (e.g. *spring to mind*, *spring onion*) and test them.

**✍️ Q12.** Why might a simple overlap method like Lesk fail? The lecture mentions that "most frequent sense" is a very strong baseline. What does this mean?

---

## Part 7 – Named Entity Recognition (15 min)

**NER** finds spans of text that refer to named things (people, places, organisations, dates…) and labels their type.

### Task 7.1 – Run NER

```python
nlp = spacy.load("en_core_web_sm")
doc = nlp("Barack Obama visited Paris in 2015 for a UNESCO event")

for ent in doc.ents:
    print(ent.text, ent.label_, spacy.explain(ent.label_))
```

### Task 7.2 – BIO tags (NER as sequence labelling)

NER is often treated as labelling **each token** with B- (begin), I- (inside), or O (outside):

```python
for tok in doc:
    tag = f"{tok.ent_iob_}-{tok.ent_type_}" if tok.ent_type_ else "O"
    print(f"{tok.text:10} {tag}")
```

**TODO:** Write the BIO tags *by hand* for this sentence first, then check them against spaCy's output:

> *"Dr Nguyen Van An joined VinUniversity in Hanoi on 1 September 2025."*

### Task 7.3 – Breaking NER

**TODO:** Run NER on each of the following and record what changes:

1. The Obama sentence written all in **lowercase**.
2. A noisy tweet: `"omg just saw @taylorswift13 at tan son nhat airport!!! #hcmc"`
3. A sentence of your own with Vietnamese names and places.

**✍️ Q13.** Why does the model perform worse on lowercase or social-media text? The model was trained mostly on edited English news and web text. How does this connect to **representativeness** in Part 1?

**✍️ Q14.** Name one domain (e.g. medicine, law, finance) where the standard labels PERSON/ORG/GPE/DATE would **not** be enough. What entity types would you add?

---

## Challenge Task (optional) ⭐

Build a mini pipeline function:

```python
def mini_pipeline(text):
    """
    1. Fix encoding with ftfy
    2. Normalise Unicode to NFC
    3. Replace URLs, emails, mentions with placeholders (<URL>, <EMAIL>, <USER>)
    4. Tokenise with TweetTokenizer
    5. Run spaCy NER on the cleaned text
    Return a dict with the tokens and entities.
    """
    ...
```

Test it on at least three messy texts (with mojibake, hashtags, emoticons, and named entities). Briefly discuss: does cleaning **help or hurt** NER?

---

## Before the lecture: checklist

- [ ] All code cells run without errors
- [ ] Written answers to Q1–Q14
- [ ] Your token-count prediction from Q7 (we will compare it in class!)
- [ ] Your list of *spring* senses from Q11
- [ ] *(Recommended reading)* Eysenbach & Till (2001), *Ethical issues in qualitative research on internet communities*, BMJ: <https://doi.org/10.1136/bmj.323.7321.1103>

## Further resources

- NLTK Book, Chapters 1–2: <https://www.nltk.org/book/>
- Jurafsky & Martin, *Speech and Language Processing* (3rd ed. draft), Chapter 2: <https://web.stanford.edu/~jurafsky/slp3/>
- Python Unicode HOWTO: <https://docs.python.org/3/howto/unicode.html>
- ftfy documentation: <https://ftfy.readthedocs.io/>
- spaCy NER guide: <https://spacy.io/usage/linguistic-features#named-entities>