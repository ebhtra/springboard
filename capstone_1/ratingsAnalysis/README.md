## These notebooks contain various analyses of the Untappd ratings  

<b>Results.ipynb</b> takes a look at the checkins from a few different angles:  

1) It models them as a networkx bipartite graph with Users as one partition and Beers as the other, with ratings as edges.  The networkx methods available on that resulting graph, such as diameter(), turn out to take too long to run, due to the graph size, so I just used my own graph representation to calculate the sparsity of the User-Beer-Rating graph (It's very sparse).

2) It attempts to use the Surprise library to apply SVD and K-Nearest Neighbors to the ratings in order to predict unseen ratings.  Both of these approaches fail to compete with an educated baseline estimate that's calculated by simply adding the user's mean bias to the mean overall rating for the beer.  The KNN in particular underperforms, which suggests that the graph is simply too sparse for such analysis.

3) An attempt is made to calculate Pearson similarities for pairs of users and to adjust the educated baseline predictions slightly, where justified.  After much parameter tuning, any tiny improvement upon the baseline appears to be just overfitting the parameters to the test batch.

<b>Results_2.ipynb</b> uses sklearn's GradientBoostingRegressor to attempt to beat the baseline predictions, but the only features that turn out to have any importance are alcohol content and global rating of the beer.  

<b>DescriptionNLP.ipynb</b> uses sklearn's SGDRegressor to find correlations between the terms used in beer descriptions and ratings.  The learned weights can help predict global ratings for new beers.  For models trained on individual users, however, the known global rating of the beer is still the best predictor, at least until the user has rated over 150 beers, at which point the descriptions can begin to help the predictions.  The way they can help at this point is shown in <b>FrequentRaters.ipynb</b>, where the rank accuracy of recommendations begins to beat the baseline accuracy.  

<b>Mile_2.ipynb</b> revisits Pearson similarities between user pairs and finds that with enough commonly-rated beers, user similarity can improve the recommendations.  This notebook uses an online learning method for every Pearson number, where a large dictionary stores the components of the Pearson calculation needed to update each number every time one of the users rates a new beer.  <b>Mile3.ipynb</b> is mostly the same, except that it just uses scipy stats' Pearson function to calculate each similarity.

The other notebooks in this directory are just used for reports which incorporate the above notebooks and comprise pieces of the overall project.



