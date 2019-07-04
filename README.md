## Entity Tagger
- The goal of this tool is to **recognise the entity in a query sentence**
- This tool uses an implementation of a Named Entity Recognizer that obtains state-of-the-art performance in NER on the 4 CoNLL datasets (English, Spanish, German and Dutch) without resorting to any language-specific knowledge or resources such as gazetteers. Details about the model can be found at: http://arxiv.org/abs/1603.01360

### Task:
  - To identify the searching intention according to the query sentence typed by users in academic search engine.
  - The entities has five main categories: **PERSON**, **ORGANIZATION**, **CONFERENCE**, **LOCATION** and  **KEYWORD**.

    Example | Category 
    -----------|-----------
    J. S. Clark | PERSON 
    Institute of Process and Plant Technology | ORGANIZATION
    ICDM | CONFERENCE
    Medina | LOCATION
    relational model | KEYWORD
  
### Data:
  - Input: **Tokenized words in a query **
  - Output: **Tags**
  - One Example:

    Tokenized words in a query   | Tags 
    -----------|-----------
    J. | B-PER 
    S. | I-PER 
    Clark | I-PER
    publications | O 
    done | O
    by | O
    Centre | B-ORG
    Urbain | I-ORG
    Nord | I-ORG
    B | I-ORG
    wrtten | O
    at | O
    1917 | B-DATE

## Initial setup

To use the tagger, you need Python 2.7, with Numpy and Theano installed.


## Train a model

To train your own model, you need to use the train.py script and provide the location of the training, development and testing set:

```
python train.py --train dataset/train --dev dataset/dev --test dataset/test
```

The training script will automatically store the best model in ./models/ as the training goes on.
There are many parameters you can tune (CRF, dropout rate, embedding dimension, LSTM hidden layer size, etc). To see all parameters, simply run:

```
python train.py --help
```

Input training files for the training script have to follow the same format than the CoNLL2003 sharing task: each word has to be on a separate line, and there must be an empty line after each sentence. A line must contain at least 2 columns, the first one being the word itself, the last one being the named entity. It does not matter if there are extra columns that contain tags or chunks in between. Tags have to be given in the IOB format (it can be IOB1 or IOB2).

## Tag Query Sentence 

```
python tagger.py --model models/english/ --input input.txt --output output.txt
```

The input file should contain one sentence by line, and they have to be tokenized. Otherwise, the tagger will perform poorly.


