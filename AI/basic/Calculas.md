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


Simply:
