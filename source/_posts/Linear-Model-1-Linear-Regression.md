---
title: Linear Model (1) - Linear Regression
date: 2016-12-08 15:50:49
tags:
- Machine Learning
- Lienar Model
categories:
- Tutorials
mathjax: true
---

### Maximize Likelihood Linear Regression

Suppose we have data set $S=\{(x^{(i)},y^{(i)}),i=1,\dots,m\}$ where $x^{(i)}\in\mathbb R^n$ such that x has $n$ features with $m$ training examples. Let us assume that the target variables and the inputs are related via a linear equation.

$$
y{(i)}=\theta^Tx{(i)}+\epsilon{(i)}
$$

Where $\epsilon^{(i)}$ is an error term that captures either un-model effects or random noise. Let's assume that the $\epsilon^{(i)}$'s are distribute i.i.d.(independently and identically distributed) according to Gaussian Distribution with mean zero and variance $\sigma^2$. Which can be written as $\epsilon^{(i)}\sim N(0, \sigma^2)$. And the pdf of $\epsilon^{(i)}$ is given by

$$
p(\epsilon^{(i)})=\frac{1}{\sqrt{2\pi}\sigma}\Big( -\frac{(\epsilon^{(i)})^2}{2\sigma^2} \Big)
$$

Because of $\epsilon^{(i)}=y^{(i)}-\theta^Tx^{(i)}$, the pdf also can be given as

$$
p(y^{(i)}|x^{(i)};\theta)=\frac{1}{\sqrt{2\pi}\sigma}\Big(-\frac{(y^{(i)}-\theta^Tx^{(i)})^2}{2\sigma^2}\Big)
$$

Notice that the notation '$p(y^{(i)}|x^{(i)};\theta)$' indicates that this is the distribution of $y^{(i)}$ given $x^{(i)}$ is parameterized by $\theta$ and $\theta$ is not a random variable, the formula is not a probability consition on $\theta$. We can write the distribution as '$y^{(i)}|x^{(i)};\theta\sim N(\theta^Tx^{(i)},\sigma^2)$'. Given an input matrix $X=(x^{(1)},x^{(2)},\dots,x^{(m)})^T$ and $\theta$, what the distribution of $y^{(i)}$'s is given by $p(\overrightarrow{y}|X;\theta)$. When we wish to explicity view this as a function of $\theta$, we call it the likelihood function:

$$
L(\theta)=L(\theta;X,\overrightarrow{y})=p(\overrightarrow{y}|X;\theta)
$$

Note that by the independence assumption on the $\epsilon^{(i)}$’s, this can be written by

$$
\begin{equation}
\begin{split}
L(\theta) =& \prod_{i=1}^{m}p(y^{(i)}|x^{(i)};\theta)\\
=& \prod_{i=1}^{m}\frac{1}{\sqrt{2\pi}\sigma}\exp\Bigg(- \frac{(y^{(i)}-\theta^Tx^{(i)})^2)}{2\sigma^2}\Bigg)
\end{split}
\end{equation}
$$

Now, given this probabilistic model relating the $y^{(i)}$'s and the $x^{(i)}$’s. The principal of maximum likelihood says that we should should choose $\theta$ so as to make the data as high probability as possible. So We are facing an optimization problem.

$$
\max_{\theta} L(\theta)
$$

We define a new likelihood function called log likelihood:

$$
\begin{equation}
\begin{split}
\ell(\theta)
&= \log L(\theta)\\
&= \log \prod_{i=1}^{m}\frac{1}{\sqrt{2\pi}\sigma}\exp\Big(-\frac{(y^{(i)}-\theta^Tx^{(i)})^2)}{2\sigma^2}\Big)\\
&= \sum_{i=1}^{m}\log\frac{1}{\sqrt{2\pi}\sigma}\exp\Big(-\frac{(y^{(i)}-\theta^Tx^{(i)})^2)}{2\sigma^2}\Big)\\
&= m\log\frac{1}{\sqrt{2\pi}\sigma}-\frac{1}{2\sigma^2}\sum_{i=1}^{m}(y^{(i)}-\theta^Tx^{(i)})^2
\end{split}
\end{equation}
$$

And the maximization problem $\max\_{\theta}\ell(\theta)$  become a minimization problem:

$$
\min_{\theta}\frac{1}{2}\sum_{i=1}^{m}(y^{(i)}-\theta^Tx^{(i)})^2
$$

This is our original least-squares cost function. Under the previous probabilistic assumptions on the data, least-squares regression corresponds to finding the maximum likelihood estimate of $\theta$.

