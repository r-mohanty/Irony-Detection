# Contextually Informed Irony Detection

## Overview
This project is an unofficial implementation of the paper: <b>Sparse, Contextually Informed Models for Irony Detection: Exploiting User Communities, Entities and Sentiment</b>

https://aclanthology.org/P15-1100.pdf

<i>2015 Association for Computational Linguistics</i>

The aim of this project is to detect verbal irony in comments posted on reddit threads. The key idea here is to use a contextually informed model that uses the information provided in the noun phrases of the comment text, thread title and parent comments along with the comment's overall sentiment and the forum (subreddit) to which the comment was posted. In this project I have implemented the baseline Bag-of-Words model and the NNP+ models as described in this paper. We can see that the fully feturized contexually informed model shows improved performance over the bag of words model.

## Requirements
  * Python
  * NumPy
  * Pandas
  * scikit-learn
  * spaCy
  * spacytextblob

## Data
The data used for this project is similar to the one described in the paper. It is a list of reddit comments organised into sentences with their respective comment ids, thread titles, subreddit and labels. Many comments also have a parent id which is the comment id of its parent comment in the thread of comments.

## Implementation Details
The first model implemented in this project is the Bag-of-Words model. This model has been used as baseline to compare the performance of other models.
For the Bag-of-Words model, I split each sentence on whitespace used the words to create uni-grams and bi-grams. A count of each of these i-grams were used as features for the model. These features also contain exclamation points and emoticons which give an insight into the sentence being ironic or non-ironic.

The second model that has been implemented in this project is the NNP+ model. In this model I used the NNP+ features, which included the NNPs of each sentence and the NNPs of all of its ancestors (Parents and Parent's parents recursively). I also implemented the three way interaction terms as described in the paper between the NNP+, sentiment of the sentence and subreddit for each sentence. Finally, I used uni-grams and bi-grams of these three way interaction terms along with the sentiment(positive/negetive) of that sentence to get the features for the model.

The model used in this project is the stochastic gradient descent model which has been implemented using sklearn. I used the l2 regularized log-loss and the class weights were balanced. I used grid search to find the values of alpha that maximized the F1 score on the training data. I used RepeatedKFold cross-validation to divide the data into 80% training set and 20% test set and the model was run on 50 different iterations of the entire dataset. Finally, the precision and recall were calculated for each iteration and the mean, meadian, 25th and 75th percentile scores of these metrics were found.


## Results
The model was run on 50 different iterations of the entire dataset and precision and recall were calculated for each iteration.
Below are the values of the mean, meadian, 25th and 75th percentile scores of these metrics:


### <u><b>Bag of Words Baseline:</b></u>
#### <b>Precision</b>
Mean: 0.09 | Median: 0.09 | 25th Percentile: 0.06 | 75th Percentile: 0.13
#### <b>Recall</b>
Mean: 0.14 | Median: 0.13 | 25th Percentile: 0.08 | 75th Percentile: 0.17

### <u><b>NP Sentiment Context Model:</b></u>
#### <b>Precision</b>
Mean: 0.15 | Median: 0.15 | 25th Percentile: 0.11 | 75th Percentile: 0.18
#### <b>Recall</b>
Mean: 0.31 | Median: 0.31 | 25th Percentile: 0.26 | 75th Percentile: 0.37

## References
```
@inproceedings{wallace-etal-2015-sparse,
    title = "Sparse, Contextually Informed Models for Irony Detection: Exploiting User Communities, Entities and Sentiment",
    author = "Wallace, Byron C.  and
      Choe, Do Kook  and
      Charniak, Eugene",
    booktitle = "Proceedings of the 53rd Annual Meeting of the Association for Computational Linguistics and the 7th International Joint Conference on Natural Language Processing (Volume 1: Long Papers)",
    month = jul,
    year = "2015",
    address = "Beijing, China",
    publisher = "Association for Computational Linguistics",
    url = "https://aclanthology.org/P15-1100",
    doi = "10.3115/v1/P15-1100",
    pages = "1035--1044",
}
```
