# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

FHE-agent-bench is a monorepo containing two AI agent benchmarking frameworks as git submodules:

- **MLAgentBench** - Evaluates AI agents on machine learning experimentation tasks (model development, hyperparameter tuning, etc.)
- **AIDE-FHE** - LLM-driven agent that solves Fully Homomorphic Encryption challenges via tree-search

Each submodule has its own CLAUDE.md with detailed guidance. Refer to those when working within a specific project.

## Repository Structure

```
FHE-agent-bench/
├── MLAgentBench/          # ML experimentation benchmark (git submodule)
│   ├── MLAgentBench/      # Core package
│   ├── agents/            # Agent implementations
│   └── benchmarks/        # Task datasets
└── AIDE-FHE/              # FHE challenge solver (git submodule)
    ├── aide/              # Core package
    └── challenges/        # FHE challenges
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