Back to over Linear Regression problem, assume we have data set $S=\{(x^{(i)},y^{(i)}),i=1,\dots,m\}$ , and our hypothesis $h\_{\theta}(x)=\theta^Tx$ (we set $x\_0$ to be $1$ so that the constant $\theta\_0$ could be include into $\theta$ and thus $x\_{(i)}\in\mathbb R^{(n+1)}, \theta\in\mathbb R^{(n+1)}$). Notice that in our hypothesis, the $\theta$ is not the population parameter, this is the parameter we are going to estimate by maximize likelihood function. According to the probability analysis above, we define the cost function

$$
\mathit{J}(\theta)=\frac{1}{2}\sum_{i=1}^{m}(h_\theta(x^{(i)})-y^{(i)})^2
$$

And the linear regression problem can be express as this optimization problem

$$
\min_\theta J(\theta)
$$


Let's rewrite this problem with a simple form by matrix, denote $X=(x^{(1)},x^{(2)},\dots,x^{(m)})^T$, $y=(y^{(1)},y^{(2)},\dots,y^{(m)})$ where $x^{(i)}\in\mathbb R^{(n+1)},y\in\mathbb R^{(n+1)}$ and $\theta\in\mathbb R^{(n+1)}$. So the problem can be expressed by

$$
\min_\theta \|X\theta-y\|^2_2
$$

And the linear model of inputs $X$ can be shown as $y=\theta^Tx$, where $\theta=\arg \min\_\theta \|X\theta-y\|^2\_2 $. We will solve this question latter.

### Least Square Linear Regression

If we want to build a model which can fit the sample data with least error, a simple way is to make the different between the estimator and the samples to be smallest in some form. In the least square linear regression, we optimize the square of the errors. Suppose we have hypothesis $h\_\theta=X\theta$ (in the form of matrix, where $X\in\mathbb R^{m*(n+1)}$ and $\theta\in\mathbb R^{(n+1)}$, $x^{(i)}\_0=1$ for all the inputs to make $\theta\_0$ to be constant), the problem can be expressed in the form

$$
\min_\theta \|X\theta-y\|^2_2
$$

This is same with the maximize likelihood regression in expression but they have differences. In maximize likelihood estimation we have an important assumption that all the samples $x^{(1)}, x^{(2)},\dots,x^{(m)}$ are i.i.d. The $\theta$ is the parameter of the model, $h$ is our model or our hypothesis. With regard to maximizing likelihood regression, the most reasonable estimation should be the one which makes the probability of $n$ samples extracted from the model observe those $y$'s maximum. But for least square, the most reasonable estimation is the one which can fit the samples best(the minimum of the square of error). It is clear that those regression method are come from different idea.

When we employ maximize likelihood regression, we need to know the probability distribution of errors or the hypothesis. In general, we assume that the distribution is Gaussian. Under this assumption, maximize likelihood regression is equivalent to least square regression.

For least square, we can also try to understand it in the form of geometry. Suppose we have a vector space $N\in\mathbb R^{(n+1)}$ and all the input sample $x^{(i)}$ is in this space. In this regression problem, the real thing we want is to find one way that hold $x^{(i)}\theta=y^{(i)}$ for all $m$ samples, which can be written as $X\theta=y$. But in real world problems the most likely situation is the number of samples $m$ is larger than the features $n$ which indicates that the equation $X\theta=y$ will be overdetermined. Assume the solution of this least square problem is $\theta'$ and $X\theta'$ is the orthogonal projection $y$ project to the space spanned by $X$'s column vector. And in linear algebra the orthogonal projection from $y$ to $X\theta'$ is $X(X^T X)^{-1}X^Ty$. The solution can be expressed by $\theta'=(X^T X)^{-1}X^Ty$ easily. We will see that this is same with the solution we solve by taking the differential later.

### Solve <span>$\min\_\theta \|X\theta-y\|^2\_2$</span>

Except the least square solution of the overdetermined system, we can solve this by other way. With respect to $\|X\theta-y\|^2\_2$ we have $J(\theta)=(X\theta-y)^T(X\theta-y)$ and the optimization problem will be

$$
\min_\theta J(\theta)=(X\theta-y)^T(X\theta-y)
$$

We take the derivative

$$
\begin{equation}
\begin{split}
\nabla_\theta J
&=\nabla_\theta (X\theta-y)^T(X\theta-y)\\
&=\nabla_\theta(\theta^TX^TX\theta-\theta^TX^Ty-y^TX\theta+y^Ty)\\
&=\nabla_\theta(\mathbb{tr}(\theta^TX^TX\theta)-2\mathbb{tr}(y^TX\theta))\\
&=X^TX\theta+X^TX\theta-2X^Ty
\end{split}
\end{equation}
$$

And set it to zero

$$
2X^TX\theta=2X^Ty
$$

We can get the solution

$$
\theta=(X^TX)^{-1}X^Ty
$$
