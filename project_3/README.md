# Project 3: Web APIs & Classification

## Problem Statement

**Scenario:**

[r/TalesFromTheCustomer](https://www.reddit.com/r/TalesFromTheCustomer/) and [r/TalesFromRetail](https://www.reddit.com/r/TalesFromRetail/) are similar subreddits describing customer service experiences, one from the point of view of the customer, and one from the service staff. 

These subreddits contain narratives of people's experiences and are thus rich in text data and suitable for natural language processing (NLP) modelling using a bag of words approach. As they are not too dissimilar in content, it is interesting to examine if a NLP machine learning model can distinguish between these 2 subreddits and in the process, identify the most frequent words associated with customer / retail experiences.

Such a NLP model could be useful to retail executives who wish to understand more about the experiences of their customers and frontline staff. As such, the NLP model should preferably be interpretable, allowing inference on the significance of each word to the model's classification criteria.

**Task:**

This project will scrape the Reddit API of these 2 subreddits to collect text data (title + main post). After data cleaning, exploratory data analysis will be performed to identify the most frequent words in each subreddit. 

The data will be split into a train and test set. Classification models will be fit on the train set and scored on the test set to identify the best performing model. F1 score will be used as the main metric. The best models will be analyzed to examine how their underlying algorithms could have affected their predictive ability on this bag of words classification problem.

## Executive Summary

927 rows of data for r/TalesFromTheCustomer and 320 rows for r/TalesFromRetail were scraped and combined into a single dataframe. The columns 'title' and 'selftext' were combined into a single 'text' column. Lemmatized and stemmed versions of the text were created as new columns.

A first level of screening was performed across each shortener (lemmatized, stemmed, raw unshortened text), each vectorizer (Count Vectorizer, TF-IDF Vectorizer), and each model (Logistic Regression, Multinomial Naive Bayes, Support Vector Machine, K-Nearest Neighbours, Extra Trees and Random Forest). 

Logistic Regression, Multinomial Naive Bayes and Support Vector Machine (each with Count Vectorizer) and K-Nearest Neighbours (with TF-IDF Vectorizer) were found to be the best performing models and grid searched on.

After grid searching, Logistic Regression (test f1 score = 0.70) and Multinomial Naive Bayes (test f1 score = 0.72) were selected as the final models. If we want to **maximize precision and minimize false positives**, **Logistic Regression** would be the best model. If we want to **maximize recall and minimize false negatives**, **MultinomialNB** would be the best choice.

## Data Dictionary

|Feature        |Type       |Description                |
|---------------|-----------|---------------------------|
|subreddit      |string     |Identifies which subreddit the post is from (r/TalesFromTheCustomer or r/TalesFromRetail)|
|selftext       |string     |Content of the subreddit post|
|title          |string     |Title of the subreddit post|
