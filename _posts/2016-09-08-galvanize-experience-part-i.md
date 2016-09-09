---
layout: post
title:  "My experience at Galvanize Part I"
date:   2016-09-08
---
For the past few months, I've been attending the Galvanize Data Science Immersive program. In my time there I've met a lot of very cool people and worked hard and learned a ton. These blog posts will be an effort to describe many of the things that I've learned through my experience at Galvanize.

### Week 1
For our first week, we covered a lot of basic programming concepts in python and SQL.

We started off the week covering basic ideas of programming in python; the first day we covered test-driven development and worked on a pair assignment to clean up inefficient code so that it could run faster. So for example, one of the functions takes as input a text file and a dictionary of words, and outputs a list of words that are in the file but not in the dictionary. By simply using sets instead of lists to build up the set of words, we were able to reduce the runtime from 20.6s to 13.2ms. Pretty efficient! The next day we covered Object Oriented Programming, and making objects in python. This day's pair assignment had us building a Blackjack game. Here's an example of the output when you run the program:

```cli
python blackjack.py
Play a round? yes
What is your bet? 20
Your cards are [6d, 10d]. Your cards are worth 16 points.
The dealer is showing Qh.
Hit or stay? hit
Your cards are [6d, 10d, 7d]. Your score is 23
You lost! You lost 20 dollars, and now have 180 dollars.
You finished with 23 points.
The dealer finished with 20 points.
Play a round? no
You ended with 180 dollars.
```

Next, we covered SQL. We used PostgreSQL for our basic SQL assignments, and practiced increasingly complicated SQL queries. We also used the `psycopg2` module in python to write a script that creates a SQL pipeline to create a 'daily snapshot' table of users and activity for a social media site.

We ended the week covering some basic data frame work in `pandas`. Having previously practiced a lot in R, pandas felt right at home for me. We also had a weekend assignment to practice using `pandas`, `matplotlib`, and `seaborn`. The pandas practice had us doing some moneyball-type analysis of baseball contracts, which was pretty fun. While it was good to get some practice with matplotlib and seaborn, I'm glad that I will (hopefully) never have to use them again now that the program is over; R's plotting packages are significantly better and more intuitive to use, and have much better documentation.


### Week 2
Week 2 was probably my easiest week. This week was a statistics week, so many of the concepts that we covered were review for me.

Most of this week was covering a lot of basic things you'd learn in a college-level statistics class, like basic probability (frequentist and Bayesian), sampling, and hypothesis testing. My favorite part of the week, however, was something completely new for me; on the last day we covered the multi-armed bandit problem.

The multi-armed bandit approach is a way to deal with a few problems that come up with normal hypothesis-based A/B testing. First, with normal hypothesis testing, you can only test out one thing at a time, as you either prove or disprove some underlying hypothesis. Second, if you spend all of your time hypothesis testing, it can take many trials to converge towards a significant effect, at which point you've spent too much time and resources running an experiment, where you've devoted too much time to a sub-optimal strategy. The multi-armed bandit approach alleviates both of these problems with Bayesian updating. It starts by running as many experiments as you need, randomly sends a single trial to one of the versions of the experiment, updating the hypothesized values for each version based off of the results, and then tries to send more and more trials to the highest performing version. For our exercise we tested out several different methods to minimize regret (the amount of time spent on a sub-optimal strategy), such as epsilon-greedy, softmax, ucb1, and bayesian bandits.  


### Week 3
Week 3 was when we got into some actual modeling. This week covered different topics in regression. We started off by learning about basic OLS models. This required a little bit of background in linear algebra, so we began by getting some practice with matrix operations in `numpy`, then built our own regression models and learned about troubleshooting some common problems in regression, like dealing with multicollinearity and examining residual plots for normality and heteroskedasticity.

Once we had the basics down, we learned about model tuning. In picking and building your model, you always need to keep in mind the bias-variance tradeoff. If your model is too simple, then it will be a high-bias model and won't capture enough of the signal to perform very well. With an overly complex model, you the variance will increase, and you are prone to overfitting; your model will learn all of the noise in the training data and then underperform on the test data. Cross-validation is the best way to search for the right balance. Cross-validation is a way to get an estimate of your out-of-sample error by holding out a portion of your data and using that as a 'test' set before you actually run your full model on the actual test data. You can hold out one portion as a validation set, iterate through every point in your data in the leave-one-out approach, or iterate through several distinct hold out sets in k-fold cross-validation.

