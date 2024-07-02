# Llama Natural Language Inference Experiments

This repository contains experiments on Natural Language Inference (NLI) using the Llama 3 model family. The experiments explore different approaches including zero-shot, one-shot, and fine-tuning with QLoRA.

## Dataset

The experiments use the Multi-NLI dataset (nyu-mll/multi_nli) from Hugging Face. This dataset is designed for natural language inference tasks, where the goal is to determine the relationship between a premise and a hypothesis. The possible relationships are:

- Entailment (0): The premise implies the hypothesis
- Neutral (1): The premise neither implies nor contradicts the hypothesis
- Contradiction (2): The premise contradicts the hypothesis

## Model

The base model used in these experiments is Meta-Llama-3-8B, an 8 billion parameter language model from the Llama 3 family. The model is loaded using 4-bit quantization for efficient memory usage.

## Experiments

### Zero-Shot (llama-zero-shot)

This script tests the model's zero-shot performance on the NLI task. Key points:

- Uses a carefully crafted prompt to explain the task
- Generates a single token prediction (0, 1, or 2)
- Evaluates on both matched and mismatched validation sets

### One-Shot (llama-one-shot)

This script explores one-shot learning for the NLI task. Key features:

- Searches for the best single example to include in the prompt
- Uses the same prediction mechanism as zero-shot
- Compares performance with zero-shot results

### QLoRA Fine-Tuning

Two approaches to QLoRA fine-tuning are explored:

#### Text Generation (llama-qlora-text)

- Fine-tunes the model to generate the label as text
- Uses SFTTrainer from the TRL library
- Applies LoRA to all linear layers

#### Classification Layer (llama-qlora-layer)

- Adds a classification layer on top of Llama's final hidden state
- Fine-tunes both the classification layer and Llama layers using LoRA
- Directly outputs logits for the three classes

## Results

| Approach | Accuracy |
|----------|----------|
| Zero-Shot | 64.22% |
| One-Shot | 62.03% |
| QLoRA (Text) | 88.44% |
| QLoRA (Layer) | 88.29% |

## Key Findings

- QLoRA fine-tuning significantly outperforms zero-shot and one-shot approaches, with both QLoRA methods achieving accuracy close to 88%.
- Interestingly, the one-shot approach performed slightly worse than zero-shot. This suggests that for this particular task and model, a single example may not provide enough additional context to improve performance.
- The text generation approach in QLoRA fine-tuning slightly outperformed the classification layer approach, though the difference is minimal (0.15%).
- The zero-shot performance of 64.22% indicates that the model has some inherent understanding of the NLI task, performing well above random chance (33.33% for a 3-class problem).
- The high performance of fine-tuned models (>88% accuracy) demonstrates the effectiveness of QLoRA for adapting large language models to specific tasks with relatively little training data.
