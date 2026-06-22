# Transformers

## Topics Covered

- What happens when you send a message to an LLM
- How transformers process text internally
- Tokenization and how text becomes numbers
- Attention mechanism and why it matters
- Embeddings and vector space intuition
- Context windows and what happens when you exceed them

---

# 1. What Happens When You Send a Message to an LLM

Let's use the same example throughout all topics:

**User Input**

```text
Why is the sky blue?
```

## High-Level Flow

```text
User Message
      ↓
Tokenization
      ↓
Convert Tokens to Numbers
      ↓
Embeddings
      ↓
Transformer Layers
      ↓
Attention Mechanism
      ↓
Next Token Prediction
      ↓
Generated Response
```

## Step 1: User Sends Text

```text
Why is the sky blue?
```

The LLM cannot directly understand text.

It understands numbers.

---

## Step 2: Tokenization

The sentence is split into tokens.

```text
Why
is
the
sky
blue
?
```

Possible token IDs:

```text
[4512, 318, 262, 6766, 4171, 30]
```

---

## Step 3: Convert Tokens into Embeddings

Each token becomes a vector.

```text
Why → [0.24, -0.82, 0.17, ...]
sky → [0.91, 0.11, -0.52, ...]
```

Words become mathematical representations.

---

## Step 4: Process Through Transformer Layers

Example:

```text
Layer 1
Layer 2
Layer 3
...
Layer N
```

Each layer extracts deeper meaning.

---

## Step 5: Attention

The model determines:

> Which words are important for understanding this sentence?

For:

```text
Why is the sky blue?
```

The word **blue** pays more attention to:

```text
sky
Why
```

than to:

```text
is
the
```

---

## Step 6: Predict Next Token

The model predicts one token at a time.

```text
The
sky
appears
blue
because
...
```

---

## Step 7: Generate Final Response

```text
The sky appears blue because Earth's atmosphere scatters blue wavelengths of sunlight more than other colors.
```

---

## Analogy

Imagine a student answering a question.

```text
Teacher: Why is the sky blue?
```

The student:

1. Reads the question
2. Understands the words
3. Connects concepts
4. Thinks about science
5. Answers

A Transformer performs a mathematical version of the same process.

---

# 2. How Transformers Process Text Internally

Transformers are the architecture behind modern LLMs.

Examples:

- GPT
- ChatGPT
- Claude
- Gemini
- Llama

---

## Before Transformers

Older models processed text sequentially.

```text
Word1 → Word2 → Word3 → Word4
```

Problems:

- Slow
- Limited memory
- Difficulty handling long sentences

---

## Transformers

Transformers process all words simultaneously.

```text
Word1
Word2
Word3
Word4
    ↓
Processed Together
```

This enables better understanding of relationships between words.

---

## Transformer Pipeline

```text
Input Text
     ↓
Tokenization
     ↓
Embeddings
     ↓
Positional Encoding
     ↓
Multi-Head Attention
     ↓
Feed Forward Network
     ↓
Output Prediction
```

---

## Example

Input:

```text
Why is the sky blue?
```

Tokens:

```text
[Why] [is] [the] [sky] [blue]
```

Transformer examines:

```text
sky ↔ blue
Why ↔ blue
sky ↔ Why
```

instead of reading one word at a time.

---

## Why Transformers Are Powerful

### Traditional Models

```text
Word1 → Word2 → Word3 → Word4
```

Need to remember previous words.

### Transformers

```text
Word1 ↔ Word2 ↔ Word3 ↔ Word4
```

Every word can directly interact with every other word.

---

# 3. Tokenization and How Text Becomes Numbers

Computers do not understand words.

They understand numbers.

---

## Example

Input:

```text
Why is the sky blue?
```

Token IDs:

```text
[4512, 318, 262, 6766, 4171, 30]
```

---

## What Is a Token?

A token can be:

### Entire Word

```text
sky
```

### Part of a Word

```text
play
ing
```

### Punctuation

```text
?
,
.
```

### Special Character

```text
$
@
#
```

---

## Example

Input:

```text
JavaScript is awesome
```

Possible tokens:

```text
Java
Script
is
awesome
```

Token IDs:

```text
[2312, 8755, 542, 8891]
```

---

## Why Not Store Entire Words?

Consider:

```text
play
playing
played
player
```

Instead of storing all variations, tokenizers reuse smaller pieces.

Benefits:

- Smaller vocabulary
- Better handling of new words
- Lower memory requirements

---

## Analogy

Think of LEGO blocks.

Instead of storing every possible building:

```text
House A
House B
House C
```

Store reusable pieces:

```text
Door
Window
Wall
Roof
```

Tokens are the LEGO blocks of language.

---

# 4. Attention Mechanism and Why It Matters

