
# Introduction of Machine Learning, Assignment 2

> Prepared by Udita Bose

This document describes the method and conclusion for the research question
_Recommendation of artist based on selected feature using KNN, Decision Tree and Neural Network_.

Feature selected for recommendation is Tempo. 
The tempo in the dataset is numeric (float) in value but stored as string. 
The value ranges from _30_ to _220_.
In its raw form it is a continuous numeric data. For the analysis purpose,
we converted into binned categories, ranging from low to very high.
The bar, count and scatter plots during data exploration show that lower tempo
musics are correlated with lower in tempo. The highest tempo music are most danceability.

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





