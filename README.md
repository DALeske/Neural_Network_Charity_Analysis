# MODULE 19 Challenge: Neural_Network_Charity_Analysis

## OVERVIEW
The non-profit organization, Alphabet Soup, provides funding to other organizations. Despite best intentions, not all organizations that get funded are successful.  The purpose of the analysis was to determine whether it is possible through a neural network analysis whether organizations applying for funding will be successful if funded.

## METHODS

### PREPROCESSING
The data was preprocessed prior to compiling, training, and evaluating the model. 

![Table](/Resources/Table.png)

### DATA FIELDS
- Target: 
    - IS_SUCCESSFUL
- Retained Features: 
    - APPLICATION_TYPE
    - AFFILIATION
    - CLASSIFICATION
    - USE_CASE
    - ORGANIZATION
    - STATUS
    - INCOME_AMOUNT
    - SPECIAL_CONSIDERATIONS
    - ASK_AMOUNT
- Removed Features (for lack of helpful information)
    - EIN
    - NAME

### BUCKETING
    The number of unique APPLICATION_TYPEs (n=17) and CLASSIFICATIONs (n=71) was considered too high, and therefore application types with a frequency below 500 and classifications with a frequency below 175 were combined into an 'Other' category for each feature. 

### ENCODING
    Categorical data was encoded using OneHotEncoder, which assigned presence of each classification as a 1 and absence as 0, resulting in a unique feature for each categorical classification.

### NOISY FEATURES
    In some iterations of the model, noisy features were identified and dropped. Specific features that were found to be noisy and were dropped were: 

    - AFFILIATION_CompanySponsored
    - AFFILIATION_Independent
    - CLASSIFICATION_C1000
    - CLASSIFICATION_C1200
    - CLASSIFICATION_C2000
    - USE_CASE_Preservation
    - USE_CASE_ProductDev
    - ORGANIZATION_Association
    - ORGANIZATION_Trust
    - INCOME_AMT_0
    - INCOME_AMT_25000-99999

### SPLITTING
    The data was split into training and testing data using the train_test_split method in skelarn

### SCALING
    Data was transformed using StandardScaler to ensure standardize the distribution and variability of each feature.

### COMPILE, TRAIN, and EVALUATE THE MODEL
    A deep neural network was compiled using the keras library of sklearn. A sequential model was defined, with 2 or 3 hidden layers. The number of nodes per layer was varied depending on the model. ReLU activation was used initially for the hidden layers and a sigmoid layer was used for the output layer. Tanh and Leaky ReLU activation was also trialed. The number of epochs was set at 100 for all trials as not to overfit. After fitting the model to the training data, the model was evaluated using the test data set.

## RESULTS
    The initial run of the model prior to optimization resulted in 53% accuracy in the training data and 53% accuracy in the test data. Therefore optimization was required.

### OPTIMIZATION ATTEMPT #1
    For the first attempt at optimization, the number of hidden nodes was increased from 2 to 3 to try and achieve a better fit to the data in case of a third order relationship. The ReLU activation was used because most of the data is positive. Following the first attempt, the accuracy of the training data remained at 53% and the testing data remained at 53%.

### OPTIMIZATION ATTEMPT #2
    For the second attempt at optimization, the number of neurons in the hidden layers was increased from 8, 6, 4 respectively to 12, 8, and 4 to try and describe the interactions between the data better. In addition, features with variable data were dropped in an attempt to reduce some of the noise in the data. The activation was kept as ReLU. Following the second attempt, the accuracy of the training data still remained at 53% but the testing data accuracy actually dropped to 51%.

### OPTIMIZATION ATTEMPT #3
    For the third attempt at optimization, the number of nodes in the hidden layers was increased significantly from 12, 8, and 4 respectively to 80, 40, and 10 to further try to describe the interactions between the features better, since the number appeared too low in the previous attempts. In addition the activation was changed from ReLU to LeakyReLU to try to see if allowing description of some negative values would help the model. Following the third attempt at optimization, accuracy of the training data was still 53% and the testing data was also 53%.

  ## Summary
    The target of 75% was not achieved with the models that I used, despite trying multiple different approaches. The models that I ran had an accuracy of around 53%, which is basically the same as flipping a coin in this binary outcome scenario. 

    My recommendation would be to use a random forest generator to try and model the data. It is possible that the decision tree approach may be more efficient in this case, at least in my hands. In addition, the output of the random forest analysis is easier to interpret. 