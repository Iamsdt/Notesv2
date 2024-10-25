## Chain Rule
In deep learning, the gradients of concern are often difficult to calculate because we are working with deeply nested functions (of functions (of functions…)). Fortunately, the _chain rule_ takes care of this. Returning to functions of a single variable, suppose that 𝑦=𝑓(𝑔(𝑥)) and that the underlying functions 𝑦=𝑓(𝑢) and 𝑢=𝑔(𝑥) are both differentiable. The chain rule states that
$$
\frac{dy}{dx} = \frac{dy}{du} \frac{du}{dx}.
$$
Turning back to multivariate functions, suppose that 𝑦=𝑓(𝑢) has variables 𝑢1,𝑢2,…,𝑢𝑚, where each 𝑢𝑖=𝑔𝑖(𝑥) has variables 𝑥1,𝑥2,…,𝑥𝑛, i.e., 𝑢=𝑔(𝑥). Then the chain rule states that
$$
\frac{\partial y}{\partial x_{i}} = \frac{\partial y}{\partial u_{1}} \frac{\partial u_{1}}{\partial x_{i}} + \frac{\partial y}{\partial u_{2}} \frac{\partial u_{2}}{\partial x_{i}} + \ldots + \frac{\partial y}{\partial u_{m}} \frac{\partial u_{m}}{\partial x_{i}} \ \textrm{ and so } \ \nabla_{\mathbf{x}} y =  \mathbf{A} \nabla_{\mathbf{u}} y,
$$
where 𝐴∈𝑅𝑛×𝑚 is a _matrix_ that contains the derivative of vector 𝑢 with respect to vector 𝑥. Thus, evaluating the gradient requires computing a vector–matrix product. This is one of the key reasons why linear algebra is such an integral building block in building deep learning systems.


### Chain Rule Definition:
If you have two functions \( f \) and \( g \), and you want to differentiate their composition \( h(x) = f(g(x)) \), then the chain rule states:
$$
\frac{d}{dx} [f(g(x))] = f'(g(x)) \cdot g'(x)

$$

### Intuition:
If $( g(x))$ changes, then \( f(g(x)) \) also changes based on how fast \( g(x) \) is changing. So, you first compute how fast \( f \) is changing with respect to \( g(x) \) (that’s \( f'(g(x)) \)) and then multiply that by how fast \( g(x) \) is changing with respect to \( x \) (that’s \( g'(x) \)).

### Example:
Let’s differentiate $( h(x) = (3x^2 + 2)^5 )$.

Here, you can think of it as the composition of two functions:
- Outer function: $( f(u) = u^5 )$
- Inner function: $( g(x) = 3x^2 + 2 )$

By the chain rule, you first differentiate the outer function $( f(u) = u^5 )$ with respect to ( u \), and then multiply it by the derivative of the inner function $( g(x) = 3x^2 + 2 )$ with respect to \( x \):

