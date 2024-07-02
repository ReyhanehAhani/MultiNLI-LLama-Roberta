# RoBERTa Fine-Tuning for MultiNLI

This repository demonstrates two approaches to fine-tune RoBERTa-large models on the MultiNLI dataset for natural language inference tasks.

## Notebooks

1. `roberta_lora`: Fine-tuning using Low-Rank Adaptation (LoRA)
2. `roberta_normal`: Standard fine-tuning

## Dataset

- **MultiNLI**: A crowd-sourced collection of 433k sentence pairs annotated with textual entailment information.
- We use a 25% subset of the training data to reduce computational requirements.

## Model

- Base model: RoBERTa-large from FacebookAI
- Fine-tuned for sequence classification with 3 labels (entailment, contradiction, neutral)

## Key Features

- LoRA implementation using PEFT library for parameter-efficient fine-tuning
- Comparison between LoRA and standard fine-tuning approaches
- Evaluation on both matched and mismatched validation sets

## Training Process

1. Load and preprocess the MultiNLI dataset
2. Initialize RoBERTa-large model and tokenizer
3. Apply LoRA (in `roberta_lora`) or prepare for standard fine-tuning
4. Train for 1 epoch with specified hyperparameters
5. Evaluate on validation sets
