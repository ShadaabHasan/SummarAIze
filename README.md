# SummarAIze

A simple tool that turns a long piece of text, such as part of a research paper, into a short summary.

It uses **BART** (`facebook/bart-large-cnn`), a pre-trained summarisation model from Hugging Face. You paste in a paragraph, and the tool returns a summary of 50–150 tokens.

## How it works

1. **Tokenise:** the text is turned into tokens with BART's tokenizer. Text longer than BART's limit (1,024 tokens) is cut to fit.
2. **Generate:** BART writes the summary using beam search (4 beams), which compares several possible summaries and keeps the best one.
3. **Decode:** the summary tokens are turned back into text and printed.

The model is loaded directly with `AutoModelForSeq2SeqLM`, instead of the `summarization` pipeline, which was removed in Transformers version 5.

### A design choice

An earlier version removed stop words and lemmatised the text before summarising. This was removed, because BART was trained on normal sentences and writes better summaries from them. Removing words like "not" could also change the meaning of the text.

## Tech stack

- Python
- Hugging Face Transformers (BART)
- PyTorch

## How to run

1. Open `NLP_Mini_Project.ipynb` in Google Colab (a GPU runtime is faster, but not required).
2. Run the first cell to install the packages.
3. Run the second cell, then paste in the text you want to summarise.

## Limitations

- BART can only read about **1,024 tokens** at once. Longer text is cut off, so only the start of a long paper is summarised.
- The model is used **as it is**. It was not trained or fine-tuned in this project.
- There is no automatic quality score (such as ROUGE) yet.

## Ideas for the future

- Split long documents into chunks, summarise each part, then combine them.
- Measure summary quality with ROUGE scores.
- Add a simple web interface.