Attention is the core innovation of Transformers.

---

## Problem Without Attention

Sentence:

```text
The animal didn't cross the road because it was tired.
```

Question:

```text
Who was tired?
```

Possible interpretations:

```text
animal
road
```

Humans know:

```text
animal
```

Older models often struggled with this.

---

## How Attention Helps

The word:

```text
tired
```

looks back and identifies:

```text
animal
```

as the most relevant context.

---

## Example

Sentence:

```text
Why is the sky blue?
```

When processing:

```text
blue
```

the model focuses more on:

```text
sky
Why
```

than on:

```text
is
the
```

---

## Example Attention Scores

| Word | Score |
|--------|--------|
| sky | 0.60 |
| Why | 0.20 |
| blue | 0.15 |
| is | 0.03 |
| the | 0.02 |

Higher score means:

```text
This word is more important right now.
```

---

## Analogy

Imagine being in a noisy meeting.

Many people are speaking.

Someone says:

```text
Deadline
```

Immediately your focus shifts.

Attention works similarly by identifying important information.

---

# 5. Embeddings and Vector Space Intuition

After tokenization:

```text
sky
```

becomes:

```text
6766
```

But token IDs contain no meaning.

---

## Problem

```text
cat = 100
dog = 101
car = 102
```

These numbers do not indicate relationships.

---

## Solution: Embeddings

Convert words into vectors.

```text
cat
→ [0.2, 0.5, -0.1, ...]
```

```text
dog
→ [0.3, 0.4, -0.2, ...]
```

Similar words receive similar vectors.

---

## Vector Space Visualization

```text
cat      dog

      animal

car      truck
```

Animals cluster together.

Vehicles cluster together.

---

## Famous Example

```text
King - Man + Woman ≈ Queen
```

Because embeddings capture semantic relationships.

---

## Why Embeddings Matter

The model learns:

```text
cat ≈ kitten
dog ≈ puppy
car ≈ vehicle
```

even when the words differ.

---

## Analogy

Imagine a city map.

Animals live in one neighborhood.

```text
cat
dog
kitten
puppy
```

Vehicles live in another.

```text
car
truck
bus
```

Embeddings create this semantic map.

---

# 6. Context Windows and What Happens When You Exceed Them

A context window is the model's working memory.

---

## Example

Suppose a model supports:

```text
8,000 tokens
```

Everything must fit inside:

- Conversation history
- Instructions
- Documents
- Code
- User prompts

---

## Analogy

Imagine a whiteboard.

```text
Whiteboard Size = Context Window
```

You can write only so much.

When the board fills up:

```text
Old content gets erased.
```

---

## Example Conversation

```text
Message 1
Message 2
Message 3
...
Message 100
```

If the conversation becomes too large:

```text
Message 1
Message 2
```

may no longer be visible to the model.

---

## What Happens When the Limit Is Exceeded?

### Earlier Context Is Dropped

Example:

```text
My name is Tauseef.
```

Hundreds of messages later:

```text
What is my name?
```

The model may no longer know.

---

### Instructions Can Be Lost

Important requirements may disappear.

---

### Long-Term References Break

The model may lose track of:

- Previous code
- Earlier requirements
- Initial design decisions

---

## How Modern Systems Handle This

Techniques include:

- Larger context windows
- Retrieval-Augmented Generation (RAG)
- Memory systems
- Context compression
- Summarization

---

# End-to-End Summary

```text
User Message
      ↓
Tokenization
      ↓
Token IDs
      ↓
Embeddings
      ↓
Positional Encoding
      ↓
Attention
      ↓
Transformer Layers
      ↓
Next Token Prediction
      ↓
Generated Response
```

---

# Practice Exercises

## Exercise 1

Tokenize:

```text
JavaScript powers modern web applications.
```

Identify possible tokens.

---

## Exercise 2

Explain why:

```text
King - Man + Woman = Queen
```

works using embeddings.

---

## Exercise 3

For:

```text
The cat chased the mouse because it was hungry.
```

Which word should **hungry** attend to?

---

## Exercise 4

Draw and explain:

```text
Input
→ Tokens
→ Embeddings
→ Attention
→ Transformer Layers
→ Output
```

in your own words.

---

# Mini Project (JavaScript Developer)

Build a **Mini Transformer Visualizer**.

## Features

```text
1. Enter text
2. Tokenize text
3. Assign token IDs
4. Create mock embeddings
5. Display attention scores
6. Predict next word
```

## Tech Stack

```text
HTML
CSS
JavaScript
```

## Learning Outcome

By building this project you will understand:

- Tokenization
- Embeddings
- Attention
- Context
- Next-token prediction

which are the foundational concepts behind modern LLMs and Transformers.
