# 📝 NLP Basics - Complete Guide (Zero to Hero)

> Natural Language Processing (NLP) teaches machines to **understand, interpret, and generate human language**.

---

## 🔹 What is NLP?

### 🧠 Real-World Analogy

> 👉 Like teaching a **foreigner your language**:
> - First, they learn individual words (tokenization)
> - Then grammar rules (syntax)
> - Then meaning (semantics)
> - Then context and sarcasm (pragmatics)
>
> NLP does the same for computers.

### 🔸 NLP Applications

| Application | Example |
|-------------|---------|
| Spam detection | Gmail filtering spam emails |
| Sentiment analysis | "Is this review positive or negative?" |
| Chatbots | Customer support bots |
| Translation | Google Translate |
| Voice assistants | Siri, Alexa, Google Assistant |
| Autocomplete | Google search suggestions |
| Summarization | Summarizing long articles |
| Named Entity Recognition | Extracting names, dates, locations from text |

---

## 🔹 The NLP Pipeline

```
Raw Text
  ↓
1. Text Cleaning (lowercase, remove punctuation)
  ↓
2. Tokenization (split into words/sentences)
  ↓
3. Stop Word Removal (remove "the", "is", "a")
  ↓
4. Stemming / Lemmatization (reduce words to root form)
  ↓
5. Text Representation (convert text to numbers)
  ↓
6. Model Training (classification, sentiment, etc.)
  ↓
Prediction
```

---

# 🧹 TEXT PREPROCESSING

---

## 🔹 1. Text Cleaning

### 🔸 Lowercasing

```
"Hello WORLD Python" → "hello world python"
```

🧠 Why? So "Hello" and "hello" are treated as the **same word**.

### 🔸 Remove Punctuation

```
"Hello, World! How are you?" → "Hello World How are you"
```

### 🔸 Remove Numbers (if not needed)

```
"I have 3 cats and 2 dogs" → "I have cats and dogs"
```

### 🔸 Remove Special Characters

```
"Email: user@email.com #python" → "Email user email com python"
```

### 🔸 Remove Extra Whitespace

```
"Hello    World   Python" → "Hello World Python"
```

---

## 🔹 2. Tokenization (VERY IMPORTANT 🔥)

### 🧠 Analogy

> 👉 Like **cutting a sentence into individual word cards**. Each card is a "token."

### 🔸 Word Tokenization

```
"I love Python programming"
→ ["I", "love", "Python", "programming"]
```

### 🔸 Sentence Tokenization

```
"I love Python. It is easy. Let's learn it."
→ ["I love Python.", "It is easy.", "Let's learn it."]
```

### 🔸 Subword Tokenization (Modern NLP)

Used by BERT, GPT — splits rare words into smaller pieces:

```
"unhappiness" → ["un", "happiness"]
"playing" → ["play", "##ing"]
```

✔ Handles words the model has never seen before.

---

## 🔹 3. Stop Words Removal

### 🧠 Analogy

> 👉 Like removing **filler words** from a sentence. "The cat is on the mat" → "cat mat" — the meaning is preserved.

### 🔸 What are Stop Words?

Common words that carry **little meaning**: "the", "is", "a", "an", "in", "on", "at", "and", "or", "but", "it", "to", "of"

```
Before: "The cat is sitting on the mat"
After:  "cat sitting mat"
```

### 🔸 When NOT to Remove Stop Words

- Sentiment analysis: "not good" → removing "not" changes the meaning!
- Question answering: "what", "where", "how" are important
- Machine translation: every word matters

---

## 🔹 4. Stemming (INTERVIEW FAVORITE 🔥)

### 🧠 Analogy

> 👉 Like **chopping off the end of a word** to get the root. It's rough and sometimes produces non-real words.

### 🔸 What is Stemming?

Reducing words to their **root/base form** by removing suffixes.

```
"running"    → "run"
"runner"     → "run"
"runs"       → "run"
"played"     → "play"
"playing"    → "play"
"happiness"  → "happi"    ← not a real word!
"studies"    → "studi"    ← not a real word!
```

### 🔸 Types of Stemmers

| Stemmer | Speed | Accuracy | Notes |
|---------|:-----:|:--------:|-------|
| **Porter Stemmer** | ⚡ Fast | Medium | Most common, aggressive |
| **Snowball Stemmer** | ⚡ Fast | Better | Improved Porter |
| **Lancaster Stemmer** | ⚡ Fast | Aggressive | Very aggressive, shortest stems |

### 🔸 Pros & Cons

| Pros | Cons |
|------|------|
| Fast | Produces non-real words |
| Simple | Over-stems or under-stems |
| Reduces vocabulary size | Loses meaning sometimes |

---

## 🔹 5. Lemmatization (INTERVIEW FAVORITE 🔥)

### 🧠 Analogy

