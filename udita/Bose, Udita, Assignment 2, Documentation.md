
# Introduction of Machine Learning, Assignment 2

> Prepared by Udita Bose

This document describes the method and conclusion for the research question
_Recommendation of artist based on selected feature using KNN, Decision Tree and Neural Network_.

    In this task tempo was selected as the target label to classify the data and predict an artist 
based on the tempo of the track. 
The tempo in the dataset is numeric continuous (float) in value but presented as string.
In the data cleaning phase the data is first converted in float. 
The value of tempo ranges from _30_ to _220_. The data is converted into binned categories, 
ranging from low to very high.
    During the data exploration the count plot of the tempo groups show that the data is nearly evenly 
distributed amongst the four groups.
The scatter plot of danceability vs popularity reveals that low tempo tracks are lower in danceability. 
The very high tempo songs dominates the central part of the scatter plot, but the most popular songs 
are usually the high tempo tracks. 
    The feature is a categorical nature so only 
classification models were chosen to test. As the data is fairly balanced around tempo groups, the accuracy score
is used to evaluate performance of the models. The confusion matrix is used to verify the accuracy score 
along side f1-score. In the most of the scenario both the score predicted similar performance scores.
    Recursive feature elimination with cross-validation was used to automatically engineer features
and select the best 32 from the feature set.
    To establish a baseline a Dummy classifier was trained, which resulted in 27% accuracy.
The first iteration of training, KNN with N=5, Decision and Random Forest with depth 5 and Neural Network
with 400 iteration is used. This preliminary run without feature selection showed an improvement of the 
accuracy, but not significantly. The KNN showed a modest gain of 7% accuracy, while Neural Network
performed the best with a 43% accuracy. This suggested that tempo groups are highly distributed amongst
the feature set. 
    Subsequent iterations of fitting with feature selection, scaled data, and stratified folds(5)
did not improve the accuracy beyond 43%. The data is non-hierarchical, thus neither Decision Tree or Random
forest showed any significant gain.
    To tune parameters Random Forest and Neural Network were selected. For the Random Forest the depth
the minimum depth was chosen 10, and maximum 30. The L2 regularization for the Neural Network
is kept at 1, and iteration at 400. The Random Forest outperformed Neural Network with an accuracy score of 44.88%
at depth 30.
    Finally to demonstate the capability of the model to recommend artist a small dataset from the training
data was picked and tested against the best model. From the predicted values music with predicted tempo was
selected.





The task was divided in the following steps to 
- data cleaning and pre-processing 
- data visualization
- baseline classification
- feature engineering and feature selection via cross validation
- fitting `KNeighborsClassifier`, `SVC`, `DecisionTreeClassifier`, `RandomForestClassifier`,
`MLPClassifier` without feature selection
- fitting `KNeighborsClassifier`, `SVC`, `DecisionTreeClassifier`, `RandomForestClassifier`,
`MLPClassifier` with feature selection
- fitting classifier models with startified data folds
- tuning hyperparameters of Random Forest and MLP Classifier, and selection of the best model
- using tuned parameters to execute final fitting
- 





A dummy classifier is fit to generate a baseline, which produced an accuracy of 25.65%.
Subsequently the data is fit with `KNeighborsClassifier`, `SVC`, `DecisionTreeClassifier`, `RandomForestClassifier`,
`MLPClassifier` with both feature selection and without.

For both, feature selection status, `KNeighborsClassifier` and `MLPClassifier` performed
best, but the accuracy was around 42%. This is an improvement over the Dummy classifier.
But, feature selection didn't improve the model accuracy. From the correlation data prior fitting
shows that the tempo is really well correlated with danceability, acoustics, energy and valence.
This explains well why the accuracy did not improve vastly.

`RandomForestClassifier` is used to test the theory that an ensemble method may work better, instead
of `DecisionTreeClassifier`. But that assumption was not correct. This corroborates well with
the data not being hierarchical against tempo.

At the end a hyperparameter tuning via `RandomizedSearchCV` ran on both `RandomForestClassifier` and 
`MLPClassifier`. `RandomForestClassifier` performed better, but not much better than  `MLPClassifier` 
without tuning.

For the sake of completion, final feature importance was extracted and danceabilty show high
importance.

Finally, to find recommendation for artists based on a small sample of data was split
from the test data. The test data is used to predict tempo of the music. Then from the 
dataframe artist is selected whose music is same as the predicted tempo. 





