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

### Step-by-step Instructions for Deploying Option 2

#### 1. Install the Databricks CLI

Install and configure the Databricks CLI on your machine following the [guide](https://docs.databricks.com/dev-tools/cli/databricks-cli.html)

#### 2. Set up Authentication for Asset Bundles

Follow the [guidance](https://docs.databricks.com/aws/en/dev-tools/bundles/authentication) on how to set this up. It is recommended to use [attended authentication](https://docs.databricks.com/aws/en/dev-tools/bundles/authentication#attended-authentication) for secure and seamless access. This will also configure your host workspace, as this is not explicitly set in the bundle settings.

#### 3. (Optional) Amend Default Values

The below default values are set for running the job:

* Target Catalog name: `main`
* Target Schema name: `ray_multi_model_inference`
* Transcription model Huggingface ID: `openai/whisper-medium`
* LLM Huggingface ID: `microsoft/phi-4`

If you want to change any of these, this can be done by editing the variables near the top of `databricks.yml`. For alternative ways of setting variables, please see the [documentation](https://docs.databricks.com/aws/en/dev-tools/bundles/variables#set-a-variables-value).

#### 4. Validate the Bundle

To ensure everything is correct, validate the bundle with

```bash
databricks bundle validate [-p <your-auth-profile>]
```

(with optional inline profile-based authentication with `-p` indicated).

#### 5. Deploy the Job

Create the job in your authenticated Databricks workspace with

```bash
databricks bundle deploy [-p <your-auth-profile>]
```

#### 6. Run the Job

You can now navigate to the Workflows section in your workspace and find the job created with the name _Ray Multi-Model Inference Bundle_ (unless changed).

You can run the job now, which you can expect to take between 1-2 hours if the sample data needs to be unzipped, or the models need to be downloaded, or 15-20 minutes without.

_NB these will take different times if you use different models or source data._

## Additional Resources

- [Getting Started with Databricks Asset Bundles](https://docs.databricks.com/dev-tools/bundles/index.html)
- [Databricks Workspace Setup](https://docs.databricks.com/workspace/workspace-details.html)


