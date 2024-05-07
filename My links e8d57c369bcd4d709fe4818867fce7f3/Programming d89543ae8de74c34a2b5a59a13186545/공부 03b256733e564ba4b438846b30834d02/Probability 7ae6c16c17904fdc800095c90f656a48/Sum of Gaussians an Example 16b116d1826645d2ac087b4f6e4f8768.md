# Sum of Gaussians: an Example

```mermaid
graph LR
	A[R: Total Response Time] --> B[T: Processing Time]
	A --> L[L: Network Latency] 
```

$R = T + L$

$$
T \ and \ L \ are \ independent .\newline T \sim\mathcal{N}(10, \ 2^2) \newline L \sim\mathcal{N}(5, \ 1^2)
$$

![Untitled](Sum%20of%20Gaussians%20an%20Example%2016b116d1826645d2ac087b4f6e4f8768/Untitled.png)

![Untitled](Sum%20of%20Gaussians%20an%20Example%2016b116d1826645d2ac087b4f6e4f8768/Untitled%201.png)

$R=(T+L)\sim\mathcal{N}(10+5, \ 4+1) = \mathcal{N}(15, 5)$

$\begin{cases} 
X\sim\mathcal{N}(\mu_X, \sigma^2_X
)
\newline
Y\sim\mathcal{N}(\mu_Y, \sigma^2_Y
)
\end{cases}$

→ $W\sim\mathcal{N}(a\mu_x+b\mu_y,a^2\sigma^2_x+b^2\sigma^2_y)$