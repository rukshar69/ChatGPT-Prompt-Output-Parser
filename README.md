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

Jupyter notebook link: [langchain_output_parser_prompt_engineering.ipynb](https://github.com/rukshar69/ChatGPT-Prompt-Output-Parser/blob/main/langchain_output_parser_prompt_engineering.ipynb) (The experiment is conducted in Google Colab)

- To use OpenAI's *gpt-3.5-turbo* model with LangChain, an API key is required. The API key can be obtained from [here](https://platform.openai.com/account/api-keys).

- To control the randomness and creativity of the generated text by the LLM, we used temperature = 0.0 when initializing the `ChatOpenAI` instance. Temperature is a numerical value set between 0 and 1. A temperature of 0 means that the model will always choose the most likely word to generate, while a temperature of 1 means that the model is more likely to choose less likely words, resulting in more creative and unexpected output. In general, the optimal temperature setting depends on the specific task at hand. For tasks that require accuracy and factuality, such as question answering or summarizing text, a lower temperature is usually preferred. For tasks that require creativity and originality, such as writing poetry or generating story ideas, a higher temperature may be more suitable. Since our task is to extract structured information from ChatGPT prompt responses, we set the temperature to 0.0.

- Output parser: Language models output text. But many times you want to get more *structured information* than just text. This is where **output parsers** help structure language model responses. There are **two** main methods an output parser must implement:

    - "**Get format instructions**": A method which returns a string containing instructions for how the output of a language model should be formatted.
    - "**Parse**": A method which takes in a string (assumed to be the response from a language model) and parses it into some structure.

- For our prompt engineering, we analyze customer reviews to extract 3 info:
    - **gift**: Was the item purchased as a gift for someone else? Answer True if yes, False if not or unknown.
    - **delivery_days**: How many days did it take for the product to arrive? If this information is not found, output -1.
    - **price_value**: Extract any sentences about the value or price of the product.

- An example structure of the output from a review that we want to parse:
    ```json
    {
        "gift": true,
        "delivery_days": 3,
        "price_value": "pretty affordable!"
    }
    ```

- Prompt template:
    ```
    For the following text, extract the following information:

    gift: Was the item purchased as a gift for someone else? 
    Answer True if yes, False if not or unknown.

    delivery_days: How many days did it take for the product
    to arrive? If this information is not found, output -1.

    price_value: Extract any sentences about the value or price,
    and output them as a comma separated Python list.

    text: {text}

    {format_instructions}
    ```
    Here, *text* refers to the customer review and *format_instructions* is a string containing instructions for how the output of the language model should be formatted.

- The LLM response can then be easily fed into the output parser to get structured data in our desired JSON/dictionary format. 

- As an example we used the following review:
    ```
    This leaf blower is pretty amazing.  It has four settings:
    candle blower, gentle breeze, windy city, and tornado. 
    It arrived in two days, just in time for my wife's 
    anniversary present. 
    I think my wife liked it so much she was speechless. 
    So far I've been the only one using it, and I've been 
    using it every other morning to clear the leaves on our lawn. 
    It's slightly more expensive than the other leaf blowers 
    out there, but I think it's worth it for the extra features.
    ```

- The output parser has output:
    ```json
    {
        'gift': False,
        'delivery_days': '2',
        'price_value': "It's slightly more expensive than the other leaf blowers out there, but I think it's worth it for the extra features."
    }
    ```

## References

- [OpenAI](https://platform.openai.com/docs/models/gpt-3-5-turbo)
- [LangChain Output Parser](https://python.langchain.com/docs/modules/model_io/output_parsers/)
- [Structured Output Parser](https://python.langchain.com/docs/modules/model_io/output_parsers/structured)
- [DLAI Course on LangChain](https://learn.deeplearning.ai/langchain/lesson/1/introduction)