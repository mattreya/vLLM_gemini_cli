# Gemini CLI

[Gemini CLI](https://github.com/google-gemini/gemini-cli) is a powerful, interactive command-line interface designed for software engineering tasks. It uses Google's Gemini models to provide intelligent code generation, refactoring, and project analysis directly from your terminal.

By pointing Gemini CLI at a vLLM server, you can use high-performance open-weight models as the inference engine while maintaining the feature-rich agentic capabilities of Gemini CLI.

## How It Works

vLLM provides an OpenAI-compatible API that Gemini CLI can utilize. By configuring the API base URL and model name, Gemini CLI can send its requests to a local or remote vLLM instance instead of the default Google APIs. This is ideal for private development or for using models like **Gemma 2** at scale.

## Requirements

Gemini CLI performs best with models that have strong tool-calling and reasoning capabilities. We recommend using `google/gemma-2-9b-it` or `google/gemma-2-27b-it` for the best local experience.

## Installation

Install Gemini CLI using the recommended method for your platform:

```bash
npm install -g @google/gemini-cli
```

## Starting the vLLM Server

Start vLLM with a compatible model (e.g., Gemma 2 9B):

```bash
vllm serve google/gemma-2-9b-it --served-model-name gemini-compatible-model
```

Ensure the model is exposed via the OpenAI-compatible API (default on port 8000).

## Configuring Gemini CLI

Configure Gemini CLI to use your vLLM server by setting the appropriate environment variables or updating your configuration file:

```bash
GEMINI_API_BASE=http://localhost:8000/v1 \
GEMINI_API_KEY=dummy \
GEMINI_MODEL=gemini-compatible-model \
gemini
```

| Variable          | Description                                                           |
| ----------------- | --------------------------------------------------------------------- |
| `GEMINI_API_BASE` | Points to your vLLM's OpenAI-compatible endpoint (usually `/v1`)      |
| `GEMINI_API_KEY`  | Can be any value if your vLLM server does not require authentication  |
| `GEMINI_MODEL`    | The name of the model as specified in `--served-model-name`           |

## Testing the Setup

Once Gemini CLI is connected, try a simple refactoring command to verify:

```bash
gemini "Refactor this file to use async/await"
```

If the agent successfully analyzes the codebase and proposes changes using your local model, the integration is complete.

## Troubleshooting

- **Connection Error**: Verify that vLLM is running and the `GEMINI_API_BASE` includes the `/v1` suffix if required by the client.
- **Incompatible Output**: Ensure your vLLM version is up to date and you are using a model with sufficient instruction-following capabilities for agentic tasks.
