# DSI Capstone: Shopee Product Matching

## Problem Statement

Retail companies like Shopee use product matching to assure customers that their rates are competitive to that of other retailers for the same products. They seek to identify identical products across different product images, titles and descriptions.

Given product titles and images, this project predicts which products are the same. 

Group sizes for products range from 2 to 51. Predictions will be made row-wise for each product, and will include the product itself.

For example, if the set of all products is [A, B, C, D, E], and we believe A, B, C are the same and D & E are the same, we will predict as such:

|Product|Predictions|
|-------|-------|
|A|A, B, C|
|B|B, A, C|
|C|C, A, B|
|D|D,E|
|E|E,D|

Predictions will be scored using the F1 Score / Dice Metric: $\frac{2\times(A \bigcap B)}{|A| + |B|}$, where A is the set of our predictions and B is the set of actual matches.

For example, if the actual matches for product A is only A & B, our score will be: $\frac{2\times([A,B] \bigcap [A,B,C])}{|[A,B]| + |[A,B,C]|}$ = $\frac{2\times 2}{5} = 0.8$

The F1 Score for each row will be averaged across all rows to give the final score:

|Product|Predictions|Actual Matches|F1 Score|
|-------|-----------|--------------|--------|
|A|A, B, C|A, B|0.8|
|B|B, A, C|B, A|0.8|
|C|C, A, B|C, D, E|0.33|
|D|D,E|D, C, E|0.8|
|E|E,D|E, C, D|0.8|
| |   |Average Score|0.71|

The train dataset consists of 34,250 product images, image phash and titles along with their label groups. The hidden test dataset on Kaggle will consist of 70,000+ product images, image phash and titles.

## Executive Summary

Image feature embeddings of size 1,792 were generated using default and retrained EfficientNetB4.

Text feature embeddings of size 25,053 were generated using TF-IDF vectorizer on processed title tokens.

Text feature embeddings of size 768 were generated using Google Language-agnostic BERT Sentence Embedding.

sklearn/cuML NearestNeighbors algorithm was applied to these embeddings to generate 51 nearest neighbours for each product. Grid search of various distance thresholds was performed to find the optimum threshold to predict product matches.

By taking the set union of various models, recall improved as the predictions from different models complemented each other.

By setting a soft distance threshold, precision improved as fewer excessive predictions were made.

The final model using an ensemble of image and text embeddings achieved a train score of 0.783 and [Kaggle test score of 0.728](https://www.kaggle.com/weezijian/ensemble-model).

## Data Dictionary

The train data comprises a .csv file with posting_id, image, image_phash, title and label_group.

The test data will have posting_id, image, image_phash and title.

|Column|Type|Description|
|-------|-----------|--------------|
|posting_id|string|Unique identification number for each product|
|image|string|Name of image file stored in image folder|
|image_phash|string|Perceptual hash of image|
|title|string|Product title|
|label_group|int|Identification number for product groups <br /> Products are the same if they have the same label group <br /> Not provided for test data|