# Bachelor Thesis: An Evaluation of Automatic Interlinear Glossing Models for Low-Resource Languages

Here I will provide all modifications done for each model I utilized for the evaluation. Abbreviations of models used are introduced in the thesis.

## Baseline model from the SIGMORPHON Shared Task

### selftrained
clone the code on this page: https://github.com/sigmorphon/2023glossingST

on top of the token_class_model.py file, add:

```python
from transformers import set_seed
```

in TrainingArguments, add:

```python
seed=21
```

and in main(), add:

```python
set_seed(21)
```

### doubletrained, morfM, morfS, morfOS

