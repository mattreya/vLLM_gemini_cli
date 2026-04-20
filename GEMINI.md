# Gemini Instructions for vLLM

This project uses `uv` for environment management. Follow the guidelines in [AGENTS.md](AGENTS.md) for detailed contribution policies.

## Environment Setup
```bash
# Install `uv` if you don't have it:
curl -LsSf https://astral.sh/uv/install.sh | sh

# Always use `uv` for Python environment management:
uv venv --python 3.12
source .venv/bin/activate

# Install linting tools and pre-commit hooks:
uv pip install -r requirements/lint.txt
pre-commit install
```

## Build Commands
```bash
# Python changes only (faster):
VLLM_USE_PRECOMPILED=1 uv pip install -e . --torch-backend=auto

# Python and C/C++ changes:
uv pip install -e . --torch-backend=auto
```

## Test Commands
```bash
# Install test dependencies:
uv pip install -r requirements/test/cuda.in

# Run a specific test file:
.venv/bin/python -m pytest tests/path/to/test_file.py -v
```

## Linting Commands
```bash
# Run all pre-commit hooks on staged files:
pre-commit run

# Run on all files:
pre-commit run --all-files

# Run a specific hook:
pre-commit run ruff-check --all-files

# Run mypy as in CI:
pre-commit run mypy-3.10 --all-files --hook-stage manual
```

## Commit Messages
Add attribution using the `Co-authored-by:` trailer:
```text
Your commit message here

Co-authored-by: gemini-cli
Signed-off-by: Your Name <your.email@example.com>
```
