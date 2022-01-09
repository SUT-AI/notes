<div align="center">
    <br>
    <br>
    <br>
    <br>
    <br>
    <br>
    <br>
    <br>
    <h1 style="font-size: 40px; margin: 10px 0;">AI - Inference in Bayesian Networks: Sampling</h1>
    <h1 style="font-size: 20px; font-weight: 400;">Sharif University of Technology - Computer Engineering Department</h1>
    <br>
    <h4 style="font-size: 18px; font-weight: 400; color:#555">Alireza Honarvar, Navid Eslami, Ali Najibi</h4>
    <br>
    <br>
    <br>
    <br>
    <br>
</div>
<hr>

Table of Contents
==============

- [Introduction](#introduction)
- [Basic Idea](#basic-idea)
- [Sampling from Given Distribution](#sampling-from-given-distribution)
- [Sampling in Bayes' Nets](#sampling-in-bayes-nets)
  - [Prior Sampling](#prior-sampling)
  - [Rejection Sampling](#rejection-sampling)
  - [Likelihood Weighting](#likelihood-weighting)
  - [Gibbs Sampling](#gibbs-sampling)
- [Conclusion](#conclusion)
- [References and Further Reading](#references-and-further-reading)

# Introduction

In the previous lecture note, it was shown that Inference
in Bayesian Networks, in general, is an intractable
problem. The natural approach now would be to try
and approximate the posterior probability. There are
several approximation methods for this problem, of
which we will discuss the ones based on randomized
sampling. The rest of the note is layed out as follows:
- We give intuition about the basic idea behind sampling, and why it is an attractive solution concept.
- We describe the building block of every sampling algorithm, namely, sampling from a given distribution.
- We explain four standard methods of sampling in Bayes' Nets, stating their pros and cons.


# Basic Idea

To compute an approximate posterior probability, one approach is to simulate the Bayes' Net's joint distribution. This can be achieved by drawing many samples from the joint distribution. Using these samples, we can approximate the probability of certain events.

Sampling has two main advantages:

- **Learning**: By getting samples from an unknown distribution, we can learn the associated probabilities.
- **Performance**: Getting a sample is much faster than  computing the right answer.

The primitive element in any sampling algorithm is the generation of samples from a known probability distribution. So the step-by-step algorithm is described in the following section.

# Sampling from Given Distribution
Consider the example of picking random colored cubes from a large bag of them. The probrability distribution of the colors of these cubes is given in the table below. In this setting, sampling is analogous to picking a random cube from said bag so that the probabilities are taken into account.
<table style="border:1px solid black;margin-left:auto;margin-right:auto;">
  <tr>
    <th style="text-align:center"> C </th>
    <th style="text-align:center"> Pr(C) </th>
  </tr>
  <tr>
    <td style="text-align:center"> Green </td>
    <td style="text-align:center"> 0.6 </td>
  </tr>
  <tr>
    <td style="text-align:center"> Red </td>
    <td style="text-align:center"> 0.1 </td>
  </tr>
  <tr>
    <td style="text-align:center"> Blue </td>
    <td style="text-align:center"> 0.3 </td>
  </tr>
</table>

In order to draw a sample from this distribution, we can use a uniform distribution to generate a seed 
and determine the sample based on that. As shown in the figure below, the unit length segment is 
partitioned into parts named $l_i$, each having length equal to $p_i$. These $p_i$ s represent the 
probabilities of the distribution, and are equal to $Pr(C=c_i)$. In other words, we have indexed the 
values that the random variable $C$ can take and defined the probabilities based on them. Here, we have 
$c_1 = green$, $c_2 = red$ and $c_3 = blue$.

<p style="text-align:center;">
<img src="./Images/Unit_Length_Segment_Partition.png" alt="drawing" width="auto"/>
</p>

We say that the sample drawn has the value $c_i$, if the seed chosen lies in $l_i$. Since we chose the seed from a uniform distribution, it can be shown that the probability of the sample being equal to $c_i$ is $Pr(C=c_i)$.

Thus, using uniform distributions in this manner, we can generate samples from a given distribution having the same corresponding probabilities.

# Sampling in Bayes' Nets

We now explain the four standard methods of sampling in Bayes' Nets, namely, Prior Sampling, Rejection Sampling, Likelihood Weighting, & Gibbs Sampling.

## Prior Sampling
Now we're ready to tackle the sampling problem! Suppose we want to sample from the joint distribution 
of the Bayes' Net, $Pr(x_1,...,x_n)$.

Consider the following process:

1.&nbsp; For i = 1 to n

2.&emsp;&emsp; Sample $x_i$ from $Pr(x_i | parents(x_i))$

3.&nbsp; Return $(x_1,...,x_n)$

This process generates a sample $X=(x_1,...,x_n)$ with the following probability:
$$
S_{PS}(x_1,...,x_n) = \prod_{i=1}^{n}Pr(x_i|parents(x_i)) = Pr(x_1,...,x_n),
$$
which is the Bayes' Net's joint probability.

Now we need to prove that the samples are realizations of I.I.D (Independent, Identically Distributed) random variables. 
1. Since we choose a new random number for every sample, thus samples are independent from each other. 
2. It has been also shown that they are identically distributed because of the formula above.

Suppose we have drawn $N$ samples from the joint distribution. Let the number of samples of an event be 
$N_{PS}(x_1,...,x_n)$.

So based on [the law of large numbers](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&ved=2ahUKEwiJsZWq0__0AhU6iv0HHagPClYQFnoECAcQAQ&url=https%3A%2F%2Fwww.lakeheadu.ca%2Fsites%2Fdefault%2Ffiles%2Fuploads%2F77%2Fimages%2FSedor%2520Kelly.pdf&usg=AOvVaw1xaHZqZNyROrouGHyLduDl), we have:
$$
lim_{N\to\infty}\hat{Pr}(x_1,...,x_n) = lim_{N\to\infty} \frac{N_{PS}(x_1,...,x_n)}{N}
$$
$$
= S_{PS}(x_1,...,x_n) = Pr(x_1,...,x_n),
$$

Hence, the sampling procedure is consistent with the joint distribution.

It is apparent that this algorithm is faster than its exact counter-parts. Since we can sample the joint distribution, we can approximate the probability of any event. However, in the case of conditional probabilities, it's more efficient not to consider samples inconsistent with the evidence. This brings us to the idea of rejection sampling.

Take the following Bayes' net as an example.

<p style="text-align:center;">
<img src="./Images/General_Example_BN.png" alt="drawing" width="auto"/>
</p>

Suppose we want to calculate $Pr(-a, | -c, +d)$. This means that our evidence variables are $C$ and $D$. An example of the sampling procedure is as follows.

Based on the sampling algorithm proposed above, we start with the topological sorted variables. At the first step, we sample $A$. Suppose that the result of the aforementioned operation is $+a$. Next in line could be $C$, since it can be thought of as the next node to be processed. Suppose the result of this sampling is $-c$. We continue our sampling algorithm with $B$. Suppose that after this sampling, the result is $-b$. The last variable to sample is $D$ with the result of $+d$. We return the resulting sample $(+a,-c,-b,+d)$.

After the sampling algorithm has finished, to determine $Pr(query|evidence)$, first, we need to filter out samples inconsistent with our evidence list. We will set the count of samples in this list as our denominator, and the count of samples in this list consistent with our query as our numerator.

## Rejection Sampling

The problem with prior sampling is that we keep samples which are not consistent with the evidence. Since the evidence might be unlikely, the number of unused samples (samples which will be discarded due to inconsistency with the evidence) will eventually be great.
A simple idea is to reject incosistent samples whilst sampling. To achieve this goal, as soon as an incosistency in the sample is observed, we will ignore (reject) that sample.

Consider the following process:

1.&nbsp; For i = 1 to n

2.&emsp;&emsp; Sample $x_i$ from $Pr(x_i | parents(x_i))$

3.&emsp;&emsp; if $x_i$ not consistent with evidence:

4.&emsp;&emsp;&emsp;Return (no sample is generated in this cycle)

5.&nbsp; Return $(x_1,...,x_n)$

This algorithm is also consistent with the conditional probabilities.

Take the following Bayes' net as an example.

<p style="text-align:center;">
<img src="./Images/General_Example_BN.png" alt="drawing" width="auto"/>
</p>

Suppose we want to calculate $Pr(-a, | -c, +d)$. This means that our evidence variables are $C$ and $D$. An example of the sampling procedure is as follows.

Based on the sampling algorithm proposed above, we start with the topological sorted variables. At the first step, we sample $A$. Suppose that the result of said operation is $+a$. Next in line could be $C$, since it can be thought of as the next node to be processed. Suppose that after sampling $C$, the result is $+c$. Since $-c$ is one of our evidences, we should reject this sample; which is achieved by returning None and adding no sample to our sample list.

Otherwise, in case of $-c$ for the sampling result of C, we continue our sampling algorithm with $B$. Suppose that after sampling $B$, the result is $-b$. The last variable to sample is $D$ and since it is an evidence variable, we should repeat the same procedure we performed for $C$. If the result of sampling $D$ is $-d$, we reject this sample and return None; Otherwise, we return the resulting sample $(+a,-c,-b,+d)$.

After the sampling algorithm has finished, to determine $Pr(query|evidence)$, we only need to count samples which are consistent with the query to form our numerator and the count of all samples we returned (which are not None), as our denominator. Notice that we didn't have to filter samples to make them consistent with the evidence list, since we rejected inconsistent samples.


## Likelihood Weighting

If we take a close look at the problem with prior sampling, which led us to the rejection sampling method, we see that if the evidence is unlikely, many samples will be rejected, thus we end up repeating the sampling process many times to achieve the desired sample size. This problem brings us to likelihood weighting. The idea is to fix the evidence variables and sample the rest. However, this might cause an inconsistency with the distribution. The solution is to use a weight variable indicating the probability of the evidence given their parents.

The algorithm is as follows. We start with topologically sorted nodes, and a weight variable $w$ equal to 1. At each step, we sample non-evidence variables and for evidence variables, we just assign the evidence value to it and multiply $w$ by $P(x_i|parents(x_i))$. In the end, we need to calculate the sum of consistent samples' weights with query divided by the sum of all samples' weights to calculate $P(Query|Evidence)$.

1.&nbsp; $w$ = 1.0

2.&nbsp; For i = 1 to n

3.&emsp;&emsp; if $X_i$ is an evidence variable

4.&emsp;&emsp;&emsp;$X_i$ = observation $x_i$ for $X_i$

5.&emsp;&emsp;&emsp;Set $w$ = $w$ * $Pr(x_i|parents(x_i))$

6.&emsp;&emsp; else

7.&emsp;&emsp;&emsp; Sample $x_i$ from $Pr(x_i | parents(x_i))$

8.&nbsp; Return $(x_1,...,x_n), w$

The consistency of the algorithm is proven as follows.
For each sample with query or hidden variables $Q_1, ..., Q_n$ and evidence $E_1, ..., E_m$,
the process generates a sample $X=(q_1,...,q_n,e_1,...,e_m)$ with the following probability:
$$
S_{WS}(q_1,...,q_n,e_1,...,e_m) = \prod_{i=1}^{n}Pr(q_i|parents(Q_i)).
$$

Furthermore, the weight for each sample is:

$$
w(q_1,...,q_n,e_1,...,e_m) = \prod_{i=1}^{m}Pr(e_i|parents(E_i)).
$$

Together, the weighted sampling distribution is consistent:

$$
S_{WS}(q_1,...,q_n,e_1,...,e_m) * w(q_1,...,q_n,e_1,...,e_m) 
$$
$$
=\prod_{i=1}^{n}Pr(q_i|parents(Q_i)) \prod_{i=1}^{m}Pr(e_i|parents(E_i)) = Pr(q_1,...,q_n,e_1,...,e_m).
$$

Take the following Bayes' net as an example.

<p style="text-align:center;">
<img src="./Images/General_Example_BN.png" alt="drawing" width="auto"/>
</p>

Suppose we want to calculate $Pr(-a, | -c, +d)$. This means that our evidence variables are $C$ and $D$. An example of the sampling procedure is as follows.

Based on the sampling algorithm proposed above, we start by setting the weight $w$ equal to $1.0$. Then, we sample $A$ from its distribution, since it is the first node in the topological order of the Bayes' net. Thus, $A$ will be sampled from the distribution $Pr(A)$, where $Pr(+a) = 0.7$. Suppose that the result of said operation is $+a$. Next in line could be $C$, since it can be thought of as the next node to be processed. However, $C$ is an evidence node. This means that we should set it to $-c$ and multiply $w$ by $Pr(-c | +a) = 0.9$, leading to $w=0.9$. Next in line is $B$, which is again sampled from the distribution $Pr(B | +a)$ where $Pr(+b | +a) = 0.8$. Suppose that the result of this opreation is $-b$. Now, the only node left to be processed is $D$. Since this node is again an evidence variable, we should set it to $+d$ and multiply $w$ by $Pr(+d | -b, -c) = 0.2$, which is the conditional probability based on the values generated up to this point. This changes $w$ to $0.18$. Since there are no more nodes left, $w = 0.18$ is the weight of the sample $(+a, -b, -c, +d)$.

By repeating this procedure and calculating a weight for each sample, we will eventually find a collection of weighted samples. Then we could use the calculated weights to approximate the probability in question. This is done by summing the weights of the samples consistent with the query, and dividing by the sum of all weights generated.

## Gibbs Sampling
The main problem with Likelihood Weighting was the sample inefficiency that could occur. To rectify this issue, one could use the approach of Gibbs Sampling, which is a special case of the *Metropolis-Hastings* algorithm (See Page 62 of this [lecture note](https://www.stat.umn.edu/geyer/f05/8931/n1998.pdf)).

Suppose we want to draw a sample $X = (x_1, ..., x_n)$ from the distribution $Pr(X_{Query} | X_{Evidence} = Observations)$, where $X_{Query}$ and $X_{Evidence}$ are the query and evidence variables, respectively. The algorithm operates as follows:

1. Start from an arbitrary sample $X^{(1)} = (x_1^{(1)}, ..., x_n^{(1)})$, satisfying the $X_{Evidence} = Observations$ equality.
2. Assume that the last sample generated in out sample chain was $X^{(t)}$. We want to calculate the next sample, namely, $X^{(t+1)}$. Sample one **non-evidence variable** $x_i^{(t+1)}$ at a time, conditioned on all the others being $x_j^{(t+1)} = x_j^{(t)}$. In other words, we sample $x_i^{(t+1)}$ from $Pr(x_i | x_1^{(t)}, ..., x_{i-1}^{(t)}, x_{i+1}^{(t)}, ..., x_n^{(t)})$.

The main idea of Gibbs sampling is the second step of the algorithm. It turns out that the specified probability can be calculated easily, since we have

$$
Pr(x_i | x_1^{(t)}, ..., x_{i-1}^{(t)}, x_{i+1}^{(t)}, ..., x_n^{(t)})
$$

$$
 = \frac{Pr(x_i|parents(x_i^{(t)})) \times \prod_{j \neq i}^n Pr(x_j^{(t)} | parents'(x_j^{(t)}))}{\sum_x Pr(x_1^{(t)}, ..., x_{i-1}^{(t)}, x, x_{i+1}^{(t)}, ..., x_n^{(t)})}  
$$

$$
 = \frac{Pr(x_i|parents(x_i^{(t)})) \times \prod_{j \neq i}^n Pr(x_j^{(t)} | parents'(x_j^{(t)}))}{\sum_x [Pr(x_i=x|parents(x_i^{(t)})) \times \prod_{j \neq i}^n Pr(x_j^{(t)} | parents'(x_j^{(t)}))]} 
$$

$$
 = \frac{Pr(x_i|parents(x_i^{(t)})) \times \prod_{x_j \in children(x_i)}^n Pr(x_j^{(t)} | parents'(x_j^{(t)}))}{\sum_x [Pr(x_i=x|parents(x_i^{(t)})) \times \prod_{x_j \in children(x_i)}^n Pr(x_j^{(t)} | parents'(x_j^{(t)}))]}. 
$$

Here, $parents'$ represents the values of the parents of the variables in $X^{(t)}$, replacing $x_i^{(t)}$ with the current relevant value of $x_i$. For example, this relevant value in the numerator is $x_i$ itself, while the value in denominator is the $x$ in the summation. As it is shown in the equation, the clauses corresponding to Conditional Probability Tables (CPTs) not including $x_i$ all cancel out.

This cancellation will only leave the CPTs mentioning $x_i$, namely, the CPT of $x_i$ itself and the CPTs of its children. These CPTs are often referred to as the **Markov blanket** of $x_i$.

Since the denominator is only a normalization factor, we can simply calculate the numerator by using a join operation on the Markov blanket of $x_i$! Note that the CPTs of the children of $x_i$ are all fully conditioned except for $x_i$, which we are calculating the distribution for. This means that the size of the pruned CPTs are small. (equal to $|D_i|$) As was shown in the equations, to calculate the probabilities, we only need to multiply the corresponding entries. This means that the join process of the CPTs won't introduce a large CPT and can be done efficiently. For an example of this process, refer to [the 67th slide here](http://ce.sharif.edu/courses/99-00/1/ce417-2/resources/root/Slides/PDF/Session%2013_14.pdf).

It can be shown that as $t$ approaches infinity, $X^{(t)}$ approximates the distribution of $Pr(X_{Query} | X_{Evidence} = Observations)$. The proof is based on the fact that Gibbs sampling is actually simulating a Markov chain, therefore coverging to the steady state of the chain. However, it must be proven that the steady state probability distribution of this Markov chain is actually the same as the probability distribution $Pr(X_{Query} | X_{Evidence} = Observations)$. For a detailed proof, please refer to [this lecture note](https://ocw.mit.edu/courses/economics/14-384-time-series-analysis-fall-2013/lecture-notes/MIT14_384F13_lec26.pdf).

This updating procedure takes into account both upstream and downstream evidences in the Bayes' net, since each update conditions on every variable. This property fixes the problem of Likelihood Weighting, i.e., only conditioning on upstream variables. Thus, Gibbs sampling has better sampling efficiency (sum of the samples' weights is larger, therefore generating more effective samples), creating more useful data to be used in approximation.

In practice, the samples $X^{(t)}$ with small $t$ may not accurately represent the desired distribution. Furthermore, they may not be independent of the other samples $X'$ generated with the Gibbs method, because of the arbitrary choice of $X^{(1)}$. This begining of the chain is referred to as the **burn-in period**, and the samples generated here are generally not used as the desired $X$. So, $X$ is usually selected from the $X^{(t)}$ outside this period. However, this creates a time overhead, since the burn-in period could be somewhat large.

Take the following Bayes' net as an example.

<p style="text-align:center;">
<img src="./Images/General_Example_BN.png" alt="drawing" width="auto"/>
</p>

Suppose we want to calculate $Pr(+a, -b | +c, -d)$. This means that $C$ and $D$ are our evidence variables. An example of the sampling procedure is shown below. Variables set to true are shown in green, variables set to false in red and variables selected for resampling in yellow.

<p style="text-align:center;">
<img src="./Images/Gibbs_Example_Procedure.png" alt="drawing" width=100%/>
</p>

As it is shown in the figure above, we start from an arbitrary sample that satisfies the evidence values. Often, this arbitrary sample is generated randomly. Then, in each iteration, a non-evidence variable is selected to be resampled. Here, the first variable to be resampled is chosen to be $B$. The distribution used in this sampling, based on the formula stated above, is:
$$
Pr(+b|+a, +e, +c, -d)
$$
$$
 = \frac{Pr(+b | +a)Pr(-d | +b, +c)}{Pr(+b | +a)Pr(-d | +b, +c) + Pr(-b | +a)Pr(-d | -b, +c)} 
$$
$$
= \frac{0.8 \times 0.5}{0.8 \times 0.5 + 0.2 \times 0.9} = \frac{0.4}{0.58} \approx 0.689.
$$
As it is shown, we only need to consider the terms in $B$'s Markov blanket. This is why the numerator is these terms for $+b$, while the denominator is the sum of these terms for $+b$ and $-b$. (Basically, the normalizing factor) Thus, based on the calculations, we can see that $B$ is resampled from the distribution $Pr(B | +a, +e, +c, -d)$, where $Pr(+b | +a, +e, +c, -d) \approx 0.689$. By repeating this procedure for other non-evidence variables for a number of iterations, namely, the burn-in value, we will eventually reach a sample from the distribution of the original Bayes' net. Finally, we repeat this sampling procedure to procure a healthy number of samples, and approximate the probability of the query by counting the number of consistent samples and dividing by the total number of samples.

In a more general sense, Gibbs Sampling and Metropolis-Hastings are classified as *Markov Chain Monte Carlo* algorithms. Monte Carlo algorithms are basically the same as sampling. For more information, please refer to this [lecture note](https://www.stat.umn.edu/geyer/f05/8931/n1998.pdf).

# Conclusion
In this lecture note, we studied (randomized) approximation algorithms for inference in Bayes' nets. The main idea behind these methods was sampling, which enables fast approximation of event distributions. After describing the building block of sampling algorithms, four prominent methods of this type were studied, namely, Prior sampling, Rejection sampling, Likelihood Weighting and Gibbs sampling. The pros and cons of these methods were discussed, giving a somewhat complete picture as to what method performs the best in certain situations.

# References and Further Reading
- Artificial Intelligence, Sharif University of Technology, CE417-1, By Dr. Rohban. (Specifically, this [lecture note](https://www.stat.umn.edu/geyer/f05/8931/n1998.pdf))
- Artificial Intelligence: A Mordern Approach (3rd Ed.), By Stuart Russel & Peter Norvig.
- Time Series Analysis, Massachusetts Institute of Technology, By Prof. Mikusheva. (Specifically, this [lecture note on Gibbs Sampling](https://ocw.mit.edu/courses/economics/14-384-time-series-analysis-fall-2013/lecture-notes/MIT14_384F13_lec26.pdf))
- Statistics, University of Minnesota, 8931m By Prof. Geyer. (Specifically, this [lecture note on MCMCs](https://www.stat.umn.edu/geyer/f05/8931/n1998.pdf))
