# Ray Multi-Model Inference on Databricks

## Overview

This repository demonstrates how to perform efficient multi-model inference on audio files using Ray within the Databricks environment. The workflow implements three sequential model operations:

1. Audio transcription
2. PII (Personally Identifiable Information) redaction
3. Zero-shot classification using LLM

## Purpose

The project showcases how to orchestrate multiple AI models for audio processing at scale using Ray's distributed computing capabilities on Databricks. It provides both a single-notebook solution and a production-ready workflow using Databricks Jobs.

## Getting Started

### Prerequisites

- Access to a Databricks workspace
- [Databricks CLI](https://docs.databricks.com/dev-tools/cli/databricks-cli.html) installed
- [Databricks Asset Bundles](https://docs.databricks.com/dev-tools/bundles/index.html) configured


### Usage Options

#### Option 1: Single Notebook Workflow

Use `end_to_end_notebook.ipynb` for a comprehensive workflow that:

- Downloads [LJSpeech](https://paperswithcode.com/dataset/ljspeech) sample data
- Sets up required models ([whisper-medium](https://huggingface.co/openai/whisper-medium) and [phi-4](https://huggingface.co/microsoft/phi-4))
- Executes the complete inference pipeline with [Ray on Databricks](https://docs.databricks.com/aws/en/machine-learning/ray)

#### Option 2: Production Workflow

The `job_notebooks` directory contains a structured Databricks job that:

- Intelligently checks for existing resources before downloading
- Utilizes serverless compute for lightweight tasks
- Can be deployed using Databricks Asset Bundles
- Supports parameterization for:
    - Target catalogs
    - Schemas
    - Model selection


### Deployment with Databricks Asset Bundles

1. Ensure your Databricks CLI is configured
2. Navigate to the repository root
3. Deploy using Asset Bundles commands

```bash
databricks bundle deploy
```


## Additional Resources

- [Databricks CLI Installation Guide](https://docs.databricks.com/dev-tools/cli/databricks-cli.html)
- [Getting Started with Databricks Asset Bundles](https://docs.databricks.com/dev-tools/bundles/index.html)
- [Databricks Workspace Setup](https://docs.databricks.com/workspace/workspace-details.html)


## License

[Include license information if available]

<div style="text-align: center">⁂</div>

[^1]: https://github.com/marcell-ferencz-databricks/ray-multi-model-inference

