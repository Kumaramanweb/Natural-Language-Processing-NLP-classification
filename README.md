
# Bodywash Product Review Classification using LLaMA-3.3-70B (Groq API)

## Author
Aman Kumar  
B.Tech CSE, IIT Patna  

---

# Overview

This project performs **automatic classification of bodywash product reviews into Level-1 Factors** using a **pretrained Large Language Model (LLM)**.

Each review is assigned exactly **one factor** such as:

- Fragrance
- Packaging
- Price
- Brand Value
- Product Safety
- Skin Care
- etc.

This is a **Natural Language Processing (NLP) classification task**.

---

# Problem Statement

Given:

**Training File**

bodywash-train.xlsx

Contains:

- Core Item (Review text)
- Level 1 Factors (Labels)

**Test File**

bodywash-test.xlsx

Contains:

- Core Item
- Level 1 Factors (Empty)

Goal:

Predict Level 1 Factors for test data.

---

# Model Used

## LLaMA-3.3-70B-Versatile

Accessed via:

Groq API

---

# Why this Model was Used

LLaMA-3.3-70B was selected because:

• State-of-the-art Large Language Model  
• Excellent performance on NLP classification tasks  
• Strong semantic understanding  
• No additional training required  
• Fast inference using Groq  
• Free access via Groq Cloud  

This makes it ideal for zero-shot text classification.

---

# Technique Used

## Prompt-Based Zero-Shot Classification

This project uses:

Zero-Shot Learning

Meaning:

The model was NOT trained on the provided dataset.

Instead:

The model uses its pretrained knowledge and classifies text using prompt instructions.

---

# How Model Works Conceptually

The workflow:





# How Training Data is Used

The training dataset is used ONLY to extract:

Level 1 Factors

Example: Fragrance, Packaging, Price, Brand Value


These factors are provided to model in prompt.

The model then selects the best factor.

No model training or fine-tuning is performed.

---

# Code Explanation

## Step 1: Import Libraries

```python
import pandas as pd
from groq import Groq
