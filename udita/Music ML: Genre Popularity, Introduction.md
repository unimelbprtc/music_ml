
# Introduction of Machine Learning, Assignment 2

Humans are born with musicality. Infants can mimic tunes well before they strat to walk or crawl.
Music provides us a unique way to communicate our emotions ranging from deep regret to euphoric joy
with others, even when we do not understand the language.
Thus, music is the most popular form of art. 
Music is also most digitized art, which aided in it's spread and reach. Music is diverse, in its innate elements like rhythm,
melody, lyrics, to the human context like language, national origin, and popularity.
The survey of participation in the arts show 42% of adults in the USA attended live music performances [1]. 
Victoria's own National Arts Participation Survey show 90% of Victorian listen to recorded music and 46% attended
live music [2]. 

Due to the massive popularity, reach and diversity of music, it is a great challenge to classify the attributes
in the music information retrieval.
In our study we wanted to find if the audio attributes of music can help us predict the human interest like popularity,
genre and similarity via explorative data analysis and classification model learning.
Our motive for the analysis were to find out the best ways to clean data, select the optimal set of features for 
different target labels, and tune the set of hyperparameters for the best-fit models. 

Spotify is the leader in digitized music delivery platform with more than 100 million songs. We leveraged the  
audio attributes published by Spotify for our current study. These attributes are Danceability, Energy, Loudness ,
Speechiness ,Acousticness, Instrumentalness ,Liveness ,Valence ,Tempo [3]. We leveraged the data published via
Kagglehub[6], which is one of the largest host of opensource data and analysis.

In the start, we focused keenly on data pre-processing. Many data points showed high degrees of
correlatedness, like Energy and Danceability, thus lack of independence needed to be combined to increase 
predictive capabilities of the models. We furtehr delved into enrich the data by 
feture reduction, normalization and deletion to render a dataset which can be consumed by the models. 
We leveraged multiple performance metrics like accuracy, confusion metrics and cross-validation to evalute the models.
Random Forest Search and Stacked Ensembing were used and cross validated against non-ensemple methods like KNN, 
Decision Tree to verify hypothesis around fetaure dependency and model selection.
Finally, we used hyperparameter tuning and ensemble method to choose the optimal parameters for the best-fit models for the
selected set of features and labels. 

1. U.S. Patterns of Arts Participation: A Full Report from the 2017 Survey of Public Participation in the Arts; https://www.arts.gov/sites/default/files/US_Patterns_of_Arts_ParticipationRevised.pdf
2. National Arts Participation Survey; https://creative.vic.gov.au/resources/audience-participation-survey
3. https://developer.spotify.com/documentation/web-api/reference/get-audio-features
4. Duman, D., Neto, P., Mavrolampados, A., Toiviainen, P., & Luck, G. (2022). Music we move to: Spotify audio features and reasons for listening. PloS one, 17(9), e0275228. https://doi.org/10.1371/journal.pone.0275228
5. https://www.kaggle.com/datasets/thedevastator/spotify-tracks-genre-dataset
6. https://www.kaggle.com/datasets/vicsuperman/prediction-of-music-genre
