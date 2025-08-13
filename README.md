# LLM Metadata Repository

This repository provides structured, machine-readable metadata for a wide range of large language models (LLMs). It is designed to support tools and applications that require detailed information about model capabilities, configurations, and supported parameters. Used by [BasiliskLLM](https://github.com/SigmaNight/basiliskLLM/) and [OpenAI NVDA Add-on](https://github.com/AAClause/nvda-OpenAI/).

This metadata enables:

- Dynamic population of model selection UIs
- Feature-aware prompting and parameter tuning
- Compatibility and capability checks for downstream tools

The metadata is stored in JSON format and is inspired by the [OpenRouter API model listing schema](https://openrouter.ai/docs).

Each JSON file in the data/ directory contains a list of model objects with the following structure:

```json
{
  "id": "gpt-5",
  "name": "GPT-5",
  "description": "OpenAI’s most advanced model...",
  "created": 1754587413,
  "context_length": 400000,
  "architecture": {
    "modality": "text+image->text",
    "input_modalities": ["text", "image", "file"],
    "output_modalities": ["text"],
    "tokenizer": "GPT",
    "instruct_type": null
  },
  "top_provider": {
    "context_length": 400000,
    "max_completion_tokens": 128000,
    "is_moderated": true
  },
  "supported_parameters": [
    "max_tokens",
    "temperature",
    "response_format",
    "structured_outputs"
  ]
}
```

## Metadata Fields

### Top-Level Fields

- id: Unique model identifier (e.g., gpt-4-turbo)
- name: Human-readable model name
- description: Summary of model capabilities and use cases
- created: Unix timestamp of model release
- context_length: Maximum input context length (in tokens)

### architecture

- modality: Overall input/output modality (e.g., text->text, text+image->text)
- input_modalities: Supported input types (e.g., text, image, file)
- output_modalities: Supported output types (e.g., text)
- tokenizer: Tokenizer type used by the model (e.g., GPT)
- instruct_type: Instruction tuning format (e.g., chatml, alpaca), or null if not applicable

### top_provider

- context_length: Maximum context length supported by the top provider
- max_completion_tokens: Maximum number of tokens in a single response
- is_moderated: Indicates whether the model is subject to content moderation

### supported_parameters

A list of tunable parameters supported by the model, such as:

- max_tokens
- temperature
- top_p
- frequency_penalty
- presence_penalty
- tools
- seed
- response_format
- structured_outputs

## Contributing

Contributions are welcome! To add or update metadata for a model:

1. Fork the repository
2. Add or edit the appropriate JSON file in the data/ directory
3. Submit a pull request

Please ensure your JSON is valid and follows the schema outlined above.
