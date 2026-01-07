# Yelp Review Star Rating Classifier

A sentiment analysis project that classifies Yelp reviews into 1-5 star ratings using Large Language Models (LLMs) via the Groq API. This project evaluates three prompting strategies: **Basic (Zero-Shot)**, **Chain-of-Thought (CoT)**, and **Few-Shot**.

## Overview

This project implements a robust, high-throughput evaluation pipeline for LLM-based sentiment classification. It uses the `meta-llama/llama-4-maverick-17b-128e-instruct` model to predict star ratings from review text.

### Key Features

- **Multi-key API rotation** for maximizing throughput (~120 RPM)
- **Parallel processing** with ThreadPoolExecutor
- **Structured output validation** using Pydantic models
- **Three prompting strategies** for comparison
- **Automatic retry logic** for handling rate limits

## Project Structure

```
dnyf-assignment-1/
├── simple_evaluation.py    # Main evaluation script
├── main.py                 # Entry point
├── prompts/                # Prompt templates
│   ├── basic.md            # Zero-shot prompt
│   ├── chain_of_thought.md # CoT prompt
│   └── few_shot.md         # Few-shot prompt
├── notebooks/              # Jupyter notebooks for experimentation
├── task1_summary.md        # Detailed task summary and results
├── pyproject.toml          # Project dependencies
└── .env                    # API keys (not tracked)
```

## Installation

### Prerequisites

- Python 3.13+
- [uv](https://github.com/astral-sh/uv) package manager (recommended)

### Setup

1. Clone the repository:
   ```bash
   git clone <repository-url>
   cd dnyf-assignment-1
   ```

2. Install dependencies:
   ```bash
   uv sync
   ```

3. Configure environment variables:
   ```bash
   cp .example.env .env
   ```
   
   Add your Groq API key(s) to `.env`:
   ```
   GROQ_API_KEY=your_api_key_here
   # Optional: Add multiple keys for higher throughput
   GROQ_API_KEY_2=your_second_key
   GROQ_API_KEY_3=your_third_key
   ```

4. Set up Kaggle credentials for dataset access (required by `kagglehub`).

## Usage
Run the code blocks present in the jupyter notebook present in `notebooks` folder

This will:
1. Download the Yelp reviews dataset from Kaggle
2. Sample reviews for evaluation
3. Run all three prompting strategies in parallel
4. Output accuracy and validity metrics
5. Save results to `evaluation_results_simple.csv`

## Prompting Strategies

| Strategy | Description |
|----------|-------------|
| **Basic** | Zero-shot classification with minimal instructions |
| **Chain-of-Thought** | Forces step-by-step reasoning before prediction |
| **Few-Shot** | Provides 3 example reviews with ratings as anchors |

## Results

Evaluation on 201 reviews:

| Strategy | Accuracy | Validity Rate |
|----------|----------|---------------|
| Basic    | 59.0%    | 100.0%        |
| CoT      | 60.5%    | 100.0%        |
| Few-Shot | 60.0%    | 100.0%        |

**Key Findings:**
- CoT performed best, suggesting that requiring explanations improves alignment with ground truth
- All strategies achieved 100% validity rate (proper JSON output)
- The underlying model shows strong baseline sentiment analysis capability

## Dependencies

- `openai` - API client for Groq
- `pydantic` - Data validation and structured outputs
- `kagglehub` - Dataset downloading
- `pandas` - Data manipulation
- `scikit-learn` - Accuracy metrics
- `tabulate` - Results formatting
- `python-dotenv` - Environment variable management

