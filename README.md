# Neural Network Charity Analysis with Keras

## Overview - Purpose

Beks needs help creating a binary classifier that is capable of predicting whether applicants will be successful if funded by the Alphabet Soup company. They have provided us with a CSV containing more than 34000 organizations that have received funding from Alphabet Soup over the years. Our goal is to preprocess the data, then create a basic neural network model, compile, train, and evaluate it. Afterwards, we will attempt to optimize it by performing more preprocessing by dropping bad columns, performing more binning for rare occurences, handling skewed data, and changing model parameters. 

## Results

### Preprocessing

What variable is considered the target for your model?
  - The column: IS_SUCCESSFUL, which is a binary value that tells us if the applicant was successful after receiving funding.

What variables are considered to be the features for your model?
  - After the EIN and NAME columns were dropped, the features were: APPLICATION_TYPE, AFFILIATION, CLASSIFICATION, USE_CASE, ORGANIZATION, STATUS, INCOME_AMT, SPECIAL_CONSIDERATIONS, and ASK_AMT. However, I also dropped STATUS and SPECIAL_CONSIDERATIONS. 

What variables are neither targets nor features, and should be removed from the input data? 
  - The EIN and NAME columns were unique identifiers for each entry and therefore they provide no value to a model and should be dropped. 

### Compiling, Training, and Evaluating the Model

How many neurons, layers, and activation functions did you select for your neural network, and why? 
  - I tried many different combinations of neurons, layers, and activation functions. Unfortunately, they all performed comparably so there was no clear choice. I ended up choosing a model with three hidden layers that each had 20 nodes and used tanh activation functions. Having too many nodes or hidden layers seemed to overfit on the training set, so I tried to keep them low. Tanh and Relu performed similarly, but it seemed Tanh trained a little faster, so I chose it. 

Were you able to achieve the target model performance?
  - I was not able to achieve 75% accuracy. It's possible more advanced or careful processing is needed to allow the model to perform better. It's also possible that not much can be done to improve the current performance of around 72% accuracy. 

What steps did you take to try and increase model performance? 
  - I dropped two columns that only had two classes each with one of those classes having less than 30 values.
  - I tried binning the rare occurences of some of the other columns into an Other category.
  - I also tried re-binning the Income Amount column to a smaller number of groups that were closer in counts.
  - The numerical Ask Amount column was highly skewed right, so I binned it into three groups.
  - In an earlier run I tried adding more neurons to the hidden layers to no avail.
  - A third hidden layer was added (and there were iterations without it).
  - Tanh was used in place of Relu (though both were tried several times). 
  - Finally, I increased the number of epochs from 100 to 200, but the model had effectively converged anyways. 

## Summary

The final neural network model had three hidden layers with 20 nodes each and tanh activation functions. The output layer had one unit with a sigmoid activation. After training for 200 epochs it had a training set loss of 0.5318 and an accuracy of 0.7418. The test set loss was 0.5610 and the accuracy was 0.7222. Looking at plots of the loss and accuracy the model had clearly converged. A random forest classifier would be another model that can solve this classification problem. Random Forests can also perform well with a decent amount of features and handle skewed data without needing scaling. So they require less preprocessing and train faster. Finally, random forests can allow us to see the feature importances of each feature in our model, which can help in determining which features to keep and perhaps where to focus preprocessing efforts. 
