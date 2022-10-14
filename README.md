# Cryptocurrencies (Unsupervised Machine Learning)

## Overview 

Unsupervised Machine Learning is used when one wants to machine learning algorithms to analyze and cluster unlabeled datasets. Essentially, unsupervised ML is used when one is unsure of the question to ask of the data at hand, for instance, whether the data can tell us anything useful, or tell us something that might not have been obvious at first. Unsupervised ML is different from supervised ML because the model uses a whole dataset as a whole, and there is no paired inputs and outcomes set when creating the model. 

Clustering is a technique used in ML, in which unlabeled data is grouped based on their similarities or differences. PCA, or Principal component analysis, is a type of dimensionality reduction algorithm, which reduces redundancies and compresses datasets through feature extraction. Clustering is used in unsupervised ML because clustering will determine patthens in a grouping of data, as opposed to just predicting a classification, like what is commonly seen in some supervised ML techniques. 

This project focuses on using unsupervised machine learning(UML) to create a report that shows what cryptocurrencies are on the trading market, and how they might be grouped into a classification system for new investment for customers doing business with investment banks. Unsupervised machine learning was used for this project versus supervised machine learning, because there is no known output for what cryptocurrencies will be on the trading market. In order to group the cryptocurrencies into a classification system, a clustering algorithm was used. 

## Resources & Libraries

* Anaconda (Jupyter Notebook)
* Python 3.9
* Pandas 
* Plotly
* Sklearn
* HvPlot 
* Pathlib 
* Dataset: [crypto_data.csv](https://github.com/Lucky777b/Cryptocurrencies/blob/main/Resources/crypto_data.csv)

## Results 

***1. Preprocessing the Data for PCA***

![Preprocess Data](https://github.com/Lucky777b/Cryptocurrencies/blob/main/Resources/cluster_cryptoDF.png)

* In order to preprocess the data for PCA, the 'IsTrading' column was dropped, rows that contained at least one null value were dropped, and the crypto_df was filtered to only have rows where coins were mined. A new dataframe was created to hold the cryptocurrency names, which used the same index as the crypto_df, so that the new dataframe can be reincorporated back in after running the model. Finally, the column 'CoinName' was removed since it was not going to be used on the clustering algorithm.

![Text Features](https://github.com/Lucky777b/Cryptocurrencies/blob/main/Resources/text_features.png)

* Using the get_dummies() method, variables were created for text features, 'Algorithm' and 'ProofType', and this was stored in a new dataframe named 'X'. 

![Fit Transform](https://github.com/Lucky777b/Cryptocurrencies/blob/main/Resources/fit_transform.png)

* Then, the StandardScaler fit_transform() function was used to standardize the text features created in the 'X' dataframe.

***2. Reducing Data Dimensions Using PCA***

![PCA](https://github.com/Lucky777b/Cryptocurrencies/blob/main/Resources/PCA.png)

* Using the PCA algorithm, I was able to reduce the dimensions of the 'X' dataframe into 3 principal components, and then these dimensions were placed into a new dataframe, 'df_crypto_pca'. These new dimensions were labeled: 'PC1', 'PC2', 'PC3', and also has the same index from the 'crypto_df' dataframe.

***3. Clustering Cryptocurrencies Using K-means***

![Elbow Curve](https://github.com/Lucky777b/Cryptocurrencies/blob/main/Resources/elbow_curve.png)

* In order to find the best value for K from the 'df_crypto_pca' dataframe, an elbow curve was created using hvPlot. Based on the hvplot above, it was determined that K=4 was the appropriate choice, which means that the data will be broken up into 4 cluster groups. 

![KMeans](https://github.com/Lucky777b/Cryptocurrencies/blob/main/Resources/K_means.png)

Then the K-means model was initiated, and after fitting the model, I was able to put the 'df_crypto_pca' dataframe into the model and make predictions for the 4 clusters. Using these predicted clusters and the cryptocurrencies features, a new 'clustered_df' dataframe was created, in which I could then concatenate the 'crypto_df' and 'df_crypto_pca' dataframes into one table, as shown above. I used the same concatenation function to reincorporate the 'CoinName' column dropped earlier with the 'crypto_names_df', created in step 1. 

***4. Visualizing Cryptocurrencies Results***

![HVPlot](https://github.com/Lucky777b/Cryptocurrencies/blob/main/Resources/3Dscatter_clusters.png)

* Using the scatter_3d() function, PCA data and the predicted clusters were used to make the 3D-scatter plot containing three features, for example, 'PC1', 'PC2', 'PC3'. This plot shows where each clustered cryptocurrency is, in relation to, the 3 principal components. The 'CoinName' and 'Algorithm' colums were added to the 'hover_name' and 'hover_data' parameters, so that the data points in the plot would show the coin name and algorithm when hovering over the data point.

![Tradable Table](https://github.com/Lucky777b/Cryptocurrencies/blob/main/Resources/tradable_cryptoTable.png)

* Using the hvplot.table() function, A table was created that contained data for the tradable currencies, and which of the 4 cluster classes that cryptocurrency coin name was classified into. 

![Scaled Data](https://github.com/Lucky777b/Cryptocurrencies/blob/main/Resources/clustered_df_scaled.png)

* I used the MinMaxScaler().fit_transform method to scale the columns, 'TotalCoinSupply' and 'TotalCoinsMined', between the given range of zero and one. A new dataframe was created, which could then be used to create the 2D-scatter plot shown below. 

![Scatter Plot](https://github.com/Lucky777b/Cryptocurrencies/blob/main/Resources/plot_df_scatter.png)

* An hvplot.scatter plot was then created with 'TotalCoinsMined' displayed on the x-axis, and 'TotalCoinSupply' displayed on the y-axis. The 'CoinName' column was added to the 'hover_cols' parameter, so that the cryptocurrency coin name would show when hovering over each cluster data point.

![hvScatter](https://github.com/Lucky777b/Cryptocurrencies/blob/main/Resources/hvPlot_scatter.png)

* When hovering over the data points in this scatter plot, there are two observed outliers: 'BitTorrent Crypto', which shows that it has a lot of coin supply and a lot of coins mined; and 'TurtleCoin', which has high coin supply but low coins mined. 
* The cryptocurrency coin names that seem to be most profitable are the 2 cluster class groups that show less coin supply and coins mined in comparison to the other groups. 
 