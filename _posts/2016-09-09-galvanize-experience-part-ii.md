---
layout: post
title:  "My experience at Galvanize Part II"
date:   2016-09-09
permalink: pretty
---
This is the second part of a two-part description of my time in Galvanize's Data Science Immersive program. [You can find part one here.](/2016/09/08/galvanize-experience-part-i)

### Week 5
Week 5 was somewhat of a grab-bag of different topics.

We began the week covering web scraping. Python's awesome `BeautifulSoup` package made scraping web sites extremely easy. We also covered some basic HTML and CSS, since that is essential to using BeautifulSoup to scrape data directly from websites.

Web scraping can be a great way to get information, but then how do you store it? Unfortunately, the information that you get may not be standardized in a way that can easily fit the schema of a SQL database. That's where NoSQL databases come into play. We learned about MongoDB and its corresponding python client, `PyMongo`, for this purpose.

On Tuesday we covered topics in natural language processing. This was an interesting day because the instructors tried out a different method, called a 'flipped classroom,' where we studied the concepts ahead of time, and our class was mostly discussion/talking through a lot of the concepts that we learned. We learned about using Naive Bayes for classifying documents, and about feature extraction and processing of text documents using concepts like stemming, lemmatization, and tf-idf vectorization.

Wednesday we had our first case study. We split into groups of four, and analyzed a dataset for a ride-sharing service to predict churn. Working through a (semi-) real world example was both challenging and rewarding, and I definitely learned a lot about the considerations you need to make for a real world problem, and how to work in the context of a team. While we fell into the trap of spending a little too much time cleaning the data and engineering features, we were able to train a decent random forest model which had high recall (we wanted to maximize recall under the assumption that missing out on a churn prediction would be more costly than misclassifying a customer who wouldn't churn) while still maintaining decent overall accuracy, and extracted some of the important features to help inform business decisions.

Next, we focused on time series analysis. I had done some time series analysis before in undergrad for my econometrics classes. The point of time series analysis is to make your data stationary by accounting for any long-run and seasonal trends.

We finished off the week with an introduction to unsupervised learning by covering a couple of different clustering methods. With unsupervised learning, you do not have labeled training data, so your machine needs to uncover some hidden structure within the data. Clustering techniques, as the name implies, finds structure by clustering proximal data points together. On this day we covered k-means and hierarchical clustering. K-means clustering is a pretty cool algorithm; the basic process is to randomly assign each data point to one of k classifications, compute the centroid of each classification, reassign the data points to the closest centroid, and then repeat these steps until there is no change in cluster assignment. With hierarchical clustering, you work your way from the ground up by clustering the closest data points together into a group, then clustering groups together until you've clustered all of the data points together.


### Week 6
For week 6, we went further into unsupervised learning topics.


### Week 7
Week 7 was devoted to covering Big Data topics.

The first day gave a broad overview of what you can do on Amazon Web Services, and covered multiprocessing and threading to parallelize computing processes. 


### Week 8
Week 8 was the final week of structured curriculum.


### Project
For the last few weeks of the program, we worked on our projects. We spent two weeks working on the projects, and then a week practicing presentations for our projects.

My project was to create a news summarizer. It uses web scraping to pull popular news articles from the web, and natural language processing techniques to extract the most important sentences from the article to create summaries of each article. It then takes these summaries and puts them into an automated email newsletter. You can see the project at [brief-news.info](http://brief-news.info).

For a more detailed overview of my process to create the summarizer, you can see my project's about page [here](http://brief-news.info/about).

At the end of the week, we had a "Capstone Showcase" day where we presented our projects to some potential employers, and got a chance to network with some of them afterwards over lunch.


### Wrapping up
Once we were finished with the projects and presentations, we had one more week which was focused on preparing for interviews. We talked a little bit about the structure of the interview process and what to expect, and practiced some problems that we might face in take-home tests and had a few practice interviews.

My time at Galvanize was a very enriching experience, and now I feel qualified to go out into the world and put these newfound skills to use!
