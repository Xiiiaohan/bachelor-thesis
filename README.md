# Bachelor Thesis: An Evaluation of Automatic Interlinear Glossing Models for Low-Resource Languages

Here I will provide all modifications done for each model I utilized for the evaluation. Abbreviations of models used are introduced in the thesis. Datasets for Savosavo and Yali are provided in the folder dataset.

## Baseline model from the SIGMORPHON Shared Task

### selftrained
clone model on this page: https://github.com/sigmorphon/2023glossingST

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
clone model on this page: https://github.com/LGirrbach/sigmorphon-2023-glossing

in main.py, add import:
```python
from pytorch_lightning.utilities.seed import seed_everything
```
then, in the same file, after the line:

```python
if __name__ == "__main__":
```
add seed = 21:
```python
seed_everything(21, workers=True)
```
In the following cases, different seeds are used during training:

Gitksan: ctc open: 61, 5, 58; ctc close: 11, 59, 42    morph open: 59, 58, 8; morph close: 67, 42, 5

Lezgi: ctc close: 42, 67, 16    morph close: 16, 42, 5

Savosavo: ctc open: 1    ctc close: 9

change test_file to real test dataset instead of dev dataset. Use parameters provided in best_hyperparameters.json for training. There are no pamaters provided for Savosavo and Yali.

To train ctc and morph on Savosavo and Yali, simply add language code mappings in main.py, predict_from_gloss.py, experiment.py. 
```python
# mapping for Savosavo
"Savosavo" : "savo"
# mapping for Yali
"Yali" : "apah"
```

## GlossLM
clone model on this page: https://github.com/lecs-lab/polygloss

retrieve method cloned on this page: https://github.com/michaelpginn/igt-icl.git

change for retreive method: 

in the igt.py file, add 'morpheme: Optional[str]' as attribute.

use code in glossLM.ipynb to generate prediction.

## CRF
clone the model on this page: https://github.com/shuokabe/crf_glossing.git

for the open track, simply use the model as it is. For closed track, see the folder crf

the pipeline used for training is provided in crf.ipynb

