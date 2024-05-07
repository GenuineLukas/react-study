# Kurtosis: an Example

![Untitled](Kurtosis%20an%20Example%20a202412a9bde459cb2d80555ff4f9d61/Untitled.png)

![Untitled](Kurtosis%20an%20Example%20a202412a9bde459cb2d80555ff4f9d61/Untitled%201.png)

$$
\mathop{\mathbb{E}}[X_1^2]=\frac{1}{2}(-1)^2+\frac{1}{2}(1)^2 = 1\ \ \newline \mathop{\mathbb{E}}[X^2_2]=\frac{100}{202}(-0.1)^2+\frac{100}{202} (0.1)^2
\newline
+\frac{1}{202}(-10)^2+\frac{1}{202}(10)^2 =1
$$

for both,

first moment: 0, second moment: 1, third moment:0

what about fourth moment?

$$
\mathop{\mathbb{E}}[X_1^4]=\frac{1}{2}(-1)^4+\frac{1}{2}(1)^4 = 1\ \ \newline \mathop{\mathbb{E}}[X^4_2]=\frac{100}{202}(-0.1)^4+\frac{100}{202} (0.1)^4
\newline
+\frac{1}{202}(-10)^4+\frac{1}{202}(10)^4 = 99.01
$$

when the distribution has very large numbers very far away from the center, even if the probabilities are tiny, E of x to the 4 captures this. This is Kurtosis, the fourth moment.

$Kurtosis = E[X^4] = \mathop{\mathbb{E}}[(\frac{X-\mu}{\sigma})^4]$

![Untitled](Kurtosis%20an%20Example%20a202412a9bde459cb2d80555ff4f9d61/Untitled%202.png)