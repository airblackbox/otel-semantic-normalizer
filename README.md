# genai-semantic-normalizer

[![CI](https://github.com/airblackbox/otel-semantic-normalizer/actions/workflows/ci.yml/badge.svg)](https://github.com/airblackbox/otel-semantic-normalizer/actions/workflows/ci.yml)
[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://github.com/airblackbox/otel-semantic-normalizer/blob/main/LICENSE)
[![Go](https://img.shields.io/badge/Go-1.22+-00ADD8.svg?logo=go&logoColor=white)](https://golang.org)


An OpenTelemetry Collector processor that normalizes vendor-specific LLM attributes to the standard `gen_ai.*` semantic conventions.

## What It Does

LLM providers use different attribute names for the same concepts. This processor maps them all to the [OpenTelemetry GenAI semantic conventions](https://opentelemetry.io/docs/specs/semconv/gen-ai/):

| Vendor Attribute | Normalized To |
|---|---|
| `openai.model` | `gen_ai.request.model` |
| `anthropic.input_tokens` | `gen_ai.usage.input_tokens` |
| `cohere.model_id` | `gen_ai.request.model` |
| `llm.model` | `gen_ai.request.model` |

Supports: OpenAI, Anthropic, Cohere, Azure OpenAI, Google/Vertex AI, and generic `llm.*` attributes.

## Configuration

```yaml
processors:
  genai_semantic_normalizer:
    enable_defaults: true     # Use built-in vendor mappings
    overwrite: false          # Don't overwrite existing gen_ai.* attrs
    drop_original: false      # Keep vendor-specific attrs after normalization
    custom_mappings:          # Add your own mappings
      my_vendor.model: gen_ai.request.model
```

## Part of the AIR Platform

This processor is one component of the [AIR Blackbox Gateway](https://github.com/airblackbox/gateway) collector pipeline.

## License

Apache-2.0