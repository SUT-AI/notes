# Introduction to machine learning key concepts

# Table of contents
1. [Introduction](#introduction)
    1. [History](#history)
    2. [ML Applications](#ml-applications)
2. [Types of Machine Learning](#types-of-machine-learning)
    1. [Supervised Learning](#supervised-learning)
        1. [Classification](#classification)
        2. [Naïve Bayes Classifier Algorithm](#naïve-bayes-Classifier-algorithm)
    2. [Unsupervised Learning](#unsupervised-learning)
3. [Bias and Variance](#bias-and-variance)
    1. [What is Bias?](#what-is-bias)
    2. [What is variance?](#what-is-variance)
    3. [Bias and Variance Trade-Off](#bias-and-variance-trade-off)
4. [OverFitting and Underfitting](#overFitting-and-underfitting)
    1. [So what is overfitting?](#so-what-is-overfitting)
    2. [What is underfiting?](#what-is-underfiting)
    3. [and how to prevent overfitting?](#and-how-to-prevent-overfitting)
5. [Parameter Estiamtion](#parameter-estiamtion)
    1. [What is MLE?](#what-is-mle)
    2. [What is MAP?](#what-is-map)
6. [Handle unseen events](#handle-unseen-events)
    1. [Laplace Smoothing](#laplace-smoothing)
    2. [Linear interpolation](#linear-interpolation)
7. [More about dataset](#more-about-dataset)
    1. [Training Dataset](#training-dataset)
    2. [Validation Dataset](#validation-dataset)
    3. [Test Dataset](#test-Dataset)
    4. [About the dataset split ratio](#about-the-dataset-split-ratio)
8. [Conclusion](#conclusion)
9. [References](#references)

# Introduction
Humans are capable of learning by experiencing, but how about computers? Can they learn from past data and make correct decisions for future situations?

![](./images/intro_pic_1.png)

Machine learning techniques allow computers to automatically learn from a dataset and improve their performance from experiences and enable them to predict things in a new situation without being explicitly programmed. Machine learning algorithms bring computer science and statistics together to build mathematical models from our dataset that is known as training data and use these models for future decisions. The diagram below shows the ML algorithm:

![](./images/intro_pic_2.png)

## History
The base idea behind machine learning has a long history, But the term machine learning was first used by Arthur Samuel in 1959. Below we can see a timeline of ML in brief:

*   **1834:** Charles Babbage made the first computer that could be programmed by punched cards and all modern computers followed its logical structure.
*   **1936:** Alan Turing gave a theory about how machines can execute a set of instructions.
*   **1940:** First manually operated the computer named "ENIAC" was invented.
*   **1943:** The first model of human neural network was modeled with electronic circuits.
*   **1950:** "Computer Machinery and Intelligence," was published by Alan Turing on the topic of AI with this question, "Can machines think?".
*   **1952:** Arthur Samuel created a program to play checkers for an IBM computer that could play better by playing more.
*   **1959:** Arthur Samuel first used the term “Machine Learning” and popularized it. In this year, the first neural network was used to solve a real-world problem to remove echoes over phone lines using an adaptive filter.
*   **1974 to 1980:** These years are known as AI winter that lots of people lost their interest in AI and governmental funding reduced.
*   **1985:** A neural network was developed named NETtalk that was able to correctly pronounce 20000 words in a week.
*   **1997:** IBM’s computer named Deep Blue won a chess game against human chess expert Garry Kasparov.
*   **2006:** Geoffrey Hinton has first used the name "deep learning" instead of neural net research.
*   **2012:** Google developed a deep neural network system to distinguish cat and human images in a YouTube video.
*   **2016:** AlphaGo won a Go game against number one and number second player of Go.

## ML Applications


![](./images/intro_pic_3.png)

Machine learning concepts are growing every day and we can see their usages everywhere. Some of the real-world applications of ML are:

*   **Image recognition:**
    
    One example can be Facebook friends tagging suggestion that when we upload a photo with our Facebook friends, then we can see some labels suggestions with their names. This project is called Deep Face which uses face detection and recognition algorithms.
    
![](./images/intro_pic_4.png)
*   **Speech Recognition:**
    
    This project converts your voice to text and is also known as "Computer speech recognition." Some examples of this technology are Google assistant, Siri, Cortana, and Alexa.
    
![](./images/intro_pic_5.png)
*   **Traffic prediction:**
    
    Google Maps gathers data from all its users and sends them to its database and uses ML algorithms and techniques to provide the shortest routes with the least traffic to its users.
    
![](./images/intro_pic_6.png)
*   **Product recommendations:**
    
    Amazon and Netflix use ML for their product recommendation systems. Every time a user opens an amazon page can see the most relevant suggestion according to its previous searches or other features that are used in the dataset.
    
![](./images/intro_pic_7.png)

# Types of Machine Learning


There are three major recognized categories for ML:

![](./images/types_learning_1.png)

## Supervised Learning


In this method, the computer is provided by a set of labeled (tagged) data which is called training data, and tries to create a mathematical model according to it and learn to approximate the exact nature of the relationship between examples and their labels. By the time this process of training is finished, the supervised learning algorithm will be able to observe a new, never-before-seen example and predict a good label for it. Then we provide another set of data called sample data to test if the predictions are exact or not. One example of supervised learning is Face Recognition that we have a system that takes a photo, finds faces, and guesses who is in the photo (suggesting a tag) is supervised process. It has multiple layers to it, finding faces and then identifying them, but is still supervised nonetheless. The supervised algorithms are grouped into two main categories:

*   **Classification**
*   **Regression**

### Classification

In this algorithm, the machine learns from given training data and identifies the category of input data, and classifies it into some groups or classes. The main difference between this method and regression is that classification is a process of finding a function that helps in dividing the dataset into classes based on different parameters, but regression is a process of finding the correlations between dependent and independent variables. The classifiers can be binary which means we have only two possible outcomes or multi-class which means we can have more than two labels or classes. In another hand we have two types of learners in a classification problem:

*   **Lazy Learners:**
    
    Lazy learning methods simply store the data and generalizing beyond these data is postponed until an explicit request is made. In this case, we just store the dataset without learning from it and start classifying data when test data is received. These learners find the most related data that is stored in our training dataset. First, they store the training data and start the next phase when the test dataset arrives. In this method, we reduce the training time but prediction time increases. Some algorithms of this method are:
    
    *   K-Nearest Neighbours algorithm
    *   Case-based reasoning
*   **Eager Learners:**
    
    Eager learning methods construct a general (one-fits-all), explicit (input independent) description of the target function based on the provided training examples. In this method, the learner creates a model according to the training dataset, so the training time is more than lazy learners but the prediction is faster. Some algorithms of this method are:
    
    *   Decision Trees
    *   Naïve Bayes
    *   ANN

### Naïve Bayes Classifier Algorithm

Naïve Bayes algorithm is a probabilistic classifier based on Bayes theorem and is used to solve classification problems. It is called naïve because it assumes that the occurrence of a certain feature is independent of the occurrence of other features. It is also called Bayes because it depends on the principle of Bayes' Theorem.

A general naïve Bayes model has the form below that Y is our label variable and F is our feature set:

![](./images/bayes_net.png)

As a result of bayes net above and bayes theorem we can say that:

$P(Y, F_1, F_2, ..., F_n) = P(Y)\prod_{i}P(F_i|Y)$

As we can use this equation for computing posterior distribution over label variable Y first by calculating the joint probability of evidence and label for each label using the equation above the second sum to get the probability of evidence and then divide the first by second to calculate $P(Y| F_1, F_2, ..., F_n)$ .
The process can be seen in the figure below:

![](./images/naive_bayes_inference.png)

#### Advantages of Naïve Bayes Classifier

*   It is fast and not that much complicated.
*   It can be used for Binary as well as Multi-class Classifications.
*   It is the most popular choice for text classification problems.

#### Disadvantages of Naïve Bayes Classifier

*   Naive Bayes assumes that all features are independent or unrelated, so it cannot learn the relationship between features. It can be helpful in some cases to consider features independent, but sometimes the results are not exact.

## Unsupervised Learning
In this method, our training dataset doesn’t contain labels and they have not been categorized. Instead, our algorithm would be fed a lot of data and given the tools to understand the properties of the data. In this case, the machine learns to group, cluster the data such that a human (or other intelligent algorithms) can come in and make sense of the newly organized data. In another word, the goal of unsupervised learning is to find the underlying structure of the dataset, group that data according to similarities, and represent that dataset in a compressed format. The unsupervised algorithms are grouped into two main categories:

*   **Clustering**
*   **Association**
# Bias and Variance


if the model in machine learning is not accurate, it will make errors and these errors are known as Bias and Variance. these two errors cause a small difference between predicted and actual values! In machine learning, we want to reduce these errors to get more accurate predictions.  
Based on these errors, the machine learning model is selected that can perform best on the particular dataset.

## What is Bias?

In general, a machine learning model analyzes the data, finds patterns in it, and makes predictions. While training, the model learns these patterns in the dataset and applies them to test data for prediction.
**While the model is making predictions about data, a difference occurs between prediction values made by the machine learning model and actual values is known as bias errors**  
It can be defined as an inability of ML algorithms such as polynomial Regression to capture the true relationship between the data points. Each algorithm in ML  has some amount of bias because bias occurs from assumptions in the model, which makes the target function simple to learn. A model has either:  

- **High Bias:** A model with a high bias has more assumptions, and the model can not capture the important features of our dataset. the model with high biased has good performance on training data but not test data.  
- **Low Bias:** A low bias model will make fewer assumptions about the form of the target function.

linear algorithms have a high bias, as they learn fast. The simpler the algorithm, the higher the bias it has! but a nonlinear algorithm often has low bias.


#### Machine learning algorithms with low bias:
 
- Decision Trees
- k-Nearest Neighbours


#### Machine learning algorithms with high bias:
- Linear Regression
- Logistic Regression


## What is a variance?  
  
The variance of the model tells us the amount of variation in the prediction if the different data is used. a model should not vary too much from one training dataset to another, which means the algorithm should be good in understanding the mapping between inputs and outputs. some models have **low variance** but some of them have **high variance.**  

**high variance means there is a high variation in the prediction of the target function with changes in the training dataset**  

a model that has high variance performs well on training data but can not generalize unseen datasets as well.
high variance leads to overfitting and increases model complexities!  


#### machine learning algorithms with low variance:
- Linear Regression
- Logistic Regression


#### machine learning algorithms with high variance:

- decision tree
- K-nearest neighbors


in general, variance shows us how much our model is dependent on our dataset!

in the following image you can see the impact of bias and variance in the machine learning model:  

![](./images/bias-and-variance-in-machine-learning4.png)
## Bias and Variance Trade-Off
the best and ideal model has low bias and low variance but it can not be achieved and is not possible practically!
low-bias and high-variance lead to overfitting, high-bias, and low-variance lead to underfitting! so it is required to make a balance between bias and variance errors, and this balance between the bias error and variance error is known as the Bias-Variance trade-off.
in simple words, bias and variance are related to each other and we can not reduce both of them simultaneously!  

![](./images/bias-and-variance-in-machine-learning6.png)


# OverFitting and Underfitting
Supervised machine learning is best understood as approximating a target function (f) that maps input variables (X) to an output variable (Y). f(X) = Y 

An important consideration in learning the target function from the training data is how well the model generalizes to new data. Generalization is important because the data we collect is only a sample, it is incomplete and noisy  

- **Generalization:** It shows how well a model is trained to predict unseen data.
- **Noise:** </b> Noise is meaningless or irrelevant data present in the dataset. It affects the performance of the model if it is not removed.  


The goal of a good machine learning model is to generalize well from the training data to any data from the problem domain. This allows us to make predictions in the future on data the model has never seen.  

There is terminology used in machine learning when we talk about how well a machine learning model learns and generalizes to new data, namely overfitting and underfitting.  

Overfitting and underfitting are the two biggest causes for the poor performance of machine learning algorithms.  

## So what is overfitting?
when the ml model predicts training data very well but can not predict unseen data as well as training data we face overfitting in our ml algorithm!  
This means that the noise or random fluctuations in the training data is picked up and learned as concepts by the model. The problem is that these concepts do not apply to new data and negatively impact the model's ability to generalize.  
***An overfitted model is said to have low bias and high variance.***  

To detect overfitting we must split our dataset. about 80% of our data set is going to be trained and 20% of the dataset is going to be tested! Now, if the model performs well with the training dataset but not with the test dataset, then it is likely to have an overfitting issue. for example, if the error is 2.5% in training data and 20% in test data we have overfitting  

## What is underfitting?
Underfitting refers to a model that can neither model the training data nor generalizes to new data.
An underfit machine learning model is not a suitable model and will be obvious as it will have poor performance on the training data.  

## and how to prevent overfitting?

- **cross-validation:** In the general k-fold cross-validation technique, we divided the dataset into k-equal-sized subsets of data; these subsets are known as folds.
- **regularization:** in this technique we reduce our model features and simplify them with our tools! it may increase bias but reduce the variance of the model. in many cases we add penalizing terms to our objective function. as an example, in linear regression, we use l2 regularization and add sum penalizing term to the MSE function
- ...




![](./images/overfitting-in-machine-learning.png)



# Parameter Estimation

## What is MLE?

The following is a general setup for a statistical inference problem: There is an unknown quantity that we would like to estimate. We get some data From the data, we estimate the desired quantity this is a frequentist approach to this problem. In this approach, the unknown quantity $ \theta $ is assumed to be a fixed (non-random) quantity that is to be estimated by the observed data.  

We now would like to talk about a systematic way of parameter estimation. Specifically, we would like to introduce an estimation method, called maximum likelihood estimation (MLE)  
Let $ X_1,X_2,X_3, ... ,X_n $ be a random sample from a distribution with a parameter $ \theta $ (In general, θ might be a vector, ${\theta}=(\theta_1, \theta_2, \cdots, \theta_k)$ Suppose that $ x_1,x_2,x_3, ... ,x_n $ are the observed values of $ X_1,X_2,X_3, ... ,X_n $. If Xi's are discrete random variables, we define the likelihood function as the probability of the observed sample as a function of $ \theta $:

$\begin{align}
 L(x_1, x_2, \cdots, x_n; \theta)&=P(X_1=x_1, X_2=x_2, \cdots, X_n=x_n; \theta)
&=P_{X_1 X_2 \cdots X_n}(x_1, x_2, \cdots, x_n; \theta).
\end{align}$


- If Xi's are discrete, then the likelihood function is defined as
$\begin{align}
 L(x_1, x_2, \cdots, x_n; \theta)=P_{X_1 X_2 \cdots X_n}(x_1, x_2, \cdots, x_n; \theta).
\end{align}$

- If Xi's are jointly continuous, then the likelihood function is defined as
$\begin{align}
L(x_1, x_2, \cdots, x_n; \theta)=f_{X_1 X_2 \cdots X_n}(x_1, x_2, \cdots, x_n; \theta).
\end{align}$



In some problems, it is easier to work with the log likelihood function given by
$\begin{align}
 \ln L(x_1, x_2, \cdots, x_n; \theta).
\end{align}$ 

Now that we have defined the likelihood function, we are ready to define maximum likelihood estimation. Let X1, X2, X3, ..., Xn be a random sample from a distribution with a parameter $ \theta $. Suppose that we have observed X1=x1 , X2=x2 , ⋯ , Xn=xn . The maximum likelihood estimate of $ \theta $ is the value that maximizes the likelihood function:
$\begin{align}
 L(x_1, x_2, \cdots, x_n; \theta).
\end{align}$


Note that the value of the maximum likelihood estimate is a function of the observed data. Thus, like any other estimator, the maximum likelihood estimator (MLE) is indeed a random variable  

## What is MAP?

we would like to discuss a different approach for inference, namely the Bayesian approach. In the Bayesian framework, we treat the unknown quantity, $ \theta $, as a random variable. we assume that we have some initial guess about the distribution of $ \theta $. This distribution is called the prior distribution. We observe some data. We then use Bayes' rule to make inferences about the unobserved random variable. This is generally how we approach inference problems in Bayesian statistics. That is why this approach is called the Bayesian approach.  

in this approach, our goal is to draw inferences about an unknown variable X by observing a related random variable Y. The unknown variable is modeled as a random variable X, with a prior distribution.  
After observing the value of the random variable Y, we find the posterior distribution of X. This is the conditional PDF (or PMF) of X given Y=y,
we use the Bayes formula for calculating posterior distribution.  

$\begin{align}
f_{X|Y}(x|y)=\frac{f_{Y|X}(y|x)f_{X}(x)}{f_{Y}(y)}.
\end{align}$



in the above image we have 
$f_{X|Y}(x|y)$ as postrior distribution and 
$f_{X}(x)$ as priror distribution. in many problems
$f_{Y|X}(y|x)$ is MLE function that we explained it!  

The posterior distribution, 
$f_{X|Y}(x|y)$ , contains all the knowledge about the unknown quantity X. Therefore, we can use the posterior distribution to find point estimation of X. One way to obtain a point estimate is to choose the value of x that maximizes the posterior PDF (or PMF). This is called the maximum a posterior (MAP) estimation. 

Note that 
$f_{Y}(y)$ does not depend on the value of x. Therefore, we can equivalently find the value of x that maximizes:
$\begin{align}
f_{Y|X}(y|x)f_{X}(x).
\end{align}$


***in many cases we choose an alpha-beta distribution for prior distribution***










# Handle unseen events

One of the most important concepts in machine learning is to handle unseen events. To clarify, consider the following example.  

Consider the vector $ X=[x_1,x_2,x_3,x_4,x_5] $ and the following data as training dataset.  


|    data     |    label    |
| :-----------: | :-----------: |
|[1, 1, 1, 0, 1]|    a    |
|[1, 0, 1, 0, 0]|    a    |
|[0, 0, 1, 0, 1]|    a    |
|[0, 1, 1, 0, 0]|    a    |
|[0, 0, 1, 0, 0]|    a    |
|[0, 0, 0, 0, 1]|    b    |
|[0, 1, 1, 0, 1]|    b    |
|[0, 1, 0, 1, 1]|    b    |
|[0, 1, 1, 1, 1]|    b    |
|[0, 0, 0, 1, 1]|    b    |

We want to predict the label of $[1, 1, 0, 0, 1]$ using a simple naïve Bayes model. First, we create a naïve Bayes model based on the training dataset.  
    
![](./images/naive_model_1.png)

Now, we calculate the probability of each label based on the created naïve Bayes model.  


$P(label=a)\propto \frac{2}{5} \times \frac{2}{5} \times 0 \times 1 \times \frac{2}{5} = 0$  


$P(label=b)\propto 0 \times \frac{3}{5} \times \frac{3}{5} \times \frac{2}{5} \times 1 = 0$


If you look at the naïve Bayes model again, you will find out that there is no data with $x_3=0$ or $x_4=1$ for the label a, and there is no data with $x_1=1$ or $x_5=0$ for label b.  


**So, what would we do to handle this situation?**

## Laplace Smoothing

One of the most common methods to solve the above problem is using Laplace smoothing. Consider a bag of green and yellow balls. Suppose there are three green balls and no yellow balls in the bag. So, the probability of each color is:  

![](./images/balls_1.png)

$P(color=green)=1$  

$P(color=yellow)=0$  

Using Laplace smoothing, we pretend that we saw every outcome extra time. For the above example, by using Laplace smoothing with, the probabilities for each color are as follows:  

![](./images/balls_2.png)

$P(color=green)=\frac{4}{5}$  


$P(color=yellow)=\frac{1}{5}$  

In general:  

$P_{LAP,k}(x)=\frac{c(x)+k}{N+k|X|}$  

And for conditional probabilities:  

$P_{LAP,k}(x|y)=\frac{c(x,y)+k}{c(y)+k|X|}$  

**Using Laplace smoothing with large k is not appropriate as it ignores the prior belief.**  


Now, back to the label prediction example. We use Laplace smoothing with $k=1$ and calculate label probabilities again. We consider the following extra data:  

|    data     |    label    |
| :-----------: | :-----------: |
|[1, 1, 1, 1, 1]|    a    |
|[1, 1, 1, 1, 1]|    b    |
|[0, 0, 0, 0, 0]|    a    |
|[0, 0, 0, 0, 0]|    b    |

![](./images/naive_model_2.png)

$P(label=a)\propto \frac{3}{7} \times \frac{3}{7} \times \frac{1}{7} \times \frac{6}{7} \times \frac{3}{7} = \frac{162}{16807}$  


$P(label=b)\propto \frac{1}{7} \times \frac{4}{7} \times \frac{4}{7} \times \frac{3}{7} \times \frac{6}{7} = \frac{288}{16807}$  


## Linear interpolation

In practice, Laplace smoothing often performs poorly for $P(X|Y)$ When $X$ or $Y$ is very large.  



Another useful method is **linear interpolation**. Linear interpolation (also known as **Lerp**) is a method to find unknown values between two known points. The unknown values are approximated through Linear interpolation by connecting these two known points with a straight line.  


In this method, we consider both $p(x|y)$ and $p(x)$ to calculate the $p(x|y)$  

In general:  

$P_{LIN}(x|y)=\alpha P(x|y)+(1-\alpha)P(x), 0<\alpha<1$  

By choosing an appropriate value for $\alpha$, we can handle unseen events.  


# More about the dataset

In the last section, we learned about Laplace smoothing and linear interpolation. But how can we calculate appropriate values for $\alpha$ and k?  

We introduce three datasets:  

## Training Dataset

**The sample of data used to fit the model.**
The actual dataset that we use to train the model (weights and biases in the case of a Neural Network). The model sees and learns from this data.  

## Validation Dataset
**The sample of data used to provide an unbiased evaluation of a trained model on the training dataset while tuning model hyperparameters. The evaluation becomes more biased as a skill on the validation dataset is incorporated into the model configuration.**  
The validation set is used to evaluate a given model, but this is for frequent evaluation. We, as machine learning engineers, use this data to fine-tune the model hyperparameters. Hence the model occasionally sees this data but never does it “Learn” from this. We use the validation set results and update higher-level hyperparameters. So, the validation set affects a model, but only indirectly. The validation set is also known as the Dev set or the Development set. This makes sense since this dataset helps during the “development” stage of the model. We use this dataset to calculate $\alpha$ and $k$.  

![](./images/diagram.png)  

## Test Dataset

**The sample of data used to provide an unbiased evaluation of the final trained model on the training dataset.**  

The Test dataset provides the gold standard used to evaluate the model. It is only used once a model is completely trained(using the train and validation sets). The test set is generally what is used to evaluate competing models (For example on many Kaggle competitions, the validation set is released initially along with the training set, and the actual test set is only released when the competition is about to close, and it is the result of the model on the Test set that decides the winner). Many times the validation set is used as the test set, but it is not good practice. The test set is generally well-curated. It contains carefully sampled data that spans the various classes that the model would face when used in the real world.  

## About the dataset split ratio
Now that you know what these datasets do, you might be looking for recommendations on how to split your dataset into Train, Validation, and Test sets.  
This mainly depends on 2 things. First, the total number of samples in your data, and second, on the actual model you are training.  
Some models need substantial data to train upon, so in this case, you would optimize for the larger training sets. Models with very few hyperparameters will be easy to validate and tune, so you can probably reduce the size of your validation set, but if your model has many hyperparameters, you would want to have a large validation set as well(although you should also consider cross-validation). Also, if you happen to have a model with no hyperparameters or ones that cannot be easily tuned, you probably don’t need a validation set too!  

![](./images/ratio.png)


# Conclusion
so in this chapter, we introduced key concepts of machine learning.
we learned about the applications of ML, supervised and unsupervised in ML, and some algorithms like naive Bayes.
after these primary concepts, we learned about some problems like bias and variance and their relations to overfitting and underfitting.
for parameter estimation, we learned two statistical approaches like Bayesian and frequentist approach and after that, we used these two frameworks and some formulas like Laplace and linear interpolation which are based on MLE and MAP.
we also learned about how to work with datasets in machine learning.  

# References

[Gentle Introduction to the Bias-Variance Trade-Off in Machine Learning](https://machinelearningmastery.com/gentle-introduction-to-the-bias-variance-trade-off-in-machine-learning/).  

[Understanding the Bias-Variance Tradeoff](https://towardsdatascience.com/understanding-the-bias-variance-tradeoff-165e6942b229).  

[Underfitting and Overfitting](https://www.geeksforgeeks.org/underfitting-and-overfitting-in-machine-learning/).  

[Probability concepts explained: Maximum likelihood estimation](https://towardsdatascience.com/probability-concepts-explained-maximum-likelihood-estimation-c7b4342fdbb1).  

[A Gentle Introduction to Maximum Likelihood Estimation and Maximum A Posteriori Estimation](https://towardsdatascience.com/a-gentle-introduction-to-maximum-likelihood-estimation-and-maximum-a-posteriori-estimation-d7c318f9d22d#:~:text=estimated%20with%20MLE.-,Maximum%20A%20Posteriori%20Estimation,when%20you%20have%20enough%20data.&text=For%20example%2C%20if%20Liverpool%20only,is%202%2F2%20%3D%201).
