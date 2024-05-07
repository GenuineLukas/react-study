# Supervised Learning - Linear Regression

Supervised model can be categorized into two different models:  Regression, Classification

**Regression Model**

Predicts numbers

infinitely many possible outputs 

**Classification Model**

Predicts categories

Small number of possible outputs

Terminology

![Untitled](Supervised%20Learning%20-%20Linear%20Regression%202e76023440ac4c34ac355b3844f6d0dd/Untitled.png)

![Untitled](Supervised%20Learning%20-%20Linear%20Regression%202e76023440ac4c34ac355b3844f6d0dd/Untitled%201.png)

**Squared error cost function**

![Untitled](Supervised%20Learning%20-%20Linear%20Regression%202e76023440ac4c34ac355b3844f6d0dd/Untitled%202.png)

J(w)가 Squared error cost function이라고 하고 b=0으로 놓아서 소거 시켰을 때

$$
f_w(x)\ 와\ J(w)의\ 상관관계
$$

![Untitled](Supervised%20Learning%20-%20Linear%20Regression%202e76023440ac4c34ac355b3844f6d0dd/Untitled%203.png)

가장 best fit인 라인을 위한 w를 고르려면 J(w)의 값이 가장 최소일 때의 w를 고르는게 좋다.

J(w,b)가 Squared error cost function이고 b도 변수일 때

![Untitled](Supervised%20Learning%20-%20Linear%20Regression%202e76023440ac4c34ac355b3844f6d0dd/Untitled%204.png)

**not a good fit**

![Untitled](Supervised%20Learning%20-%20Linear%20Regression%202e76023440ac4c34ac355b3844f6d0dd/Untitled%205.png)

**good fit**

![Untitled](Supervised%20Learning%20-%20Linear%20Regression%202e76023440ac4c34ac355b3844f6d0dd/Untitled%206.png)

```python
x_train = np.array([1.0, 2.0])           #(size in 1000 square feet)
y_train = np.array([300.0, 500.0])           #(price in 1000s of dollars)

def compute_cost(x, y, w, b): 
    """
    Computes the cost function for linear regression.
    
    Args:
      x (ndarray (m,)): Data, m examples 
      y (ndarray (m,)): target values
      w,b (scalar)    : model parameters  
    
    Returns
        total_cost (float): The cost of using w,b as the parameters for linear regression
               to fit the data points in x and y
    """
    # number of training examples
    m = x.shape[0] 
    
    cost_sum = 0 
    for i in range(m): 
        f_wb = w * x[i] + b   
        cost = (f_wb - y[i]) ** 2  
        cost_sum = cost_sum + cost  
    total_cost = (1 / (2 * m)) * cost_sum  

    return total_cost
```