> 👉 Like looking up a word in a **dictionary** to find its proper base form. More intelligent than stemming.

### 🔸 What is Lemmatization?

Reducing words to their **dictionary form (lemma)** using vocabulary and grammar rules.

```
"running"    → "run"
"better"     → "good"     ← knows grammar!
"studies"    → "study"    ← real word!
"happiness"  → "happiness" or "happy"
"mice"       → "mouse"    ← knows irregular forms!
"went"       → "go"       ← knows verb conjugation!
```

### 🔸 Stemming vs Lemmatization (MUST KNOW 🔥)

| | Stemming | Lemmatization |
|---|---|---|
| Method | Chops off suffixes | Uses dictionary/grammar |
| Output | May not be a real word | Always a real word |
| Speed | ⚡ Faster | 🐢 Slower |
| Accuracy | Lower | Higher |
| "better" | "better" or "bet" | "good" |
| "studies" | "studi" | "study" |
| "mice" | "mice" | "mouse" |
| Use when | Speed matters, large data | Accuracy matters |

---

# 🔢 TEXT REPRESENTATION (Converting Text to Numbers)

> ML models can't read text. We must convert words into **numbers** (vectors).

---

## 🔹 6. Bag of Words (BoW)

### 🧠 Analogy

> 👉 Like dumping all words from a sentence into a **bag** and counting how many of each word you have. You lose the order but keep the frequency.

### 🔸 How It Works

```
Sentence 1: "I love Python"
Sentence 2: "I love Java"
Sentence 3: "Python is great"

Vocabulary: [I, love, Python, Java, is, great]

BoW Matrix:
              I  love  Python  Java  is  great
Sentence 1:   1    1      1     0    0     0
Sentence 2:   1    1      0     1    0     0
Sentence 3:   0    0      1     0    1     1
```

### 🔸 Pros & Cons

| Pros | Cons |
|------|------|
| Simple to understand | Loses word order |
| Easy to implement | Ignores context/meaning |
| Works for basic tasks | Vocabulary can be huge (sparse matrix) |

---

## 🔹 7. TF-IDF (Term Frequency - Inverse Document Frequency)

### 🧠 Analogy

> 👉 Like a **highlighter** that marks important words. Common words like "the" get low scores. Rare, meaningful words like "Python" get high scores.

### 🔸 Concept

- **TF (Term Frequency):** How often a word appears in a document
- **IDF (Inverse Document Frequency):** How rare a word is across ALL documents
- **TF-IDF = TF × IDF** — high score means the word is **frequent in this document** but **rare overall**

### 🔸 Example

```
Document 1: "Python is great"
Document 2: "Java is great"
Document 3: "Python Python Python"

"is" → appears in all docs → low IDF → low TF-IDF (not important)
"Python" → appears in some docs → higher IDF → higher TF-IDF (more important)
```

### 🔸 BoW vs TF-IDF

| | Bag of Words | TF-IDF |
|---|---|---|
| Measures | Word count | Word importance |
| Common words | High score | Low score (penalized) |
| Rare words | Low score | High score (rewarded) |
| Better for | Simple counting | Finding important words |

---

## 🔹 8. Word2Vec (VERY IMPORTANT 🔥)

### 🧠 Analogy

> 👉 Like placing words on a **map** where similar words are close together. "King" is near "Queen", "Dog" is near "Cat", "Paris" is near "France".

### 🔸 What is Word2Vec?

- Converts each word into a **dense vector** (list of numbers)
- Words with similar meanings have **similar vectors**
- Captures **semantic relationships**

### 🔸 The Famous Example

```
King - Man + Woman ≈ Queen
```

🧠 Word2Vec captures that "King is to Man as Queen is to Woman."

### 🔸 Two Architectures

| Architecture | How It Learns |
|-------------|--------------|
| **CBOW** (Continuous Bag of Words) | Predicts a word from its surrounding context words |
| **Skip-gram** | Predicts surrounding context words from a single word |

```
Sentence: "The cat sat on the mat"

CBOW: [The, sat, on] → predicts "cat"
Skip-gram: "cat" → predicts [The, sat, on]
```

### 🔸 Key Properties

