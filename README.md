# contrastive-clustering

⚠️ **This repository is under heavy construction!** ⚠️

## Installation Manual

This guide assumes that you use Unix operating systems or the likes (such as WSL - Windows Subsystem for Linux).

### Python Virtual Environment
You can set up this repository using Python Virtual Environment (venv) using `requirements.txt` file.

```bash
cd contrastive-clustering
python3 -m venv cluster # set up venv
source cluster/bin/activate # activate venv
pip3 install -r requirements.txt # install packages
```

## Quick start

Run the script to see the results on benchmark dataset: [TenKGNADClusteringP2P](https://huggingface.co/datasets/slvnwhrl/tenkgnad-clustering-p2p). This dataset consists of news articles, each corresponding to one of the 9 labels.

```bash
source cluster/bin/activate # activate venv
python3 -m src.cc.data_preprocessing.download_10kgnad # download benchmark dataset
bash run_benchmark.sh # (1) pre-process data, (2) create contrastive data pairs, (3) fine-tune embedding checkpoint, and (4) cluster embeddings
```

For the details of each step, you can check the bash script itself.

The results are saved to `data/processed/augmented/*`.

### Test run

To test in a smaller dataset, use our provided test data `data/10kgnad-p2p-test.jsonl` and the test Bash script `run_test.sh`. So the following command:

```bash
source cluster/bin/activate # activate venv
bash run_test.sh # (1) pre-process data, (2) create contrastive data pairs, (3) fine-tune embedding checkpoint, and (4) cluster embeddings
```

The results are saved also to `data/processed/augmented/*`

## Adapt to your own dataset

In case you would like to adapt the codebase to your own dataset, you have to do the following:
1. update the `data_processor.py` script to include your data's metadata for pre-processing.
2. check `run_benchmark.sh` and update the dataset references to your dataset, as well as the desired number of epochs and batch size.

## Background

This project aims to improve sentence-embedding models using Contrastive Learning. This is achieved by fine-tuning the pre-trained sentence-embedding models using positive pairs (i.e. similar texts) via augmentation methods.

The project involves 4 steps:
1. Data preprocessing
2. Data augmentation
3. Fine-tuning embedding models
4. Clustering

Each step has the corresponding scripts:
- Data preprocessing - `data_preprocessing/*`
- Data augmentation - `data_augmentation/*`
- Fine-tuning embedding models - `embedding/*`
- Clustering - `clustering/*`