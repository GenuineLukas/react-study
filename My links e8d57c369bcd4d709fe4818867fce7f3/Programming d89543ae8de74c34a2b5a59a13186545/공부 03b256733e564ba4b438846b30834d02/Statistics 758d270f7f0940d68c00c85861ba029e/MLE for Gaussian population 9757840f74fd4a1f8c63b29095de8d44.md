# MLE for Gaussian population

Suppose you have $n$ samples $X=(X_1, X_2, X_3, \ldots, X_n)$ from a Gaussian distribution with mean $\mu$ and variance $\sigma^2$. This means that $X_i \sim \mathcal{N}(\mu, \sigma^2)$.

If you want the MLE for $\mu$ and $\sigma$ the first step is to define the likelihood. If both $\mu$ and $\sigma$ are unknown, then the likelihood will be a function of these two parameters. For a realization of $X$, given by $x=(x_1, x_2, \ldots, x_n):$

$$
L(\mu, \sigma;x)=\prod^n_{i=1}f_{X_i}(x_i) = \frac{1}{(\sqrt{2\pi})^2\sigma^n}e^\frac{-\sum^n_{i=1}(x_i-\mu)^2}{2\sigma^2}
$$

Now all you have to do is find the values of $\mu$ and $\sigma$ that maximize the likelihood $L(\mu, \sigma;x)$.

Taking the derivative of the likelihood is a cumbersome procedure, because of all the products involved. However, there is a nice trick you can use to simplify things. Note that the logarithmic function is always increasing, so the values that maximize $L(\mu,\sigma;x)$ will also maximize is logarithm. This is the **log-likelihood**, and it is defined as

$\textit{l}\ (\mu, \sigma) = log(L(\mu, \sigma; x))$

after calculation you will get

$$
\textit{l}\ (\mu, \sigma) = log(L(\mu, \sigma; x))\newline =-\frac{n}{2}log(2\pi)-nlog(\sigma)-\frac{1}{2}\frac{\sum^n_{i=1}(x_i-\mu)^2}{\sigma^2}
$$

Now after getting partial derivatives, we reach to the conclusion that the MLE for $\mu$ and $\sigma$ has to be 

$$
\overset{\wedge}{\mu}=\frac{\sum^n_{i=1}x_i}{n} = \overline{x} \newline
\overset{\wedge}{\sigma}=\sqrt{\frac{\sum(x_i-\overline{x})}{n}}
$$

the expression tells you that the MLE for the standard deviation of a Gaussian population is very similar to the sample standard deviation’s formula. the only difference is the normalizing constant: for the MLE you have $\frac{1}{n}$ while for the sample standard deviation you have $\frac{1}{n-1}$.

A final comment: formally, what you just did was the derivation of the critical point. To make it all complete, you would need to show that these are the coordinates of a maximum point(and not a minimum or saddle point). However, we will skip it here.