# LinkedIn-post-analysis
```
Analyzing trends in and predicting LinkedIn post performance
```
## 🔍 Background
Unsatisfied with the analytics currently provided to LinkedIn members who use 'Creator Mode', I wanted to get a better idea of the common factors behind my most popular LinkedIn posts, as well as build a simple model to predict which attributes would contribute to the highest views.

## 🔢 Data
Using Naas.ai's template scripts, I scraped data from the 48 posts I've made on LinkedIn. This template was super easy and free to use in the Naas' [virtual environment](https://www.naas.ai)

The full, outputted dataset can be seen in the `LINKEDIN_POSTS_all.csv` file. However, I filtered this dataset down to exclude outliers, specifically posts that I had created very early on, before I was serious about "creating content" on LinkedIn, and my one viral post that gained almost 5x more views than all of my other posts have COMBINED (this [one]())!

Once my data was cleaned and filtered, the resulting final dataset can be seen in the `LINKEDIN_POSTS_updated.csv` file. As you will see in the analysis section below, some visualizations used all posts, while others only used the filtered dataset.

## 🗺 Exploratory Data Analysis
Summary statistics can be shown below for all 48 posts:

![](https://github.com/mhlieu/LinkedIn-post-analysis/blob/fa6f76bfb8a277902b846532eb3a821cf7385bbb/Post%20stats%20table.png)

Views and likes over time, including those for outlier posts, can be seen below. With the viral post included, it is difficult to see details for any other posts:

![](https://github.com/mhlieu/LinkedIn-post-analysis/blob/fa6f76bfb8a277902b846532eb3a821cf7385bbb/All%20views.png)

![](https://github.com/mhlieu/LinkedIn-post-analysis/blob/10f1cfba32c82719c950920c27fbe2a261a9d6a2/All%20likes.png)

Thus, views over time excluding outliers is much more informative:

![](https://github.com/mhlieu/LinkedIn-post-analysis/blob/fa6f76bfb8a277902b846532eb3a821cf7385bbb/Views%20excl%20outliers.png)

![](https://github.com/mhlieu/LinkedIn-post-analysis/blob/fa6f76bfb8a277902b846532eb3a821cf7385bbb/Likes%20excl%20outliers.png)

The same case applies to an analysis of the top 5 most viewed posts (and their titles):

![](https://github.com/mhlieu/LinkedIn-post-analysis/blob/fa6f76bfb8a277902b846532eb3a821cf7385bbb/Most%20viewed%20all.png)

So the same chart without the outlier viral post is shown here:

![](https://github.com/mhlieu/LinkedIn-post-analysis/blob/fa6f76bfb8a277902b846532eb3a821cf7385bbb/Most%20viewed%20excl%20outliers.png)

The relationship between views, comments and likes can be seen in the below 3d scatter plot. For presentation purposes of this plot, the TWO most popular posts were removed because even the second-most popular post had almost 150k views--including this would have caused almost all other points to still be heavily concentrated in the bottom left corner of the plot, and thus was removed too.

![](https://github.com/mhlieu/LinkedIn-post-analysis/blob/fa6f76bfb8a277902b846532eb3a821cf7385bbb/Views%20comments%20likes.png)

Lastly, I wanted to get an idea of the most common words used in my posts through the use of a Wordcloud:

![](https://github.com/mhlieu/LinkedIn-post-analysis/blob/fa6f76bfb8a277902b846532eb3a821cf7385bbb/Word%20cloud.png)

## 📈 Predicting Post Performance using Linear Regression
Linear regression was the model chosen because we are predicting a continuous variable using independent variables that are also continuous. The four independent variables selected were number of characters, number of emojis, likes and comments, and these were used to predict the target variable of views on each post. The major assumption made here is that likes and comments on a post cause the algorithm to show one's post to more people in your network and beyond. In reality, I acknowledge a post can't receive any likes or comments without receiving views first, so this is a simplifying assumption.

The coefficients of the resulting model can be seen here:

![](https://github.com/mhlieu/LinkedIn-post-analysis/blob/fa6f76bfb8a277902b846532eb3a821cf7385bbb/Regression%20model.png)

The interpretation of this model is that on average, each additional character will result in 9.2 views, each emoji DECREASES views by 514.2 views, each comment increases views by 15.7 and each like contributes to 120.1 views, when we start at an intercept of -7389 views.

These coefficients can be confirmed when we run an OLS model as shown below, and this also shows that our linear regression model explains 96.5% of the variability observed in the target variable, views, based on the R^2 score.

![](https://github.com/mhlieu/LinkedIn-post-analysis/blob/fa6f76bfb8a277902b846532eb3a821cf7385bbb/OLS%20Results.png)
