# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

FHE-agent-bench is a monorepo containing two AI agent benchmarking frameworks and an FHE challenge test bench:

- **MLAgentBench** - Evaluates AI agents on machine learning experimentation tasks (git submodule)
- **AIDE-FHE** - LLM-driven agent that solves FHE challenges via tree-search (git submodule)
- **fhe_challenge** - 20 FHE challenges from [FHERMA](https://fherma.io/challenges) for benchmarking

Each submodule has its own CLAUDE.md with detailed guidance.

## Repository Structure

```
FHE-agent-bench/
├── MLAgentBench/          # ML experimentation benchmark (git submodule)
├── AIDE-FHE/              # FHE challenge solver (git submodule)
└── fhe_challenge/         # FHE test bench (20 challenges)
    ├── black_box/         # Pre-encrypted challenges (3)
    └── white_box/         # Full implementation challenges (17)
        ├── openfhe/       # OpenFHE C++ (11)
        ├── ml_inference/  # ML model inference (4)
        └── non-OpenFHE/   # Other libraries (2)
```

## Quick Start

### MLAgentBench
```bash
cd MLAgentBench
pip install -e .
bash install.sh

# Run experiment
python -u -m MLAgentBench.runner --python $(which python) --task cifar10 --device 0 --log-dir logs --work-dir workspace --llm-name claude-3-5-sonnet-20241022

# Evaluate results
python -m MLAgentBench.eval --log-folder logs --task cifar10 --output-file results.json
```

### AIDE-FHE
```bash
cd AIDE-FHE
pip install -e .

# Run challenge
aide-fhe challenge_dir=/path/to/challenge
```

### FHE Challenge Test Bench

**Black Box** (pre-encrypted inputs):
```bash
cd fhe_challenge/black_box/challenge_relu
docker build -t relu .
docker run --rm -v $(pwd)/tests/testcase1:/data relu
```

**White Box** (full implementation):
```bash
cd fhe_challenge/white_box/openfhe/challenge_max
./verify.sh
```

Available challenges: relu, sigmoid, sign (black_box); array_sorting, gelu, invertible_matrix, knn, lookup_table, matrix_multiplication, max, parity, shl, softmax, svd (openfhe); cifar10, house_prediction, sentiment_analysis, svm (ml_inference); string_search, swift (non-OpenFHE)

## API Key Configuration

**MLAgentBench** - Place files in MLAgentBench root:
- `openai_api_key.txt` (format: `organization:APIkey`)
- `claude_api_key.txt`
- `crfm_api_key.txt`

**AIDE-FHE** - Environment variables:
- `OPENAI_API_KEY`
- `OPENROUTER_API_KEY`
- `OPENAI_BASE_URL` (optional, for local LLMs)

## Working with Submodules

```bash
# Initialize submodules after clone
git submodule update --init --recursive

# Update submodules to latest
git submodule update --remote
```
