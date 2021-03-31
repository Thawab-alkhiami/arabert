# AraBERTv2 / AraGPT2 / AraELECTRA

<img src="https://github.com/aub-mind/arabert/blob/master/arabert_logo.png" width="100" align="right"/>

This repository now contains code and implementation for:
- **AraBERT v0.1/v1**: Original
- **AraBERT v0.2/v2**: Base and large versions with better vocabulary, more data, more training [Read More...](#AraBERT)
- **AraGPT2**: base, medium, large and MEGA. Trained from scratch on Arabic [Read More...](#AraGPT2)
- **AraELECTRA**: Trained from scratch on Arabic [Read More...](#AraELECTRA)

If you want to clone the old repository:
```bash
git clone https://github.com/aub-mind/arabert/
cd arabert && git checkout 6a58ca118911ef311cbe8cdcdcc1d03601123291
```
# AraBERTv2

## What's New!

AraBERT now comes in 4 new variants to replace the old v1 versions:

More Detail in the AraBERT folder and in the [README](https://github.com/aub-mind/arabert/tree/master/arabert) and in the [AraBERT Paper](https://arxiv.org/abs/2003.00104)

 Model | HuggingFace Model Name | Size (MB/Params)| Pre-Segmentation | DataSet (Sentences/Size/nWords) |
 ---|:---:|:---:|:---:|:---:
AraBERTv0.2-base | [bert-base-arabertv02](https://huggingface.co/aubmindlab/bert-base-arabertv02) | 543MB / 136M | No | 200M / 77GB / 8.6B |
 AraBERTv0.2-large| [bert-large-arabertv02](https://huggingface.co/aubmindlab/bert-large-arabertv02) | 1.38G / 371M | No | 200M / 77GB / 8.6B |
AraBERTv2-base| [bert-base-arabertv2](https://huggingface.co/aubmindlab/bert-base-arabertv2) | 543MB / 136M | Yes | 200M / 77GB / 8.6B |
AraBERTv2-large| [bert-large-arabertv2](https://huggingface.co/aubmindlab/bert-large-arabertv2) | 1.38G / 371M | Yes | 200M / 77GB / 8.6B |
 AraBERTv0.1-base| [bert-base-arabertv01](https://huggingface.co/aubmindlab/bert-base-arabertv01) | 543MB / 136M | No | 77M / 23GB / 2.7B |
AraBERTv1-base| [bert-base-arabert](https://huggingface.co/aubmindlab/bert-base-arabert) | 543MB / 136M | Yes | 77M / 23GB / 2.7B |

All models are available in the `HuggingFace` model page under the [aubmindlab](https://huggingface.co/aubmindlab/) name. Checkpoints are available in PyTorch, TF2 and TF1 formats.

## Better Pre-Processing and New Vocab

We identified an issue with AraBERTv1's wordpiece vocabulary. The issue came from punctuations and numbers that were still attached to words when learned the wordpiece vocab. We now insert a space between numbers and characters and around punctuation characters.

The new vocabulary was learnt using the `BertWordpieceTokenizer` from the `tokenizers` library, and should now support the Fast tokenizer implementation from the `transformers` library.

**P.S.**: All the old BERT codes should work with the new BERT, just change the model name and check the new preprocessing function

**Please read the section on how to use the [preprocessing function](#Preprocessing)**

## Bigger Dataset and More Compute

We used ~3.5 times more data, and trained for longer.
For Dataset Sources see the [Dataset Section](#Dataset)

Model | Hardware | num of examples with seq len (128 / 512) |128 (Batch Size/ Num of Steps) | 512 (Batch Size/ Num of Steps) | Total Steps | Total Time (in Days) |
 ---|:---:|:---:|:---:|:---:|:---:|:---:
AraBERTv0.2-base | TPUv3-8 | 420M / 207M | 2560 / 1M | 384/ 2M | 3M | 36
AraBERTv0.2-large | TPUv3-128 | 420M / 207M | 13440 / 250K | 2056 / 300K | 550K | 7
AraBERTv2-base | TPUv3-8 | 420M / 207M | 2560 / 1M | 384/ 2M | 3M | 36
AraBERTv2-large | TPUv3-128 | 520M / 245M | 13440 / 250K | 2056 / 300K | 550K | 7
AraBERT-base (v1/v0.1) | TPUv2-8 | - |512 / 900K | 128 / 300K| 1.2M | 4

# AraGPT2

More details and code are available in the AraGPT2 folder and [README](https://github.com/aub-mind/arabert/blob/master/aragpt2/README.md)

## Model

 Model | HuggingFace Model Name | Size / Params|
 ---|:---:|:---:
 AraGPT2-base | [aragpt2-base](https://huggingface.co/aubmindlab/aragpt2-base) | 527MB/135M |
 AraGPT2-medium | [aragpt2-medium](https://huggingface.co/aubmindlab/aragpt2-medium) |  1.38G/370M  |
 AraGPT2-large | [aragpt2-large](https://huggingface.co/aubmindlab/aragpt2-large) |  2.98GB/792M  |
 AraGPT2-mega | [aragpt2-mega](https://huggingface.co/aubmindlab/aragpt2-mega) |  5.5GB/1.46B  |
 AraGPT2-mega-detector-long | [aragpt2-mega-detector-long](https://huggingface.co/aubmindlab/aragpt2-mega-detector-long) | 516MB/135M |

All models are available in the `HuggingFace` model page under the [aubmindlab](https://huggingface.co/aubmindlab/) name. Checkpoints are available in PyTorch, TF2 and TF1 formats.

## Dataset and Compute

For Dataset Source see the [Dataset Section](#Dataset)

Model | Hardware | num of examples (seq len = 1024) | Batch Size | Num of Steps | Time (in days)
 ---|:---:|:---:|:---:|:---:|:---:
AraGPT2-base | TPUv3-128 | 9.7M | 1792 | 125K | 1.5
AraGPT2-medium | TPUv3-128 | 9.7M | 1152 | 85K | 1.5
AraGPT2-large | TPUv3-128 | 9.7M | 256 | 220k | 3
AraGPT2-mega | TPUv3-128 | 9.7M | 256 | 800K | 9

# AraELECTRA

More details and code are available in the AraELECTRA folder and [README](https://github.com/aub-mind/arabert/blob/master/araelectra/README.md)

## Model

Model | HuggingFace Model Name | Size (MB/Params)|
 ---|:---:|:---:
AraELECTRA-base-generator | [araelectra-base-generator](https://huggingface.co/aubmindlab/araelectra-base-generator) |  227MB/60M  |
AraELECTRA-base-discriminator | [araelectra-base-discriminator](https://huggingface.co/aubmindlab/araelectra-base-discriminator) |  516MB/135M  |

## Dataset and Compute
Model | Hardware | num of examples (seq len = 512) | Batch Size | Num of Steps | Time (in days)
 ---|:---:|:---:|:---:|:---:|:---:
ELECTRA-base | TPUv3-8 | - | 256 | 2M | 24

# Dataset

The pretraining data used for the new AraBERT model is also used for **AraGPT2 and AraELECTRA**.

The dataset consists of 77GB or 200,095,961 lines or 8,655,948,860 words or 82,232,988,358 chars (before applying Farasa Segmentation)

For the new dataset we added the unshuffled OSCAR corpus, after we thoroughly filter it, to the previous dataset used in AraBERTv1 but with out the websites that we previously crawled:
- OSCAR unshuffled and filtered.
- [Arabic Wikipedia dump](https://archive.org/details/arwiki-20190201) from 2020/09/01
- [The 1.5B words Arabic Corpus](https://www.semanticscholar.org/paper/1.5-billion-words-Arabic-Corpus-El-Khair/f3eeef4afb81223df96575adadf808fe7fe440b4)
- [The OSIAN Corpus](https://www.aclweb.org/anthology/W19-4619)
- Assafir news articles. Huge thank you for Assafir for the data

# Preprocessing

It is recommended to apply our preprocessing function before training/testing on any dataset.
**Install farasapy to segment text for AraBERT v1 & v2 `pip install farasapy`**

```python
from arabert.preprocess import ArabertPreprocessor

model_name = "aubmindlab/bert-base-arabertv2"
arabert_prep = ArabertPreprocessor(model_name=model_name)

text = "ولن نبالغ إذا قلنا: إن 'هاتف' أو 'كمبيوتر المكتب' في زمننا هذا ضروري"
arabert_prep.preprocess(text)
>>>"و+ لن نبالغ إذا قل +نا : إن ' هاتف ' أو ' كمبيوتر ال+ مكتب ' في زمن +نا هذا ضروري"
```

You can also use the `unpreprocess()` function to reverse the preprocessing changes, by fixing the spacing around non alphabetical characters, and also de-segmenting if the model selected need pre-segmentation. We highly recommend unprocessing generated content of `AraGPT2` model, to make it look more natural.
```python
output_text = "و+ لن نبالغ إذا قل +نا : إن ' هاتف ' أو ' كمبيوتر ال+ مكتب ' في زمن +نا هذا ضروري"
arabert_prep.unpreprocess(output_text)
>>>"ولن نبالغ إذا قلنا: إن 'هاتف' أو 'كمبيوتر المكتب' في زمننا هذا ضروري"
```

### Accepted Model Names:
The `ArabertPreprocessor` class expects one of the following model names:

Note: You can also use the same model name from the `HuggingFace` model repository without removing `aubmindlab/`. Defaults to `bert-base-arabertv02` with no pre-segmentation

```
bert-base-arabertv01
bert-base-arabert
bert-base-arabertv02
bert-base-arabertv2
bert-large-arabertv02
bert-large-arabertv2
araelectra-base
araelectra-base-discriminator
araelectra-base-generator
aragpt2-base
aragpt2-medium
aragpt2-large
aragpt2-mega
```
# Examples Notebooks

- You can find the old examples that work with AraBERTv1 in the `examples/old` folder
- Check the [Readme.md](https://github.com/aub-mind/arabert/tree/master/examples) file in the examples folder for new links to colab notebooks

# TensorFlow 1.x models

**You can find the PyTorch, TF2 and TF1 models in HuggingFace's Transformer Library under the ```aubmindlab``` username**

- `wget https://huggingface.co/aubmindlab/MODEL_NAME/resolve/main/tf1_model.tar.gz` where `MODEL_NAME` is any model under the `aubmindlab` name


# If you used this model please cite us as :
## AraBERT
Google Scholar has our Bibtex wrong (missing name), use this instead
```
@inproceedings{antoun2020arabert,
  title={AraBERT: Transformer-based Model for Arabic Language Understanding},
  author={Antoun, Wissam and Baly, Fady and Hajj, Hazem},
  booktitle={LREC 2020 Workshop Language Resources and Evaluation Conference 11--16 May 2020},
  pages={9}
}
```
## AraGPT2
```
@misc{antoun2020aragpt2,
      title={AraGPT2: Pre-Trained Transformer for Arabic Language Generation},
      author={Wissam Antoun and Fady Baly and Hazem Hajj},
      year={2020},
      eprint={2012.15520},
      archivePrefix={arXiv},
      primaryClass={cs.CL}
}
```

## AraELECTRA
```
@misc{antoun2020araelectra,
      title={AraELECTRA: Pre-Training Text Discriminators for Arabic Language Understanding},
      author={Wissam Antoun and Fady Baly and Hazem Hajj},
      year={2020},
      eprint={2012.15516},
      archivePrefix={arXiv},
      primaryClass={cs.CL}
}
```


# Acknowledgments
Thanks to TensorFlow Research Cloud (TFRC) for the free access to Cloud TPUs, couldn't have done it without this program, and to the [AUB MIND Lab](https://sites.aub.edu.lb/mindlab/) Members for the continous support. Also thanks to [Yakshof](https://www.yakshof.com/#/) and Assafir for data and storage access. Another thanks for Habib Rahal (https://www.behance.net/rahalhabib), for putting a face to AraBERT.

# Contacts
**Wissam Antoun**: [Linkedin](https://www.linkedin.com/in/wissam-antoun-622142b4/) | [Twitter](https://twitter.com/wissam_antoun) | [Github](https://github.com/WissamAntoun) | wfa07 (AT) mail (DOT) aub (DOT) edu | wissam.antoun (AT) gmail (DOT) com

**Fady Baly**: [Linkedin](https://www.linkedin.com/in/fadybaly/) | [Twitter](https://twitter.com/fadybaly) | [Github](https://github.com/fadybaly) | fgb06 (AT) mail (DOT) aub (DOT) edu | baly.fady (AT) gmail (DOT) com