1. $( f'(u) = 5u^4 ) where ( u = 3x^2 + 2 )$
2. $( g'(x) = 6x )$

So, applying the chain rule:
$$
\frac{d}{dx} \left( (3x^2 + 2)^5 \right) = 5(3x^2 + 2)^4 \cdot 6x
$$
Simplified:
$$
= 30x(3x^2 + 2)^4
$$

### Explanation:
- The outer function \( f(u) = u^5 \) gives us \( 5(3x^2 + 2)^4 \).
- The inner function \( g(x) = 3x^2 + 2 \) gives us \( 6x \).
- Multiply them together to get the final derivative. 

# Back propagation

```python
x = torch.arange(4.0, requires_grad=True)  
print(x)  
print(x.grad)  # The default value is None  
  
y = 2 * torch.dot(x, x)  
print(y)  
y.backward()  
print(x.grad)
```

This code demonstrates the use of **autograd** in PyTorch, which is PyTorch’s automatic differentiation engine. Let's break down the code step by step and explain what happens, especially focusing on `y.backward()` and `x.grad`:

### Code Breakdown

#### 1. `x = torch.arange(4.0, requires_grad=True)`
- This line creates a 1D tensor `x` with values `[0.0, 1.0, 2.0, 3.0]`. The `requires_grad=True` argument tells PyTorch that we want to compute the gradient for this tensor during the backward pass. 
- **Autograd** will track all operations on tensors that have `requires_grad=True` so that it can compute derivatives for optimization or gradient-based learning.

#### 2. `print(x)`
- This will simply print the values of `x`: `tensor([0., 1., 2., 3.], requires_grad=True)`.

#### 3. `print(x.grad)  # The default value is None`
- `x.grad` is initially `None` because no backward operation has been called yet. Gradients are stored in the `grad` attribute of tensors only after a backward pass.

#### 4. `y = 2 * torch.dot(x, x)`
- The expression `torch.dot(x, x)` computes the dot product between `x` and itself, which is the sum of the element-wise products:
$$

  \text{dot}(x, x) = 0 \cdot 0 + 1 \cdot 1 + 2 \cdot 2 + 3 \cdot 3 = 14
  
  $$
  Then, `y = 2 * 14 = 28`. 
  So, `y` is a scalar tensor (i.e., a single value) with the value `28.0`.

#### 5. `y.backward()`
- This triggers the **backward pass**, where PyTorch computes the **gradients** of `y` with respect to `x`. 
- Since `y` is a scalar, PyTorch can compute the derivative of `y` with respect to each element in `x`, using the chain rule. Internally, PyTorch constructs a computational graph from the operations performed on tensors with `requires_grad=True` and uses that graph to compute the gradients.

#### 6. `print(x.grad)`
- After calling `y.backward()`, `x.grad` will contain the **gradients of `y` with respect to each element in `x`**. The gradient tells us how much a small change in `x` will affect the value of `y`. These gradients are stored in `x.grad`.

### Gradient Calculation (y.backward())

The expression for `y` is:
$$
y = 2 \times (0^2 + 1^2 + 2^2 + 3^2) = 28
$$

We need to compute the gradient of `y` with respect to `x`, i.e., $( \frac{dy}{dx} )$. Since:
$$
y = 2 \times (x_0^2 + x_1^2 + x_2^2 + x_3^2)
$$

The derivative of `y` with respect to each component of `x` is:
$$
\frac{dy}{dx_i} = 4 \times x_i
$$

So:
- For $( x_0 = 0 )$, $( \frac{dy}{dx_0} = 4 \times 0 = 0 )$
- For $( x_1 = 1 )$, $( \frac{dy}{dx_1} = 4 \times 1 = 4 )$
- For $( x_2 = 2 )$, $( \frac{dy}{dx_2} = 4 \times 2 = 8 )$
- For $( x_3 = 3 )$, $( \frac{dy}{dx_3} = 4 \times 3 = 12 )$

Thus, after `y.backward()`, the gradients stored in `x.grad` will be:
$$
x.grad = [0., 4., 8., 12.]
$$


The factor of **4** in the derivative of \( y \) with respect to each component $( x_i )$ comes from the specific structure of the equation for \( y \). Let's go through this step-by-step to see how this derivative is computed.

Recall that:
$$
y = 2 \times \text{dot}(x, x)
$$
where the dot product \( \text{dot}(x, x) \) is:
$$
\text{dot}(x, x) = x_0^2 + x_1^2 + x_2^2 + x_3^2 = \sum_{i=0}^{3} x_i^2
$$

So, the full equation for \( y \) becomes:
$$
y = 2 \times (x_0^2 + x_1^2 + x_2^2 + x_3^2)
$$

To find the derivative of \( y \) with respect to each component $( x_i )$, apply the **chain rule** from calculus.

### Step-by-Step Derivative

1. The expression for (y) can be rewritten as:
   $$
   y = 2 \times \sum_{i=0}^{3} x_i^2
   $$
   
2. Now, we need to differentiate \( y \) with respect to each $( x_i )$. Since \( y \) is a sum of squared terms, let's focus on one term at a time.

   For a single term $( x_i^2 )$, the derivative with respect to $( x_i )$ is:
   $$
   \frac{d}{dx_i} \left( x_i^2 \right) = 2x_i
   $$

3. The equation for \( y \) multiplies this sum by 2. So, when differentiating \( y \), you need to account for that outer factor of 2 as well.

   Applying the chain rule:
   $$
   \frac{dy}{dx_i} = 2 \times \frac{d}{dx_i} \left( x_i^2 \right) = 2 \times 2x_i = 4x_i
   $$

Thus, the derivative of \( y \) with respect to each component \( x_i \) is:
$$
\frac{dy}{dx_i} = 4x_i
$$

### Summary of Where 4 Comes From

- The factor of **2** comes from the scalar multiplication in the definition of $( y = 2 \times \text{dot}(x, x) )$.
- Another factor of **2** comes from differentiating $( x_i^2 )$ (the derivative of $( x_i^2 )$ is $( 2x_i ))$.

Multiplying these two factors together gives the **4**:
$$
\frac{dy}{dx_i} = 4x_i
$$

This is why the gradient for each component of \( x \) is $( 4x_i )$.

### Key Concepts

- **`y.backward()`**: This computes the gradients of `y` with respect to all tensors that have `requires_grad=True` and stores them in the `.grad` attribute of those tensors. It computes the derivative \( \frac{\partial y}{\partial x} \).
  
- **`x.grad`**: After the backward pass, `x.grad` contains the gradients of `y` with respect to each element of `x`. These gradients indicate how much `y` would change if we slightly increased or decreased the corresponding element of `x`.