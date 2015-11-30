# Personal Solutions to Chapter 1 of Fundamentals of Machine Learning for Predictive Analytics

## 1. What is *predictive data analytics*?

Predictive data analytics is a branch of data analytics that is concerned with
gaining insights from current data to make predictions about future unseen
data. It generally consists of understanding the questions that the end user
(e.g. business people, etc.) have, understanding the types of data available to
the end user, proposing solutions that would solve the business problem,
validating the data to ensure data quality, and finally implementing prediction
models which make use of the data to help solve a business need (e.g.
predicting customer churn, fraud detection, etc.)

## 2. What is *supervised machine learning*?

Supervised machine learning is a subset of machine learning that consists of
making use of labeled training data to predict something about future data.
This could be a classification task (e.g. predicting which mushrooms are
poisonous and which ones are not, based on attributes such as size, color,
shape, etc.) This could also be a regression task (e.g. predict what the
average temperature will be next year given the temperatures, \\(CO_2\\))
levels, from the years before.

## 3. Machine Learning is often referred to as an *ill-posed problem*. What does this mean?

With Machine Learning, we are trying to induce a model (i.e. generalize) from
data such that it will do well with unseen, future data. A problem, however, is
that we can generate multiple models that perfectly fit the data set, but these
models might predict different values for the target features of unseen data.
Since we cannot determine a unique solutions to problems tackled by Machine
Learning, they are "ill-posed."

## 4. Credit Scoring question

### a. a. Which of these two models do you think will generalise better to instances not contained in the dataset?

Model 1 will probably generalize better than Model 2 because the feature that
Model 1 is using, `Loan-Salary Ratio`, seems to be much more relevant to the
likelihood of someone defaulting than `Age`. Also, the second model seems to be
much more complicated as well and is most likely to be overfitting the small
dataset.

### b. Propose an inductive bias that would enable a machine learning algorithm to make the same preference choice as you did in part (a).

When you have models that are doing equally well, choose the simpler one.
Follow Occam's Razor.

### c. Do you think that the model that you rejected in part (a) of this question is overfitting or underfitting the data?

I think the model I rejected was definitely overfitting.

## What is meant by the term *inductive bias*?

Inductive bias consists of restriction bias and preference bias. Restriction
bias describes all the hypotheses that the Machine Learning model will
entertain. The model will entertain some of those hypotheses over others. That
is Preference bias. Together, these two concepts describe inductive bias. Knowing
about the inductive bias of different models helps us decide what is more
appropriate to use, given that we know the strengths and weaknesses of our
dataset.

## How do machine learning algorithms deal with the fact that machine learning is an ill-posed problem?

Machine Learning algorithms have inductive biases that narrow the search space
while searching for the model that best generalizes the data. Choosing one
machine learning algorithm over another means favoring one model selection
criteria over another.

## What can go wrong when an inappropriate *inductive bias* is used?

When the inappropriate inductive bias is used, the model might underfit or
overfit the data, resulting in poor performance.

## It is often said that 80% of the work done on predictive data analytics projects is done in the Business Understanding, Data Understanding, and Data Preparation phases of *CRISP-DM*, and just 20% is spent on the Modeling, Evaluation, and Deployment phases. Why do you think this would be the case?

I think it's because it is so important that business people and data analysts
are in complete agreement that 1) there is a problem to be solved, 2) there is
a predictive analytics solution that can solve the problem, 3) there is data of
good quality that can be used for predictive analytics.  Without any of these
three parts, a project is likely to fail.

For example, if the data analyst has the proper data in hand, is of good
quality, we have the the perfect model, but we don't have *Business
Understanding*, then the project is probably going to be useless to the
business, since key business people have not been convinced that 1) there is a
business need, 2) that the data analyst has a solution that solves the problem.
Without business understanding, the data analyst might come up with a solution
to a problem that doesn't exist.

Data understanding is important because it lets us figure out the qualiity of
the data. It might help us figure out which features are useless, which ones
are important, and which might need some transformations, etc. It might
highlight outliers that may be due to typos, and it might highlight ones that
are actually valid. Without data understanding, it is more likely that the
predictions made by our models in the later stages, will perform more poorly,
as we might include features that have poor predictive performance or training
instances that are invalid outliers. Thus, we should understand the data
thoroughly before making running machine learning algorithms.

Once we have gone through the three phases and have established an Analytics
Base Table (ABT), then we can use off-the-shelf algorithms to make predictions
and evaluate the data.
