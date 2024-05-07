# Gradient descent

:for linear regression or any function

Have a function $J(w,b)$

want $min\ J(w,b)$

![Untitled](Gradient%20descent%2042d71a21c6834f7bbab82b660d83b0fe/Untitled.png)

gradient descent는 local minima 를 알려준다

![Untitled](Gradient%20descent%2042d71a21c6834f7bbab82b660d83b0fe/Untitled%201.png)

### Gradient Descent Algorithm

$$
w = w-\alpha \frac{d}{dx}J(w,b)
$$

$$
b = b-\alpha\frac{d}{db}J(w, b)
$$

where $\alpha$ is learning rate which is **always a positive number**.

![Untitled](Gradient%20descent%2042d71a21c6834f7bbab82b660d83b0fe/Untitled%202.png)

![Untitled](Gradient%20descent%2042d71a21c6834f7bbab82b660d83b0fe/Untitled%203.png)

### how to choose the right alpha?

Near a local minimum.

- Derivative becomes smaller
- Update steps become smaller

Can reach minimum without decreasing learning rate, alpha

![Untitled](Gradient%20descent%2042d71a21c6834f7bbab82b660d83b0fe/Untitled%204.png)

![Untitled](Gradient%20descent%2042d71a21c6834f7bbab82b660d83b0fe/Untitled%205.png)

[C1_W1_Lab04_Gradient_Descent_Soln.ipynb](Gradient%20descent%2042d71a21c6834f7bbab82b660d83b0fe/C1_W1_Lab04_Gradient_Descent_Soln.ipynb)