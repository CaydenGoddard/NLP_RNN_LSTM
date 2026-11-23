# NLP_RNN_LSTM - RNN vs LSTM Next Word Prediction

## Overview
This project builds two sequence models, a **SimpleRNN** and an **LSTM**, and compares how well they predict the next word in a sentence. Both models are trained on the same small dataset with the same settings so the comparison is fair.

## Files
| File | Description |
|---|---|
| `main.py` | Prepares the data, builds and trains both models, and prints their predictions |
| `data.py` | The training sentences |
| `requirements.txt` | Required Python libraries |

## Setup
Install the dependencies:

```bash
pip install -r requirements.txt
```

Run the program:

```bash
python main.py
```

## How It Works
1. **Preprocessing** - The text is tokenized, each word is converted to an integer, and the text is split into input sequences of 3 words with the next word as the target.
   - Example: `the dog ran` -> `across`
2. **Models** - Both models use the same structure:
   - Embedding layer (10 dimensions)
   - SimpleRNN **or** LSTM layer (32 units)
   - Dense output layer with softmax over the vocabulary
3. **Training** - Both models train for 150 epochs with categorical cross-entropy loss and the Adam optimizer.
4. **Predictions** - Both models predict the next word for the same set of prompts.

## Results
| Model | Training Accuracy |
|---|---|
| SimpleRNN | 0.7925 |
| LSTM | 0.5472 |

| Prompt | SimpleRNN | LSTM |
|---|---|---|
| the dog ran | across | across |
| the cat sat | on | the |
| the dog chased | the | the |
| the boy threw | the | the |
| the girl ran | across | across |
| the bird flew | in | the |

## Findings
- The **SimpleRNN** had higher accuracy and more sensible predictions on this small dataset with short 3-word inputs.
- The **LSTM** was undertrained at 150 epochs and often predicted "the", the most common word. It has more parameters, so it needs more training; with more epochs it caught up.
- The SimpleRNN failed on "the bird flew", predicting "in" instead of "over".
- LSTMs usually perform better on **longer** sequences because their gates and cell state help them remember earlier words and avoid the vanishing gradient problem that limits SimpleRNNs.

## Requirements
- Python 3
- TensorFlow
- NumPy
