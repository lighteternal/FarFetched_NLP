# Introduction

We provide instructions to reproduce Farfetched on a local Python 3.7.10 environment.
## Installation

The following non-Python dependencies are required: 

* Neo4J Community edition 4.3, available [here](https://neo4j.com/download-center/#community). You can also install Neo4J desktop to automatically handle DBMS and all the necessary plugins (e.g. APOC) installation. 

To install the Python requirements run:
```bash
pip install -r requirements.txt
```

## Usage

To crawl for news articles, a news-please daemon needs to be configured and executed as a shell command. Instructions [here](https://github.com/fhamborg/news-please).

You can then use the step-by-step process in the provided *Farfetched_step_by_step.ipynb* Jupyter notebook to:
* preprocess and add the processed article sections to the Neo4J KG
* apply wikification on the stored sections to link them with Wikidata entities 
* enter a claim (hypothesis) and discover its entities
* create a set of candidate evidence sets and evaluate them via the STS component of the Evidence Constructor
* Apply NLI on the claim-evidence pair to decide on the veracity of the initial claim.

To retrain the NLI and STS models, the user will need to download the sentence-transformers repo found [here](https://github.com/UKPLab/sentence-transformers) and read the instructions of the Application Examples section. 
We also provide individual notebooks: 
* for training and evaluating the Greek NLI model: *training_NLI_greek.ipynb*
* for training and evaluating the Greek STS model: *make_multilingual_greek_STS.ipynb*
* for evaluating FarFetched on the Greek FEVER dataset: *FEVER-GR_benchmark-Farfetched-desktop.ipynb*
Alternatively, the trained models can be downloaded and used directly in the *Farfetched_step_by_step.ipynb* Jupyter notebook.

## Model parameters
This section provides technical details regarding the trained NLI and STS model for the Greek language

### Trained NLI model hyperparameters
| _name_or_path                 | architectures.0                     | attention_probs_dropout_prob | bos_token_id | classifier_dropout | eos_token_id | gradient_checkpointing | hidden_act | hidden_dropout_prob | hidden_size | id2label.0    | id2label.1 | id2label.2 | initializer_range | intermediate_size | label2id.contradiction | label2id.entailment | label2id.neutral | layer_norm_eps | max_position_embeddings | model_type  | num_attention_heads | num_hidden_layers | output_past | pad_token_id | position_embedding_type | torch_dtype | transformers_version | type_vocab_size | use_cache | vocab_size |
| ----------------------------- | ----------------------------------- | ---------------------------- | ------------ | ------------------ | ------------ | ---------------------- | ---------- | ------------------- | ----------- | ------------- | ---------- | ---------- | ----------------- | ----------------- | ---------------------- | ------------------- | ---------------- | -------------- | ----------------------- | ----------- | ------------------- | ----------------- | ----------- | ------------ | ----------------------- | ----------- | -------------------- | --------------- | --------- | ---------- |
| lighteternal/nli-xlm-r-greek/ | XLMRobertaForSequenceClassification | 0.1                          | 0            |                    | 2            | false                  | gelu       | 0.1                 | 768         | contradiction | entailment | neutral    | 0.02              | 3072              | 0                      | 1                   | 2                | 0.00001        | 514                     | xlm-roberta | 12                  | 12                | true        | 1            | absolute                | float32     | 4.10.0               | 1               | true      | 250002     |
### Trained STS model hyperparameters
| _name_or_path    | architectures.0 | attention_probs_dropout_prob | bos_token_id | classifier_dropout | eos_token_id | gradient_checkpointing | hidden_act | hidden_dropout_prob | hidden_size | initializer_range | intermediate_size | layer_norm_eps | max_position_embeddings | model_type  | num_attention_heads | num_hidden_layers | output_past | pad_token_id | position_embedding_type | torch_dtype | transformers_version | type_vocab_size | use_cache | vocab_size |
| ---------------- | --------------- | ---------------------------- | ------------ | ------------------ | ------------ | ---------------------- | ---------- | ------------------- | ----------- | ----------------- | ----------------- | -------------- | ----------------------- | ----------- | ------------------- | ----------------- | ----------- | ------------ | ----------------------- | ----------- | -------------------- | --------------- | --------- | ---------- |
| xlm-roberta-base | XLMRobertaModel | 0.1                          | 0            |                    | 2            | false                  | gelu       | 0.1                 | 768         | 0.02              | 3072              | 0.00001        | 514                     | xlm-roberta | 12                  | 12                | true        | 1            | absolute                | float32     | 4.10.0               | 1               | true      | 250002     |

## Disclaimer
The crawled Greek articles used to showcase the functionalities of FarFetched cannot be shared publicly as no licence of copyright transfer is in place. However you can use FarFetched on your own set of monitored websites using news-please.

The trained NLI and STS models for the Greek language that were produced in the context of FarFetched can be downloaded via the *Farfetched_step_by_step.ipynb* notebook. The produced benchmark datasets are shared in the FarFetched_data folder. 


## License
[GPL 3.0](https://choosealicense.com/licenses/gpl-3.0/)
 
