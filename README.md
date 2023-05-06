# Amazon-ML-Challenge-Entropy
Our submission for the Amazon ML challenge 2022 for the use of predicting the product length given a large data of 2.2million products. 

Feature Engineering:


1. Text Preprocessing:
The text data in the 'DESCRIPTION', 'TITLE', and 'BULLET_POINTS' columns were preprocessed using the following steps:
* The NaN values in the dataset were replaced with an empty string. 
* Stemming: Porter stemming was applied to the 'DESCRIPTION' and 'BULLET_POINTS' columns to reduce the words to their root form.
* Punctuation Removal: Punctuation symbols were removed from all three columns using the remove_punctuation function.
* Stopwords Removal: Common English stopwords were removed from all three columns using the remove_stop_words function.
* Lowercasing: All text in the three columns was converted to lowercase using the to_lower function.
2. Vectorization:
* The preprocessed text data was then vectorized using the CountVectorizer and TfidfVectorizer functions from scikit-learn.
* The CountVectorizer function was used for the 'TITLE' column, while the TfidfVectorizer function was used for the 'DESCRIPTION' and 'BULLET_POINTS' columns.
* The TfidfVectorizer function assigns higher weights to words that are more unique to a product, and lower weights to words that are common to many products. 
3. Column Reduction:
* To reduce the dimensionality of the data, columns with low document frequency were removed using the reducecolumns function.
* The final features were then merged into a sparse matrix
4. Target Variable:
* The target variable was the 'PRODUCT_LENGTH' column, which was logarithmically transformed using NumPy’s log function to achieve a more normalized distribution.


Model Building:
1. Train-Test Split:
* The dataset was split into training and testing sets using the train_test_split function at a split ratio of 65:35.
2. Model Architecture:
* A Sequential model is built using Keras. 
* The model consists of two hidden layers with 7 units and 1 unit respectively with ReLU activation function. 
* The model is compiled using mean squared error as the loss function and Adam optimizer. 
3. Model Train and Prediction:
* The model was trained on the training set using the KerasRegressor wrapper function from scikit-learn.
* The trained model was used to make predictions on the testing set, and the resulting predictions were exponentiated using NumPy’s expm1 function to transform them back to the original scale of the 'PRODUCT_LENGTH' column.
4. Model Evaluation:
Given metric was used for evaluation-
 score = max( 0 , 100*(1-metrics.mean_absolute_percentage_error(actual,predicted)))
