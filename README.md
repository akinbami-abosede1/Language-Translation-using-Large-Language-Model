# Language Translation Using a Large Model

This project demonstrates a language translation model pipeline using a pretrained Transformer model from the Hugging Face library. The goal is to translate English sentences into French.

## Data Collection and Preparation

The project begins by loading a dataset of English and French sentences. A sample of **5,000 sentence pairs** is taken from the original dataset, which contains over **175,000 pairs**. A fixed `random_state` is used to ensure the sampling is reproducible.

- **Original Data Size:** (175,621, 2)  
- **Sampled Data Size:** (5,000, 2)  

## Data Preprocessing

The text data was preprocessed to clean and standardize it before it's used to train the model. The following steps are performed on both English and French sentences:

- **Unicode Normalization:** Normalizes the text to a standard form, which is important for handling special characters and accents.  
- **Punctuation Removal:** All punctuation is removed from the text.  
- **Lowercasing:** All characters are converted to lowercase.  
- **Renaming Columns:** The DataFrame columns are renamed for clarity to `english_words` and `french_words`.  

This preprocessing ensures that the model receives clean, consistent data, which helps improve its performance.

## Model Loading and Tokenization

A pretrained Transformer model is used for the translation task. This approach is highly efficient as it leverages a model that has already learned the complexities of language.

- **Model:** `Helsinki-NLP/opus-mt-en-fr`  
- **Tokenizer:** `AutoTokenizer.from_pretrained(...)`  
- **Model Loader:** `TFAutoModelForSeq2SeqLM.from_pretrained(...)`  

The data is split into training and testing sets, with **10% of the data reserved for testing**. The training and testing sentences are then tokenized, converting them into numerical representations that the model can process. A maximum length of **64 tokens** is set for each sentence.


## Model Training

The model is compiled and trained on the preprocessed dataset.

- **Optimizer:** Adam-based optimizer with a learning rate of `5e-5`  
- **Epochs:** 3  

The training process involves the model learning to map the tokenized English inputs to the corresponding tokenized French labels. The loss decreases with each epoch, indicating that the model is learning effectively.

- **Epoch 1 Loss:** 0.7946  
- **Epoch 2 Loss:** 0.4474  
- **Epoch 3 Loss:** 0.3265  

## Evaluation and Prediction

After training, the model's performance was tested with the test dataset and it was evaluated using the **BLEU score**,  a metric commonly used for evaluating machine translation quality. A higher BLEU score indicates better translation.

- **BLEU Score on Test Set:** 75.67%  

The project concludes with a demonstration of the model's ability to translate new, unseen English sentences into French:

- `"Good morning, how are you?"` → `"Bonjour, comment allezvous ?"`  
- `"can you give me your rice?"` → `"pouvezvous me donner votre riz ?"`  
