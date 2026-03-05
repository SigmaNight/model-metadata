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
- created: Unix timestamp of model release (used for sorting by release date; models with `-latest` in the id are listed first)
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

## Data Sources

Metadata is curated from official provider documentation and APIs. Official model listings:

- **OpenAI**: [Models](https://platform.openai.com/docs/models) · [API Reference](https://platform.openai.com/docs/api-reference/models/list)
- **Anthropic**: [Models Overview](https://docs.anthropic.com/en/docs/models-overview) · [API Models](https://docs.anthropic.com/en/api/getting-started/models)
- **Mistral AI**: [Models](https://docs.mistral.ai/getting-started/models) · [Model Comparison](https://docs.mistral.ai/getting-started/models/compare)
- **xAI**: [Models and Pricing](https://docs.x.ai/docs/models) · [Release Notes](https://docs.x.ai/docs/release-notes)
- **Google**: [Gemini API Models](https://ai.google.dev/api/models) · [Vertex AI Models](https://cloud.google.com/vertex-ai/generative-ai/docs/model-garden/overview)
- **DeepSeek**: [API Documentation](https://platform.deepseek.com/api-docs) · [Model List](https://platform.deepseek.com/api-docs/api/list-models/)

Data may also be synchronized from [OpenRouter API](https://openrouter.ai/api/v1/models) which aggregates models from multiple providers.

## Contributing

Contributions are welcome! To add or update metadata for a model:

1. Fork the repository
2. Add or edit the appropriate JSON file in the data/ directory
3. Submit a pull request

Please ensure your JSON is valid and follows the schema outlined above. Prefer official provider documentation when updating model IDs, descriptions, or parameters.

Models are sorted with `*-latest` aliases first, then by release date (newest first). Run `python sort_models.py` after editing to maintain sort order.
