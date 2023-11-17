# ChatGPT-Prompt-Output-Parser
Use LangChain's Output Parser to Extract Information from ChatGPT Prompt Response

## Overview

This Jupyter notebook demonstrates how to use LangChain's `StructuredOutputParser` to extract structured information from ChatGPT prompt responses.

## Key Points

- Imports necessary libraries like `OpenAI`, `LangChain`, and defines a `ChatOpenAI` instance.

- Defines example output structure with fields like `"gift"`, `"delivery_days"`, `"price_value"`. 

- Shows a sample customer review text to be parsed.

- Constructs `ResponseSchema` objects for each output field.

- Creates a `StructuredOutputParser` using the response schemas.

- Defines a prompt template that incorporates the parser's format instructions. 

- Prompts ChatGPT to analyze the review text and output in the structured format.

- Parses the JSON response to extract the gift, delivery days, and price value into a dictionary.

## Summary 

In summary, the notebook shows how LangChain's output parser can be used to get structured data from free-form ChatGPT responses, enabling prompt engineering for information extraction.

## Code Description

Jupyter notebook link: [langchain_output_parser_prompt_engineering.ipynb](https://github.com/rukshar69/ChatGPT-Prompt-Output-Parser/blob/main/langchain_output_parser_prompt_engineering.ipynb)