- Each word = a vector of 100-300 numbers
- Similar words have similar vectors
- Captures analogies (King - Man + Woman = Queen)
- Pre-trained models available (Google's Word2Vec, trained on billions of words)

### 🔸 BoW vs TF-IDF vs Word2Vec

| | BoW | TF-IDF | Word2Vec |
|---|---|---|---|
| Type | Sparse vector | Sparse vector | Dense vector |
| Size | Vocabulary size | Vocabulary size | 100-300 dimensions |
| Captures meaning? | ❌ | ❌ | ✅ |
| Word order? | ❌ | ❌ | Partially |
| Similar words close? | ❌ | ❌ | ✅ |
| Training needed? | ❌ | ❌ | ✅ |

---

## 🔹 9. GloVe (Global Vectors)

### 🔸 Concept

- Similar to Word2Vec — produces word vectors
- But uses **global word co-occurrence statistics** (how often words appear together across the entire corpus)
- Pre-trained models available (Stanford's GloVe)

### 🔸 Word2Vec vs GloVe

| | Word2Vec | GloVe |
|---|---|---|
| Method | Predicts context (neural network) | Co-occurrence matrix |
| Training | Local context window | Global statistics |
| Result | Similar quality | Similar quality |

✔ In practice, both produce good word embeddings. Choice often depends on the task.

---

## 🔹 10. Word Embeddings — The Big Picture

### 🧠 Analogy

> 👉 Word embeddings are like giving every word a **GPS coordinate**. Similar words have nearby coordinates. The entire vocabulary lives on a map.

### 🔸 Evolution of Text Representation

```
1. One-Hot Encoding → huge sparse vectors, no meaning
2. Bag of Words → word counts, no meaning
3. TF-IDF → word importance, no meaning
4. Word2Vec / GloVe → dense vectors WITH meaning ✅
5. Contextual Embeddings (BERT, GPT) → meaning changes with context ✅✅
```

### 🔸 Static vs Contextual Embeddings

| | Static (Word2Vec, GloVe) | Contextual (BERT, GPT) |
|---|---|---|
| "bank" | Same vector always | Different vector for "river bank" vs "money bank" |
| Context-aware? | ❌ | ✅ |
| Quality | Good | Excellent |
| Speed | Fast | Slower |

---

## 🔹 Common NLP Tasks

| Task | What It Does | Example |
|------|-------------|---------|
| **Text Classification** | Assign category to text | Spam detection, topic labeling |
| **Sentiment Analysis** | Detect emotion/opinion | "Great product!" → Positive |
| **Named Entity Recognition (NER)** | Extract entities | "Giridhar lives in Hyderabad" → Person: Giridhar, Location: Hyderabad |
| **Machine Translation** | Translate languages | English → Hindi |
| **Text Summarization** | Shorten text | Long article → 3-sentence summary |
| **Question Answering** | Answer questions from text | "Who is the CEO?" → "Satya Nadella" |
| **Text Generation** | Generate new text | ChatGPT, story writing |

---

## 🔹 Interview Questions 💡

### Q1: What is the difference between stemming and lemmatization?
**Answer:** Stemming chops off word endings (fast but may produce non-real words like "studi"). Lemmatization uses dictionary/grammar to find the proper root form (slower but always produces real words like "study").

### Q2: What is TF-IDF?
**Answer:** A measure of word importance. TF = how often a word appears in a document. IDF = how rare it is across all documents. TF-IDF = TF × IDF. Common words get low scores, rare meaningful words get high scores.

### Q3: What is Word2Vec?
**Answer:** A technique that converts words into dense numerical vectors where similar words have similar vectors. It captures semantic relationships like "King - Man + Woman ≈ Queen."

### Q4: What is the difference between CBOW and Skip-gram?
**Answer:** CBOW predicts a target word from surrounding context words. Skip-gram predicts surrounding context words from a target word. Skip-gram works better for rare words, CBOW is faster.

### Q5: Why can't we feed raw text directly to ML models?
**Answer:** ML models work with numbers, not text. We must convert text to numerical representations (BoW, TF-IDF, Word2Vec, or embeddings) before feeding it to a model.

### Q6: What are stop words?
**Answer:** Common words like "the", "is", "a" that carry little meaning. Removing them reduces noise and vocabulary size. But be careful — in sentiment analysis, "not" is a stop word that changes meaning.

### Q7: What is the difference between static and contextual embeddings?
**Answer:** Static embeddings (Word2Vec, GloVe) give the same vector for a word regardless of context. Contextual embeddings (BERT, GPT) give different vectors based on context — "bank" in "river bank" vs "money bank" gets different vectors.

---

## 🔹 Complete Summary 📌

| Concept | Description |
|---------|-------------|
| NLP | Teaching machines to understand human language |
| Tokenization | Splitting text into words/sentences |
| Stop Words | Common words with little meaning |
| Stemming | Chop suffixes (fast, rough) |
| Lemmatization | Dictionary lookup (slow, accurate) |
| Bag of Words | Count word frequencies |
| TF-IDF | Measure word importance |
| Word2Vec | Dense vectors capturing meaning |
| GloVe | Global co-occurrence vectors |
| CBOW | Predict word from context |
| Skip-gram | Predict context from word |
| Embeddings | Words as numerical vectors |
| Static embeddings | Same vector always (Word2Vec) |
| Contextual embeddings | Vector changes with context (BERT) |
| Sentiment Analysis | Detect positive/negative opinion |
| NER | Extract names, places, dates |

---

> 🚀 **Next:** Deep Learning Basics →
