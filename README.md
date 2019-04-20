Tweet Sentiment Classification
===
In this project, I implemented a sentiment classification algorithm using single hidden layer neural network that classifies the sentiment of a tweet/sentence giving the dominant emotion(s) e.g. anger,sadness,fear or joy in the text.

![results](https://user-images.githubusercontent.com/41015749/56460488-27aee500-6369-11e9-8518-69e9e2f8cd65.jpg)

Details
-------
We read a large Tweet dataset and clean each tweet then use Stemming and using bag of words model, feed each tweet to single layer neural network for classification. Link for dataset is given below:
        http://saifmohammad.com/WebPages/EmotionIntensity-SharedTask.html

This link has 4 kinds of dataset: one for anger, one for fear, one for joy and one for sadness for training set and 4 files for test set. Each of these datasets have the following format:
All sentences start with a 

[number, tweet_sentence, label [fear,anger,joy,sadness], intensity_of_emotion].

The intensity of emotion varies from 0 to 1 where 1 expresses high intensity of anger, fear, joy or sadness. It is seen that only tweets with threshold higher than 0.5 or 0.6 “ACTUALLY” express the sentiment strongly. I am using this threshold which leaves us with the following:

Anger_training_set: emotion intensity threshold 0.5 411 lines

Fear_training_set: emotion intensity threshold 0.6 347 lines 

Joy_training_set: emotion intensity threshold 0.5 405 lines

Sadness_training_set: emotion intensity threshold 0.5 384 lines

In total I have 1547 lines in training data and total 3783 unique words that includes emoticons

### Working of Software
The working of software is categorized into following steps:

### Preprocessing of the text
First we get rid of numbers, punctuations and extra spaces in every tweet/sentence text string. We also remove @<tags> becasuse we dont need them. This is done in the clean_data method of the code.

#### 1)	Tokenization
We create a bag of words which is just a dictionary of the words and their frequencies with which they appear in a text string line.
For example “How are you my friend?” when tokenized becomes a list of words as:
[‘How’,’are’,’you’,’my’,’friend’,’?’]
This is also done in the clean_data method of the code.

#### 2)   Stemming
Stemming in text processing means cutting the word to its origin for example, walking, walked and walker have stem “walk”. NLTK toolkit in Python has different kinds of stemmers such as Porter, Lancaster stemmer. We are using Lancaster Stemmer for our software. This function is implemented in the bag_of_words method of code.

#### 3)   Bag of Words
Neural network cannot process words so we encode the words in tweets according to the total number of distinct words we have in all the tweets of the whole training set. We have 3783 unique words so we make a list 3783 elements long and in each tweet sentence we put a 1 where the word in tweet matches the word in those 3783 unique words and 0 otherwise. This function is implemented in bag_of_words and encode_sentence method of code.

### Neural Network Classifier
Now we create a classifier using Neural networks for which we will start with a single hidden layer RELU activation function neural network with dimensions equal to (bag of words length i.e. 3783) x (training samples i.e. 1547). And see what results we get. The last layer will be of softmax activation function with 4 units as we have 4 classes i.e. sadness, anger, joy and fear.

### Classification stats
We trained our single hidden layer neural network for just 50 EPOCHS and it gives the following stats at the end of 50 EPOCHS:

              precision    recall  f1-score   support

           0       1.00      0.98      0.99       417
           1       0.98      0.97      0.98       349
           2       0.96      0.98      0.97       377
           3       0.99      0.99      0.99       404

![all_curves](https://user-images.githubusercontent.com/41015749/56461263-313e4a00-6375-11e9-9ae0-ee53366f3440.png)

## Results
Giving a real-time tweet or a sentence to this software gives the classification to us. Following image shows the result. We show all the emotions expressed by the text if their magnitude is greater than 0.2.

![results](https://user-images.githubusercontent.com/41015749/56460488-27aee500-6369-11e9-8518-69e9e2f8cd65.jpg)

It can be seen in image above that the classifier predicts the right emotion in each tweet, however, in the last sentence, "I want to be happy", the classifier thinks that "joy" is expressed in the sentence which is not correct. This is where LSTM (Long Short Term Models) will be effective as using previous word of a sentence will help understand context of the sentence. Still this one does a pretty good job. In the next tutorial i am going to extend this project to a "Depression Assistant". Please give a STAR if you liked this project.

## Acknowledgement
----------------
I would like to give credit to this article "https://machinelearnings.co/text-classification-using-neural-networks-f5cd7b8765c6" for useful insights that helped me learn about this project and while the article is based on text classification using 2 hidden layer neural network with sigmoid activation function, I did Tweet sentiment classification using single hidden layer neural network with Relu activation function.
