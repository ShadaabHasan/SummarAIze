# SummarAIze

A simple tool that turns a long piece of text, such as part of a research paper, into a short summary.

It uses **BART** (`facebook/bart-large-cnn`), a pre-trained summarisation model from Hugging Face. You paste in a paragraph, and the tool returns a summary of 50–150 words.

## How it works

1. **Clean the text:** NLTK removes stop words and punctuation, and spaCy reduces words to their base form (lemmatisation).
2. **Summarise:** the cleaned text is passed to the BART summarisation pipeline from Hugging Face Transformers.
3. **Show the result:** the summary is printed below the input.

## Tech stack

- Python
- Hugging Face Transformers (BART, running on PyTorch)
- NLTK and spaCy for text cleaning

## How to run

1. Open `NLP_Mini_Project.ipynb` in Jupyter or Google Colab.
2. Run the first cell to install the packages:
   `transformers`, `torch`, `nltk`, `spacy`
3. Download the spaCy English model if needed:
   `python -m spacy download en_core_web_sm`
4. Run the second cell, then paste in the text you want to summarise.

## Limitations

- BART can only read about **1,024 tokens** at once. Longer text is cut off, so very long papers need to be split into parts first.
- The model is used **as it is**. It was not trained or fine-tuned in this project.
- Removing stop words before summarising can make the summaries less fluent, because BART was trained on normal sentences.
- There is no automatic quality score (such as ROUGE) yet.

## Ideas for the future

- Split long documents into chunks and summarise each part.
- Compare summaries with and without the text cleaning step, using ROUGE scores.
- Add a simple web interface.
