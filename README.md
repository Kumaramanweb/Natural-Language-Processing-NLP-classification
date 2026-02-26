
# Bodywash Product Review Classification using LLaMA-3.3-70B (Groq API)

## Author
Aman Kumar  
B.Tech CSE, IIT Patna  

🔗 GitHub Repository:  
https://github.com/Kumaramanweb/Natural-Language-Processing-NLP-classification.git

---

# Overview

This project performs **automatic classification of bodywash product reviews into Level-1 Factors** using a **pretrained Large Language Model (LLM)**.

Each review is assigned **one or more factor**  such as:

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

This assignment is a **Natural Language Processing (NLP) case study** designed to evaluate technical skills in text classification using Large Language Models (LLMs).

The objective is to classify bodywash product reviews into predefined Level 1 Factors.

These factors represent **labels, categories, or tags** that describe different aspects of the product.

---

## Dataset Description

Two files are provided:

### 1. bodywash-train.xlsx

This file contains:

- Core Item → Bodywash product review text
- Level 1 Factors → Corresponding classification labels

Each review is already mapped to one or more Level 1 Factors.

These factors represent different product aspects such as:

- Fragrance
- Packaging
- Price
- Brand Value
- Product Safety
- Skin Care
- etc.

This dataset is used to:

- Understand classification categories
- Extract the list of possible Level 1 Factors

---

### 2. bodywash-test.xlsx

This file contains:

- Core Item → Bodywash product review text
- Level 1 Factors → Empty column

The goal is to:

Predict and assign the correct Level 1 Factors for each review.

Each review may belong to:

- One factor  
or  
- Multiple factors  

The task is to find **all relevant associations between the review and Level 1 Factors**.

---

## Task Objective

The main objective is to build an NLP-based classification system that:

- Reads product review text
- Understands its semantic meaning
- Assigns the correct Level 1 Factor(s)

---

## Model Requirements

The assignment requires the use of:

Large Language Models (LLMs)

Examples:

- LLaMA
- Mixtral
- GPT
- Gemma

You may use any free LLM inference provider such as:

- Groq Cloud
- Google Cloud Platform (GCP)

---

## Restriction

BERT model is NOT allowed for this assignment.

This restriction ensures the use of modern Large Language Models instead of traditional transformer classification models.

---

## Expected Output

The final output should be:

bodywash-test file with Level 1 Factors column filled.

Each test review should be assigned its correct factor(s).

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


Training Data  
↓  
Extract Factors  
↓  
Test Review  
↓  
Prompt Creation  
↓  
Send to LLaMA-3.3 Model  
↓  
Model analyzes semantic meaning  
↓  
Model selects best matching factor  
↓  
Output saved  





# How Training Data is Used

The training dataset is used ONLY to extract:

Level 1 Factors

Example: Fragrance, Packaging, Price, Brand Value


These factors are provided to model in prompt.

The model then selects the best factor.

No model training or fine-tuning is performed.

---

# Code Explanation

## Step1: Install libraries

```python
!pip install groq pandas openpyxl tqdm
```

## Step 2: Import Libraries

```python
import pandas as pd
from groq import Groq
from tqdm import tqdm
```

## Step3: Load Dataset

```python
train = pd.read_excel("bodywash-train.xlsx")
test = pd.read_excel("bodywash-test.xlsx")
```

## Step 3: Extract Factors

```python
factors = train['Level 1 Factors'].dropna().unique()
factor_list = ", ".join(factors)
```

## Step 4: Connect to Model

```python
client = Groq(api_key="YOUR_API_KEY")
```
## Step 5: Classification Function
---Prompt Creation
---Send Prompt to Model
---Extract Model Output

```python
def classify(text):

    prompt = f"""
You are an expert product classifier.

Classify the following customer review into one or more of these Level 1 Factors:

{factor_list}

Rules:

• Only choose from given factors
• Do NOT create new factors
• If multiple apply, separate by comma
• Output only factor names

Review:
{text}
"""

    response = client.chat.completions.create(

        model="llama-3.3-70b-versatile",

        messages=[

            {"role": "user", "content": prompt}

        ]

    )

    return response.choices[0].message.content.strip()
```

## Step 6: Apply to Test Data

```python
predictions = []

for text in tqdm(test['Core Item']):

    pred = classify(text)

    predictions.append(pred)
```


# Tools and Technologies Used

| Tool | Purpose |
|---|---|
| Python | Programming |
| Groq API | Model access |
| LLaMA-3.3-70B | Classification model |
| Pandas | Data processing |
| Google Colab | Execution |


# Advantages of Prompt-Based Approach

| Advantage | Explanation |
|---|---|
| No Training Required | The pretrained LLM already understands language, so no additional model training is needed |
| High Accuracy | Modern LLMs like LLaMA-3.3 provide highly accurate classification results |
| Fast Implementation | No need for data preprocessing, feature engineering, or training |
| Easy to Implement | Requires only prompt design and API call |
| Industry Standard Approach | Widely used in real-world NLP applications and production systems |

---

# Summary

This project demonstrates the application of Large Language Models for:

- Text classification
- NLP automation
- Semantic understanding of product reviews

using prompt-based classification techniques.



