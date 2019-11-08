# Sequential Recommendation Datasets
This repo simplifies how sequential recommendation datasets are used.
<p>
    <img src="https://img.shields.io/badge/pandas->=0.24-brightgreen?style=flat-square"/>
    <img src="https://img.shields.io/badge/python->=3.5-brightgreen?style=flat-square"/>
    <img src="https://img.shields.io/badge/pypi-v0.0.1-brightgreen?style=flat-square"/>
</p>

## Datasets
Name | Item | Website
---- | ---- | -------
MovieLens-20M | Movie | https://grouplens.org/datasets/movielens/
Last.fm-1K | Artist or Music | http://ocelma.net/MusicRecommendationDataset/lastfm-1K.html
Gowalla | Check-in | https://snap.stanford.edu/data/loc-Gowalla.html

## Installation
Install from pypi:
```
pip install srdatasets
```
Or from Github for the latest version:
```
pip install git+https://github.com/guocheng2018/sequential-recommendation-datasets.git
```

## Usage

1. Download a dataset, for example `MovieLens-20M`
```bash
python -m srdatasets download --dataset="MovieLens-20M"
```
2. Process the downloaded dataset with details logged to console
```bash
python -m srdatasets process --dataset="MovieLens-20M"

# Add -h option to see all specific settings of dataset processing
python -m srdatasets process -h
```
3. Check local datasets info
```
python -m srdatasets info
```
4. Use `srdatasets.DataLoader` to get data batchly
```python
from srdatasets import DataLoader

# For development (tune hyperparameters)
trainloader = DataLoader("MovieLens-20M", batch_size=32, Train=True, development=True)
testloader = DataLoader("MovieLens-20M", batch_size=32, Train=False, development=True)

# For performance test
trainloader = DataLoader("MovieLens-20M", batch_size=32, Train=True, development=False)
testloader = DataLoader("MovieLens-20M", batch_size=32, Train=False, development=False)

for epoch in range(10):

    # Train
    for user_ids, input_item_ids, target_items_id in trainloader:
        # Shapes
        # user_ids: (batch_size,)
        # input_item_ids: (batch_size, input_len)
        # target_item_ids: (batch_size, target_len)
        ...

    # Evaluate
    for user_ids, input_item_ids, target_item_ids in testloader:
        ...
```

## TODO
- [ ] Add negative sampling
- [ ] Add timestamp feature to dataset
- [ ] Enable loading datasets with different processing setttings
- [ ] Store dataset statistics to local
- [ ] Support Custom datasets


## Disclaimers
The datasets have their own licenses, this repo (under MIT license) only provides an way to use them.