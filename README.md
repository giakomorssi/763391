# Machine Learning Project

## Title
Customer Segmentation Based on RFM Analysis

## Members: 
Giacomo Rossi - 763391

Flavia Martini - 

Fraia

## Introduction
The aim of this project is to predict the customer segmentation based on the RFM analysis. The RFM analysis is a measure of the frequency, recency and monetary of purchases of the same customer.
We started with an Exploratory Data Analysis with the aim of checking the presence of null values, duplivates and check the distributions of the features. 
We then used the RFM analysis to predict the customer segmentation.
At the end we clustered the customers based on their RFM values obtained before.

## Methods

### EDA

We looked at the distributions of our features and the first thing we noticed was that Customer City, Seller City, Customer State and Seller State had a very long tail.
We needed to transform them into numeric values but the classical encodings were either wrong (LabelEncoder) or needed to much computational costs (OneHotEncoder). We decided to use the TargetEncoder which encodes the categories based on its frequency.
Also other variables such as price, payment_value and fright_value had a long tail and the majority of the value were close to zero.
We decided to dont apply any transformations since the results resulted very different.
We then transformed the order_status, payment_type, product_category_name_english columns with a classical label encoder.
To deal with the datetime object we used the timestamp method to transform them into numbers.
The dataset had no null values, but had 83 duplicated that we removed.
Only tyhe price and the payment_value had an hiugh correlation of 76% but we decided not to remove.

### Market Segmentation
We created 3 features:
- Recency: we found the most recent purchase date as the maximum of the purchase_date column. We then grouped by customer and found the most recenct purchase date and subtracted it from the maximum of the purchase_date column.  
- Frequency: We calculated the frequency of unique items per order for each customerby grouping the data by 'customer_unique_id' and then counting the number of unique values in the 'item_per_order' column for each group.
- Monetary: we grouped by customer and evaluated the monetary by summing the payment values.

### Clustering
We scaled the data with a Standard Scaler.
We used the K-Means algorithm and the Hierarchical Clustering algorithm.
The results were very similar but in terms of computational cost the K-Means algorithm was the best choice.
To choose the best number of clusters we used the elbow method and the KneeLocator algorithm.

## Experimental Design

List here both the Kmeans and the Hierarchical Clustering.
explain the comparison.

## Results
The results are the following:
We identified 5 clusters.
* **Cluster 0: Blue**

  This cluster has the `highest monetary value`, the `2rd highest recency value`, it has the `highest frequency` but it has only `few observations (28)`.

* **Cluster 1: Orange** 

  This is the cluster with the `most recent purchases`, but is has the `lowest monetary value` and the `lowest frequency`. It is the cluster with `the most observations`.

* **Cluster 2: Green**

  This is the cluster with the `highest recency value (longer time since last buy)`, and has the `2nd lowest monetary value` and the `2nd lowest frequency`. It is the `2nd cluster by size`.

* **Cluster 3: Red**

  This cluster has the `3nd lowest recency` and has the `2nd highest monetary value`. It has the `2nd highest frequency` but it has `few observations`.

* **Cluster 4: Purple**

  This cluster has the `2nd highest recency`, it has the `3rd highest monetary value` and it has a `medium frequency`. It has `a medium amount of observations`.


## Conclusions

Decide how and which cluster to target.