After learning about these tuning methods, we put them to use in our exploration of lasso and ridge regularization methods. These regularization methods are techniques used to shrink the coefficients in our regression models. There are a few reasons you might want to do this. Doing so will help reduce the variance in your model to prevent overfitting. If you have very sparse data where many of the features are unimportant, then regularization will help reduce the effect of these noisy variables (in the case of lasso it can completely eliminate unimportant features). Regularization can also help deal with influential data points. Sometimes outliers can strongly affect the coefficients of your model; through regularization you shrink your coefficients, which can help alleviate some of the problems caused by these influential points. Regularization techniques work by introducing a penalty on the cost function used to train your model. Normally OLS trains by minimizing the sum of squared residuals as its cost function (OLS stands for ordinary least squares), but regularization introduces the coefficients themselves into the cost function, ensuring that large coefficients are penalized in the model.

Next, we were introduced to binary classification techniques through logistic regression. Logistic regression works similarly to OLS, but puts the regression output into a sigmoid function, so that all predictions are between 0 and 1 (and thus can be used as an estimate of the probability of being in a certain class). We also learned about setting different thresholds for classification, and how to examine an ROC curve to consider the tradeoffs between the sensitivity and specificity of a model.

We finished the week off by learning about gradient descent, which is used to train these models. With gradient descent, you are looking for a global minimum of your cost function by initializing your model with a guess at the coefficients, and then traveling along the steepest descent of your cost functions gradient (the partial derivatives of the cost function with respect to each of the model's coefficients).


### Week 4
In week 4 we learned about some supervised learning methods for classification purposes. Supervised learning is building machine learning models where your target variable is labeled ahead of time in your training data; so say if you have a dataset where that has classified transactions as to whether they're fraud events, and you want to use that to predict whether future transactions are fraud events, you would use supervised learning methods.

To start the week we learned about k-nearest neighbors. This algorithm is very simple and intuitive. To classify a single data point, you look at how a certain number of the closest data points are classified, and then set your prediction to the majority class of its nearest neighbors.

That same day we learned about decision trees. Decision trees are also fairly intuitive, as they are representative of how a person might think about predicting some sort of event. Decision trees look for optimal splits to make based off of what split gives the most information. Let's say I want to predict whether people will be playing basketball at the park. I know ahead of time that if it's raining, no one every plays, and if it's over 90 degrees outside, then there's a 20% chance people will be playing. First, I'd check to see if it's raining outside, since that is a stronger indicator, then if it isn't I would look at the temperature. Decision trees continue to split the data based off what provides the most information (there are a few different methods to determine this), until it's reached some sort of stopping criteria.

While single decision trees are not used very frequently anymore, they are important to build the intuition behind a lot of ensemble learning methods that are used. Next, we learned about bagging and random forests, which are methods to ensemble the results of many different decision trees. Single decision trees can be prone to overfitting, so these methods are ways to reduce the variance of a model while keeping bias low. With bagging, you train many different trees using a bootstrapped sample, meaning that you sample from the data with replacement, and then make predictions based on what the majority of trees predicts for that data point. While this can be somewhat effective, over time if you train enough trees, if there is any systematic bias in your training set, most of your trees will continue to make the same mistakes. This is where random forests comes into play. To decorrelate the different trees, in addition to the bootstrapped sampling, random forests also takes a random subset of the features to calculate the best split at each node for each tree.

Next, we learned about support vector machines (SVM). The SVM is a maximal margin classifier which tries to create a separating hyperplane to separate the different classes of points with the largest amount of separation, or margin, possible. While this generally works with linearly separable data, it can also be extended into non-linear data, by using a kernel function to map the data into a higher-dimensional space and find a separating plane there.

We then learned about boosted tree models. Boosted trees are another ensemble method similar to bagging and random forests, however boosted models build their trees based off of the errors of previous trees, and thus must be built sequentially. Boosted tree models build the next tree by looking at how the previous tree performed, and adjusting based off of the errors that the previous tree made.

We finished the week off by trying to put some of these models into a more realistic context. We worked on building profit curves for our models, which helped us think about what we want our models to do in specific contexts. Sometimes you might want to optimize for things other than just pure accuracy, such as precision or recall, depending on the goals of the business and what kind of costs are associated with different errors. We also learned about methods to deal with imbalanced classes, such as undersampling, oversampling, and SMOTE, which is important because many real world problems are not going to have nicely balanced data.


### Next time
I had originally intended for this to be one post that described everything that I did at Galvanize. This has gotten very long already, and I haven't even gone into nearly as much detail as I would have liked, so I will split this into two blog posts and post the second half tomorrow.
