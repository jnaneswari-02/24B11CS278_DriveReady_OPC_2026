# AI Agents Workshop -- Level 1, Day 1

## Your First LLM API Call with Groq and Google Colab

This project follows **Day 1: Fundamentals** of the AI Agents Workshop.
It introduces LLMs, tokens, temperature, conversation history, context
windows, hallucinations, and the basic API-call workflow.

The practical exercise uses **Sweet Crumbs Home Bakery** as a case
study. The goal is to build a small customer-support assistant that
answers questions using the bakery's supplied facts and rules.

## Learning objectives

-   Understand how an LLM generates text by predicting the next token.
-   Learn what tokens are and why they affect cost and context limits.
-   Understand how temperature changes response variation.
-   Understand why an API model does not automatically remember earlier
    calls.
-   Learn what a context window is and how hallucinations can be reduced
    with supplied facts.
-   Make an API request using Python, Google Colab, and Groq.

## Requirements

-   A Google account and a notebook running in [Google
    Colab](https://colab.research.google.com/).
-   A Groq account and API key from [Groq Console -- API
    Keys](https://console.groq.com/keys).
-   Internet access in the Colab runtime.

## Setup

### 1. Create a Colab notebook

Open Google Colab and create a new notebook.

### 2. Store the API key in Colab Secrets

1.  Open the **Secrets** panel using the key icon in Colab's left
    sidebar.
2.  Add a secret named `GROQ_API_KEY`.
3.  Paste your Groq API key as its value.
4.  Turn on **Notebook access** for that secret.

**Security:** Never write the actual API key directly in a notebook
cell, commit it to Git, or share it in screenshots. If a key is exposed,
revoke it in Groq Console and create a replacement.

### 3. Install the client library

Run this in a Colab code cell:

``` python
!pip install -q openai
```

### 4. Load the secret and create the Groq client

``` python
from google.colab import userdata
from openai import OpenAI

GROQ_API_KEY = userdata.get("GROQ_API_KEY")

client = OpenAI(
    api_key=GROQ_API_KEY,
    base_url="https://api.groq.com/openai/v1"
)

print("Groq client setup completed!")
```

The `userdata.get()` call is intended for a notebook running in Google
Colab with the secret configured and notebook access enabled.

## Practical assignment: Sweet Crumbs Home Bakery

### 5. Define the system prompt

The prompt contains five business facts and three response rules.

``` python
SYSTEM = """
ROLE:
You are a friendly customer support assistant
for Sweet Crumbs Home Bakery.

FACTS:
1. We bake cakes only after receiving orders.
2. Orders require 24 hours advance notice.
3. Eggless cakes are available.
4. Plum cake costs Rs 500.
5. Chocolate cake costs Rs 650.

RULES:
1. Never provide incorrect prices or information.
2. Never promise a delivery time.
3. If information is unavailable, say
   "I'll check with the owner."

FORMAT:
Give short, friendly answers in English or Telugu,
matching the customer's language.
Keep answers under 50 words.
"""
```

### 6. Create a function to ask questions

``` python
def ask_ai(question):
    response = client.chat.completions.create(
        model="openai/gpt-oss-20b",
        temperature=0.2,
        messages=[
            {"role": "system", "content": SYSTEM},
            {"role": "user", "content": question}
        ]
    )

    print("Customer:", question)
    print("\nAI Response:")
    print(response.choices[0].message.content)

    print("\nToken Usage:")
    print("Input tokens:", response.usage.prompt_tokens)
    print("Output tokens:", response.usage.completion_tokens)
    print("Total tokens:", response.usage.total_tokens)
    print("-" * 60)
```

### 7. Ask three customer questions

``` python
questions = [
    "Can I order an eggless chocolate cake?",
    "What is the price of a plum cake?",
    "Can I get a chocolate cake today evening?"
]

for question in questions:
    ask_ai(question)
```

Expected behaviour:

  -----------------------------------------------------------------------
  Customer question                   Expected behaviour
  ----------------------------------- -----------------------------------
  Can I order an eggless chocolate    Explain that eggless cakes are
  cake?                               available.

  What is the price of a plum cake?   Give the supplied price: Rs 500.

  Can I get a chocolate cake today    Explain the 24-hour advance-notice
  evening?                            requirement; do not promise
                                      same-day availability.
  -----------------------------------------------------------------------

The model's exact wording may vary. Check that its answer follows the
supplied facts and rules.

### 8. Compare temperature settings (additional practice)

``` python
for temp in [0.2, 1.2]:
    response = client.chat.completions.create(
        model="openai/gpt-oss-20b",
        temperature=temp,
        messages=[
            {"role": "system", "content": SYSTEM},
            {
                "role": "user",
                "content": "Write a creative tagline for Sweet Crumbs Bakery"
            }
        ]
    )

    print("Temperature:", temp)
    print(response.choices[0].message.content)
    print("-" * 50)
```

A lower temperature generally produces more focused, repeatable
responses. A higher temperature generally allows more variation. The
exact effect depends on the model and provider.

## Troubleshooting

### `TimeoutException` while reading `GROQ_API_KEY`

-   Confirm that the notebook is open and running on Google Colab, not a
    local Jupyter runtime.
-   Confirm the secret name is exactly `GROQ_API_KEY`.
-   Confirm Notebook access is enabled for the secret.
-   Refresh or reopen the notebook and retry. A temporary Colab Secrets
    service issue can also cause a timeout.

### `SecretNotFoundError`

The secret may be missing or its name may not match. Recheck the
spelling in the Colab Secrets panel.

### `401 AuthenticationError`

The key may be invalid, revoked, or expired. Create a new key in Groq
Console and update the Colab secret. Do not paste the key into a shared
notebook.

### `404 model not found`

The model identifier may no longer be available to your account. Check
the model names currently supported by Groq and update the `model`
value.

### `429 RateLimitError`

The request may have reached a rate limit. Wait and retry according to
the provider's limits.

## Day 1 completion checklist

-   [ ] Created a Google Colab notebook.
-   [ ] Created a Groq API key.
-   [ ] Saved it as `GROQ_API_KEY` in Colab Secrets.
-   [ ] Enabled Notebook access.
-   [ ] Installed the `openai` Python package.
-   [ ] Created the Groq client successfully.
-   [ ] Added a system prompt with five facts and three rules.
-   [ ] Asked three customer questions.
-   [ ] Checked the answers against the bakery facts and rules.
-   [ ] Viewed input, output, and total token usage.
-   [ ] Tried the temperature comparison (additional practice).

## Key concepts recap

  -----------------------------------------------------------------------
  Concept                             Main idea
  ----------------------------------- -----------------------------------
  API                                 Lets your code send a request to a
                                      hosted model and receive a
                                      response.

  LLM                                 Generates text by predicting the
                                      next token repeatedly.

  Token                               A piece of text used for model
                                      input, output, cost, and limits.

  Temperature                         Controls how varied or predictable
                                      generation tends to be.

  Memory                              The application can resend earlier
                                      messages as conversation history.

  Context window                      The token budget for instructions,
                                      history, documents, and the reply.

  Hallucination                       A fluent answer can still be
                                      incorrect; provide trusted facts
                                      and verify outputs.

  AI engineering                      Connect a model, give it context,
                                      obtain an answer, and wrap it in an
                                      interface.
  -----------------------------------------------------------------------

## Before Day 2

Prepare **10 common customer questions** for the business you choose.
Day 2 will build on the first API call by working with a system prompt,
chatbot conversation history, and a test file.

------------------------------------------------------------------------

**Note:** The model identifier and provider limits can change. Check
Groq's current model availability if the example model is unavailable.
This README is a learning guide; successful completion should be
confirmed by running the notebook cells and checking their outputs.
