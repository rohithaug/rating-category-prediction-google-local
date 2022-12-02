# Understanding the interplay between rating and category for restaurants in Google Local Review

## Table of contents:
1. [Collaborators](#collaborators)
2. [Abstract](#abstract)
3. [Dataset](#data)
4. [Predictive Task](#task)
5. [Experiments and Results](#results)
6. [Conclusion](#conclusion)
7. [Future Scope](#future)

## Collaborators <a name="collaborators"></a>
* [Prasannakumaran Dhanasekaran](https://www.linkedin.com/in/prasannakumaran/)
* [Aakriti Kedia](https://www.linkedin.com/in/aakriti-kedia/)

### Abstract: <a name="abstract"></a>
With the ever-increasing demand for a spontaneous response for queries raised by users, the need for robust systems to predict outcomes is imperative. The modern world powered by the internet has a high impact on the lives of people on a day-to-day basis ranging from internet searches to suggesting products on ecommerce websites. Consequently, online review forums and blogs act as a critical factor for a user to choose an outcome. In recent times, people tend to evaluate a business based on the reviews it has received on Google. The task of personal or relevant recommendation and determining the ratings or quality of business based on the engagements is the need of the hour. In this work we propose an experiment on how information from multiple points of interests such as restaurant information, GPS, user review sentiments could contribute to the task of rating prediction and suggesting personalized cuisines. We conduct experiments on the Google local reviews dataset. Our proposed strategy exhibits less than 11% inaccuracy in the prediction task, thus showing the effectiveness of the feature extraction strategy.

## Dataset: <a name="data"></a>
In this project, we perform analysis and modeling on the [Google Local Reviews Dataset](https://doi.org/10.1145/3109859.3109882). This dataset consists of a large collection of users, places and business reviews and rating. In this work, we evaluate datasets containing restaurants.

## Predictive Task <a name="task"></a>
We will predict the rating of a user for a restaurant given the features and predict the most likelihood category for a given user. The predictive task
is divided into two subparts as follows

1. Ratings Prediction:

This involves predicting the rating of a place based on ‘Rating’, ‘Categories’, and ‘Price’ feature inputs to the model. 𝑌 = {1, 2, 3, 4, 5} denotes the predictions made by the proposed model where each value indicates the rating given by the user. Given U, P, and R, this work aims to determine the ratings provided by the user as illustrated in the equation: 𝐹: ∆(𝑈,𝑃, 𝑅) → 𝑌𝑟

2. Categories Prediction:

We also try to find similarities between different existing ‘Restaurant’ categories and trying to recommend the user a category which best suits his taste based on his history of places visited, using ‘Rating’, ‘Categories’, and ‘Price’. The predicted category would still be of ‘Restaurant’ type and has 40 possible values. Let the preferred place category for the user recommended
by the model be represented as 𝑌𝑐 = {'American Restaurant', 'Asian Restaurant'}. Mathematically, Given U, P, and R, this work aims to determine the preferred categories of the user as illustrated in the equation: 𝐹: ∆(𝑈,𝑃, 𝑅) → 𝑌𝑐

## Experiments and Results <a name="results"></a>

### 1. Rating Prediction
The objective of this work is to predict the ratings of the restaurant based on its features and the reviews it had received from users who visited the restaurant. For carrying out the experiments we implement machine learning models on the dataset. We did not consider using deep learning models such as Recurrent Neural Networks (RNNs), Artificial Neural Networks (ANNs) in this work
since they perform better than machine learning models when the dimensionality of the data is high. In this work, we implemented linear model algorithms such as Linear Regression, Lasso Regressions and Ridge Regression. We also implemented Random Forest Regressor to test out the performance of ensemble methods on this data.

**Unsampled Data Results:**

| Model  | RMSE | MAE |
| ------------- |:-------------:|:-------------:|
| Linear Regression | 1.044 | 0.855
| Lasso Regression | 0.859 | 0.677
| Ridge Regrssion | 0.780 | 0.599
| Random Forest Regrssion | 0.759 | 0.581

**Over-sampled Data Results:**

| Model  | RMSE | MAE |
| ------------- |:-------------:|:-------------:|
| Linear Regression | 1.231 | 1.044
| Lasso Regression | 0.876 | 0.706
| Ridge Regrssion | 0.843 | 0.645
| Random Forest Regrssion | 0.836 | 0.648

**Under-sampled Data Results:**

| Model  | RMSE | MAE |
| ------------- |:-------------:|:-------------:|
| Linear Regression | 1.231 | 1.044
| Lasso Regression | 0.886 | 0.723
| Ridge Regrssion | 0.857 | 0.661
| Random Forest Regrssion | 0.849 | 0.650

Since we are focused on minimizing error rate, a low RMSE and MAE is desirable. From the above tables, we can infer that the results of both over-sampled and under-sampled data are similar and do not show any improvement. In fact, the model trained on unsampled data performs better than the sampled ones. Unsampled data with random forest regressor gives a RMSE of 0.759 and MAE of 0.581. On the other hand, sampled data run on the same algorithm gives an RMSE of 0.836 and 0.648. Out of the models run, unsampled data Random Forest Regressor performed the best. With an RMSE of 0.759 and MAE of 0.581, and given that the target ratings range from 1 to 5, the error rate relative to the range is 11.62%. Linear models with regularization perform better than non-regularized linear regression models as they regularize the parameters and force the weights of the uninformative features close to or exactly zero (L2 and L1 respectively). Thus, tree-based regression models perform best on this dataset

### 2. Category Prediction
The objective of this task is to predict the top preference categories of the user based on features like ‘Rating’, ‘Sentiment score’, ‘Price’. As part of experiments, we tried to one-hot encode the available categories and find similarities between them by using methods of clustering like k-means clustering and recommend categories which fall within the same cluster. We also experimented with Regression methods like Logistic Regression by considering the categories as multi-classes. Finally, we introduced personalization in these predictions by using SVD models and used variations of ratings and categories probability received from the Logistic Regression model to determine the top preferred categories of the user. Additionally, we also used a mathematical model which could be used for predicting startup ideas for categories no present within a determined ‘x’ km radius.

## Conclusion: <a name="conclusion"></a>
We performed a predictive task of rating prediction of a user for a item with linear and tree based models with and without sampling. We also predicted top categories likelihood prediction for a user using various traditional machine learning models such as clustering and regression and other collaborative filtering and mathematical models. We evaluated the rating prediction task using
standard metrics such as Root Mean Squared Error (RMSE) and Mean Absolute Error (MAE) and found that the random forest regression model performed the best on unsampled data. The category prediction task was evaluated with custom matching of the predicted categories. Both the models seem to give convincing results. The performance of both the predictive task can be improved by better engineering additional features and by incorporating better modeling strategies.


## Future Scope: <a name="future"></a>

1. Incorporate dimensionality reduction techniques to improve the modeling for rating prediction.
2. Take time into consideration when predicting, i.e., if there is a trend of declining ratings, or negative sentiments in recent reviews, penalize this restaurant and avoid recommending it and suggest a startup idea of this category. The unix timestamp available in the review dataset can be used for this. 
3. Evaluate the performance of the category prediction model on other datasets such as yelp and compare the accuracy.
4. Evaluating the impact of timing of the restaurant on category prediction for the user.

## Thank you!

I hope you found the project useful and interesting. This project was developed as part of the [CSE 258 class](https://cseweb.ucsd.edu/classes/fa22/cse258-a/) offered Prof. Julian McAuley in Fall 2022 at UCSD. Find the copy of the complete report [here](https://github.com/rohithaug/rating-category-prediction-google-local/blob/main/report.pdf) for reference.

-- [Rohith S P](https://www.linkedin.com/in/rohithsp/)
