---
title: Get Started
linkTitle: Get Started
menu: {main: {weight: 05}}
show_toc: true
---

## Overview
TGB-Seq comprises eight temporal graph datasets that exhibit intricate sequential dynamics inherently. It provides both a dataloader and an evaluator for ease of use. The dataloader manages automatic downloading and preprocessing, and the evaluator provides standardized evaluation with fixed negative samples and metrics.
## Install

You can install TGB-Seq using Python package manager pip.

```bash
pip install tgb-seq
```

#### Requirements

- Python>=3.9
- numpy>2.0
- pandas>=2.2.3
- huggingface-hub>=0.26.0
- torch>=2.5.0


## Package Usage

### Quick Start
Get started with TGB-Seq using this quick-start example built on [DyGLib](https://github.com/yule-BUAA/DyGLib). Just follow the commands below to begin your journey with TGB-Seq! 🚀🚀🚀

```bash
pip install tgb-seq
git clone git@github.com:TGB-Seq/TGB-Seq.git
cd examples
python train_link_prediction.py --dataset_name GoogleLocal --model_name DyGFormer --patch_size 2 --max_input_sequence_length 64 --gpu 0 --batch_size 200 --dropout 0.1 --sample_neighbor_strategy recent
```

To submit your results to the [TGB-Seq leaderboard](https://TGB-Seq.github.io/leaderboard/), please fill in this [Google Form](https://forms.gle/dbhX8vVNzVTLU9pL8).


### Dataloader

For example, to load the Flickr dataset to `./data/`, run the following code:
```python
from tgb_seq.LinkPred.dataloader import TGBSeqLoader
data=TGBSeqLoader("Flickr", "./data/")
```
Then, Flickr.csv and Flickr_test_ns.npy will be downloaded in `./data/Flickr/`. The arrays of source nodes, destination nodes, interaction times, negative destination nodes for the test set can be accessed as follows.

```python
src_node_ids=data.src_node_ids
dst_node_ids=data.dst_node_ids
node_interact_times=data.time
test_ns=data.test_ns
```

### Evaluator
Up to now, all the TGB-Seq datasets are evaluated by the MRR metric. The evaluator takes `positive_probabilities` with size as `(batch_size,)` and `negative_probabilities` with size as `(batch_size x number_of_negatives)` as inputs and outputs the rank of eash positive sample with size as `(batch_size)`.
```python
from tgb_seq.LinkPred.evaluator import Evaluator 
evaluator=Evaluator()
# For the MRR metric, this will return a list of rank, 
# each represents the rank of one positive sample.
result_dict=evaluator.eval(positive_probabilities,negative_probabilities)
```

## Citing TGB-Seq
If you use TGB-Seq datasets, please cite [our paper](https://openreview.net/forum?id=8e2LirwiJT).