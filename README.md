# Bachelor Thesis: An Evaluation of Automatic Interlinear Glossing Models for Low-Resource Languages

Here I will provide all modifications done for each model I utilized for the evaluation. Abbreviations of models used are introduced in the thesis. Datasets for Savosavo and Yali are provided in the folder dataset.

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

### doubletrained
Simply double the corresponding training dataset and train the baseline model

### morfM, morfS, morfOS
use code in morfessor.ipynb to generate morphological segmentation. For morfM, take the output file and train the baseline model with it. For morfS, use the method provided in morfessor.ipynb to generate training data. For morfOS, simply combine original training data and morfS training data.

## TÜ-CL
clone the cde on this page: https://github.com/LGirrbach/sigmorphon-2023-glossing

in main.py, add import:
```python
from pytorch_lightning.utilities.seed import seed_everything
```
then, in the same file, after the line:

```python
if __name__ == "__main__":
```
add:
```python
seed_everything(21, workers=True)
```
change test_file to real test dataset instead of dev dataset. Use parameters provided in best_hyperparameters.json for training. There are no pamaters provided for Savosavo and Yali.

To train ctc and morph on Savosavo and Yali, simply add language code mappings in all files. For Savosavo: "Savosavo" : "savo"; for Yali: "Yali" : "apah".

