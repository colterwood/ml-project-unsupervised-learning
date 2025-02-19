# machine_learning_project-unsupervised-learning

## Project Goal
- To build an unsupervised learning model that helps us gain valuable insights into the wholesale sales data provided.
- I tested multiple models: KMeans Cluserting, Hierarchical Clustering, and PCA 
## Process:
### 1. Import data from Wholesale_Data.csv
### 2. Clean up data:
   - The data was pretty clean out of the box, I chose to standardize the data because of the models we were using and the vast disparity between client size. I also did not want to remove outliers because all of this data is real customer sales data and relevant to the overall picture for this wholesaler.
### 3. Visualize the data
   - We ran a number of different visualizations to get an idea of how the data was distributed and also how it was correlated.
   ![Histograms of All Variables](visualizations/histograms.png)
### 4. Feature Selection
   - I found that 'Grocery' and 'Detergents_Paper' were highly correlated, as you can see in the correlation heatmap, so I chose to remove 'Detergents_Paper' due to multicollinearity.
   - Next I ran a PCA to see if any features had low variance and I found that 'Delicassen' had essentially a 1% variance, so I removed that as well.
   - I landed on using 'Fresh', 'Milk', 'Grocery', and 'Frozen' as my features for model testing and building.
### 5. Model Testing & Evaluation
   - As mentioned, I tested 3 different models: KMeans Clustering, Hierarchical Clustering, and PCA
   - For KMeans, through Silhouette score, I determined that 3 was the most appropriate number of clusters to model on. 3 had the highest Silhouette Score and when I increased the clusters I ended up with clusters that only contained a few customers.
   - Hierarchical Clustering was equally unclear by visualization alone, so I ran Silhouette scores again and found 5 clusters had the highest Silhouette Score. Once again, having 5 clusters resulted in 2 very small clusters that felt relatively unuseul. Not because clusters this small cannot be relevant, but because the customers were not that similar inside those clusters, they just happened to be far away from the more dense clusters. I also ran a Cophenetic Correlation Coefficient evaluation on this model, which came back quite low at 0.4070.
   - Lastly, I ran a Principal Component Analysis model. It was determined that using 3 of the four Principal Components was all that was necessary, as they accounted for nearly 94% of the variance. I also verified that PC1 was important to explaining the variance, and it was determined that PC1, PC2, and PC3 were necessary. PCA also resulted in 3 clusters after running Silhouette Scores to verify the visualizations.
   
## Results:
### Silhouette Scores
K-Means: 0.5188 (k=3)
PCA: 0.4854 (k=3)
Hierarchical Clustering: 0.3136 (k=3)

### Davies-Bouldin Index
K-Means: 0.9218 (k=3)
PCA: 0.7693 (k=3)
Hierarchical Clustering: 0.9218 (k=3)

### Calinski-Harabasz Score
PCA: 206.7866 (k=3)
K-Means: 157.9444 (k=3)
Hierarchical Clustering: 157.9444 (k=3)

### Based on the results above I prefer PCA, slightly above K-Means, because it is consistently providing the best results. 

## Our clusters (customer info):
### Cluster 0: 
Balanced Customers (Majority)

#### -Business Application:
    -Standard marketing efforts apply here.
    -Could be targeted with bundled discounts across categories.

### Cluster 1: 
High Frozen & Fresh, Low Grocery & Milk

#### Business Application:
    -Likely restaurants, food service businesses, or meal prep companies.
    -Marketing Focus: Bulk discounts on fresh produce & frozen foods.
    -Inventory Planning: Ensure reliable supply chain for perishable goods.

### Cluster 2: 
High Grocery & Milk, Low Frozen & Fresh

#### Business Application:
    -Likely retail stores, large-scale distributors, or supermarkets.
    -Marketing Focus: Promotions on bulk grocery and dairy.
    -Inventory Planning: Maintain high availability of shelf-stable products.

## Challenges:
- Ideally I could spend a bit of time with the customer to determine those outlier clients and if maybe they are best suited as fourth and/or fifth clusters. 

## Future Goals:
- To understand the wholesaler and its clients better
- To understand the models better to have more confidence that narrowing to 3 clusters is the right decision, rather than going with a higher cluster count even though two of the clusters just contained 3 and 4 customers respectively.
