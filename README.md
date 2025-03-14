# Day 1 - Prompting with Gemini API

This notebook is part of the Kaggle 5-day Generative AI course, designed to help you get started with the Gemini API and explore various prompting techniques. The notebook walks you through example prompts and techniques, which are also covered in the Prompting whitepaper. You don't need to read the whitepaper to use this notebook, but it provides additional theoretical context and background.

## Table of Contents
1. [Introduction](#introduction)
2. [Before You Begin](#before-you-begin)
3. [Getting Started with Kaggle Notebooks](#getting-started-with-kaggle-notebooks)
4. [Setting Up the Gemini API](#setting-up-the-gemini-api)
   - [Installing the SDK](#installing-the-sdk)
   - [Setting Up Your API Key](#setting-up-your-api-key)
5. [Running Your First Prompt](#running-your-first-prompt)
6. [Starting a Chat](#starting-a-chat)
7. [Choosing a Model](#choosing-a-model)
8. [Exploring Generation Parameters](#exploring-generation-parameters)
   - [Output Length](#output-length)
   - [Temperature](#temperature)
   - [Top-K and Top-P](#top-k-and-top-p)
9. [Prompting Techniques](#prompting-techniques)
   - [Zero-Shot Prompting](#zero-shot-prompting)
   - [One-Shot and Few-Shot Prompting](#one-shot-and-few-shot-prompting)
   - [Chain of Thought (CoT)](#chain-of-thought-cot)
   - [ReAct: Reason and Act](#react-reason-and-act)
10. [Code Prompting](#code-prompting)
    - [Generating Code](#generating-code)
    - [Code Execution](#code-execution)
    - [Explaining Code](#explaining-code)
11. [Learn More](#learn-more)

## Introduction
This notebook introduces you to the Gemini API and demonstrates how to use it for various tasks, including text generation, chat, and code generation. You'll explore different prompting techniques and learn how to fine-tune model parameters to achieve desired outputs.

## Before You Begin
Before diving into the notebook, you might want to explore some apps built using the Gemini family of models:
- [TextFX](https://textfx.withgoogle.com/): A suite of AI-powered tools for rappers.
- [SQL Talk](https://sql-talk-r5gdynozbq-uc.a.run.app/): A tool to talk directly to a database using the Gemini API.
- [NotebookLM](https://notebooklm.google/): A personal AI research assistant.

## Getting Started with Kaggle Notebooks
If you're new to Kaggle notebooks, you'll need to verify your account and make a copy of this notebook to run the code. Follow the instructions in the notebook to get started.

## Setting Up the Gemini API
### Installing the SDK
Install the Gemini Python SDK using the following command:
```bash
%pip install -U -q "google-generativeai>=0.8.3"
```

### Setting Up Your API Key
To use the Gemini API, you need to set up your API key. Store it in a Kaggle secret named `GOOGLE_API_KEY`. Follow the instructions in the notebook to add and enable your key.

## Running Your First Prompt
Test your API key by running a simple prompt:
```python
flash = genai.GenerativeModel('gemini-1.5-flash')
response = flash.generate_content("Explain AI to me like I'm a kid.")
print(response.text)
```

## Starting a Chat
You can also set up a multi-turn chat structure:
```python
chat = flash.start_chat(history=[])
response = chat.send_message('Hello! My name is Zlork.')
print(response.text)
```

## Choosing a Model
The Gemini API provides access to various models. List all available models and their capabilities:
```python
for model in genai.list_models():
  print(model.name)
```

## Exploring Generation Parameters
### Output Length
Control the output length using the `max_output_tokens` parameter:
```python
short_model = genai.GenerativeModel(
    'gemini-1.5-flash',
    generation_config=genai.GenerationConfig(max_output_tokens=200))
```

### Temperature
Adjust the temperature to control randomness in token selection:
```python
high_temp_model = genai.GenerativeModel(
    'gemini-1.5-flash',
    generation_config=genai.GenerationConfig(temperature=2.0))
```

### Top-K and Top-P
Use top-K and top-P parameters to control the diversity of the model's output:
```python
model = genai.GenerativeModel(
    'gemini-1.5-flash-001',
    generation_config=genai.GenerationConfig(
        temperature=1.0,
        top_k=64,
        top_p=0.95,
    ))
```

## Prompting Techniques
### Zero-Shot Prompting
Zero-shot prompts describe the request directly:
```python
zero_shot_prompt = """Classify movie reviews as POSITIVE, NEUTRAL or NEGATIVE.
Review: "Her" is a disturbing study revealing the direction
humanity is headed if AI is allowed to keep evolving,
unchecked. I wish there were more movies like this masterpiece.
Sentiment: """
```

### One-Shot and Few-Shot Prompting
Provide examples to guide the model's response:
```python
few_shot_prompt = """Parse a customer's pizza order into valid JSON:
EXAMPLE:
I want a small pizza with cheese, tomato sauce, and pepperoni.
JSON Response:
```
{
"size": "small",
"type": "normal",
"ingredients": ["cheese", "tomato sauce", "peperoni"]
}
```
"""

### Chain of Thought (CoT)
Encourage the model to output intermediate reasoning steps:
```python
prompt = """When I was 4 years old, my partner was 3 times my age. Now,
I am 20 years old. How old is my partner? Let's think step by step."""
```

### ReAct: Reason and Act
Use ReAct prompting to perform step-by-step reasoning and actions:
```python
model_instructions = """
Solve a question answering task with interleaving Thought, Action, Observation steps.
"""
```

## Code Prompting
### Generating Code
Generate code using the Gemini API:
```python
code_prompt = """
Write a Python function to calculate the factorial of a number. No explanation, provide only the code.
"""
```

### Code Execution
Automatically run generated code and return the output:
```python
model = genai.GenerativeModel(
    'gemini-1.5-flash-latest',
    tools='code_execution',)
```

### Explaining Code
Explain code at a high level:
```python
explain_prompt = """
Please explain what this file does at a very high level. What is it, and why would I use it?
```
{file_contents}
```
"""
```

## Learn More
To dive deeper into prompting and the Gemini API:
- Read the whitepaper issued with today's content.
- Explore the apps listed at the top of this notebook.
- Check out the [Introduction to Prompting](https://ai.google.dev/gemini-api/docs/prompting-intro) from the Gemini API docs.
- Visit the Gemini API's [prompt gallery](https://ai.google.dev/gemini-api/prompts) and try them out in AI Studio.
- Explore the Gemini API cookbook for [inspirational examples](https://github.com/google-gemini/cookbook/blob/main/examples/) and [educational quickstarts](https://github.com/google-gemini/cookbook/blob/main/quickstarts/).

Share your exciting experiments in the Kaggle Discord!
