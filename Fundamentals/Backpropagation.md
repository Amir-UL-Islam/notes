**Backpropagation algorithm** is probably the most fundamental building block in a neural network. It was first introduced in 1960s and almost 30 years later (1989) popularized by Rumelhart, Hinton and Williams in a paper called _“_[_Learning representations by back-propagating errors_](https://www.nature.com/articles/323533a0)_”_.

**The algorithm is used to effectively train a neural network through a method called chain rule.** In simple terms, after each forward pass through a network, backpropagation performs a backward pass while adjusting the model’s parameters (weights and biases).

In this article, I would like to go over the mathematical process of training and optimizing a simple 4-layer neural network. _I believe this would help the reader understand how backpropagation works as well as realize its importance._

# Define the neural network model

The 4-layer neural network consists of 4 neurons for the **input layer**, 4 neurons for the **hidden layers** and 1 neuron for the **output layer**.

![](https://miro.medium.com/v2/resize:fit:1400/1*sSIeU-WhsuHCQlOA00IBXg.jpeg)

Simple 4-layer neural network illustration

## Input layer

The neurons, colored in **purple**, represent the input data. These can be as simple as scalars or more complex like vectors or multidimensional matrices.

![](https://miro.medium.com/v2/resize:fit:540/1*JVKKlpPpmnes2CQoQ3uAbw.png)

Equation for input x_i

The first set of activations (_a_) are equal to the input values. _NB: “activation” is the neuron’s value after applying an activation function. See below._

## Hidden layers

The final values at the hidden neurons, colored in **green**, are computed using _z^l_ — weighted inputs in layer _l_, and _a^l_— activations in layer _l_. For layer 2 and 3 the equations are:

- _l = 2_

![](https://miro.medium.com/v2/resize:fit:528/1*38G8wzETqpzwQvtExO6k3w.png)

Equations for z² and a²

- _l = 3_

![](https://miro.medium.com/v2/resize:fit:576/1*pmnSATBMHgCnTSiL_cCy9Q.png)

Equations for z³ and a³

_W²_ and _W³_ are the weights in layer 2 and 3 while b² and b³ are the biases in those layers.

Activations _a²_ and _a³_ are computed using an activation function _f_. Typically, this **function _f_ is non-linear** (e.g. [sigmoid](https://en.wikipedia.org/wiki/Sigmoid_function), [ReLU](https://en.wikipedia.org/wiki/Rectifier_(neural_networks)), [tanh](https://en.wikipedia.org/wiki/Hyperbolic_function)) and allows the network to learn complex patterns in data. We won’t go over the details of how activation functions work, but, if interested, I strongly recommend reading [this great article](https://medium.com/the-theory-of-everything/understanding-activation-functions-in-neural-networks-9491262884e0).

Looking carefully, you can see that all of _x, z², a², z³, a³, W¹, W², b¹_ and _b²_ are missing their subscripts presented in the 4-layer network illustration above. **The reason is that we have combined all parameter values in matrices, grouped by layers.** This is the standard way of working with neural networks and one should be comfortable with the calculations. However, I will go over the equations to clear out any confusion.

Let’s pick layer 2 and its parameters as an example. The same operations can be applied to any layer in the network.

- _W¹_ is a weight matrix of shape _(n, m)_ where _n_ is the number of output neurons (neurons in the next layer) and _m_ is the number of input neurons (neurons in the previous layer). For us, _n = 2_ and _m = 4_.

![](https://miro.medium.com/v2/resize:fit:924/1*yRlAdSEUTPeteVQ6xFT8xg.png)

Equation for W¹

**NB: The first number in any weight’s subscript matches the index of the neuron in the next layer** (in our case this is the _Hidden_2 layer_) **and the second number matches the index of the neuron in previous layer** (in our case this is the _Input layer_).

- _x_ is the input vector of shape _(m, 1)_ where _m_ is the number of input neurons. For us, _m = 4_.

![](https://miro.medium.com/v2/resize:fit:288/1*VQav2v1g6qkRXD48-HlmpQ.png)

Equation for x

- _b¹_ is a bias vector of shape _(n , 1)_ where _n_ is the number of neurons in the current layer. For us, _n = 2_.

![](https://miro.medium.com/v2/resize:fit:376/1*S4fXnuMxU0BTPZ_W78hAaQ.png)

Equation for b¹

Following the equation for _z²,_ we can use the above definitions of _W¹, x_ and _b¹_ to derive “_Equation for z²”_:

![](https://miro.medium.com/v2/resize:fit:1400/1*rYAiLFIXevABB60bMZuFOQ.png)

_Equation for z²_

Now carefully observe the neural network illustration from above.

![](https://miro.medium.com/v2/resize:fit:1400/1*02zF6C6PYzGBbiah4-5fTQ.jpeg)

Input and Hidden_1 layers

You will see that _z²_ can be expressed using (_z_1)²_ and (_z_2)²_ where (_z_1)²_ and (_z_2)²_ are the sums of the multiplication between every input _x_i_ with the corresponding weight (_W_ij)¹._

This leads to the same “_Equation for z²”_ and proofs that the matrix representations for _z², a², z³_ and _a³_ are correct.

## Output layer

The final part of a neural network is the output layer which produces the predicated value. In our simple example, it is presented as a single neuron, colored in **blue** and evaluated as follows:

![](https://miro.medium.com/v2/resize:fit:340/1*D1vfLBOaZSKCuBaOp8gK7Q.png)

Equation for output s

Again, we are using the matrix representation to simplify the equation. One can use the above techniques to understand the underlying logic. **Please leave any comments below if you find yourself lost in the equations — I would love to help!**

# Forward propagation and evaluation

The equations above form network’s forward propagation. Here is a short overview:

![](https://miro.medium.com/v2/resize:fit:1400/1*51X_xj8p-jO8-plMfsyajg.png)

Overview of forward propagation equations colored by layer

The final step in a forward pass is to evaluate the **predicted output _s_** against an **expected output _y_**.

The output _y_ is part of the training dataset _(x, y)_ where _x_ is the input (as we saw in the previous section).

Evaluation between _s_ and _y_ happens through a **cost function**. This can be as simple as [MSE](https://en.wikipedia.org/wiki/Mean_squared_error) (mean squared error) or more complex like [cross-entropy](http://neuralnetworksanddeeplearning.com/chap3.html).

We name this cost function _C_ and denote it as follows:

![](https://miro.medium.com/v2/resize:fit:400/1*f8CwUGDguGaqCh-qvtW7lA.png)

Equation for cost function C

were _cost_ can be equal to MSE, cross-entropy or [any other cost function](https://stats.stackexchange.com/questions/154879/a-list-of-cost-functions-used-in-neural-networks-alongside-applications).

Based on _C_’s value, the model “knows” how much to adjust its parameters in order to get closer to the expected output _y_. This happens using the backpropagation algorithm.

# Backpropagation and computing gradients

According to the paper from 1989, backpropagation:

> repeatedly adjusts the weights of the connections in the network so as to minimize a measure of the difference between the actual output vector of the net and the desired output vector.

and

> the ability to create useful new features distinguishes back-propagation from earlier, simpler methods…

In other words, **backpropagation aims to minimize the cost function by adjusting network’s weights and biases.** The level of adjustment is determined by the gradients of the cost function with respect to those parameters.

One question may arise — **why computing gradients**?

To answer this, we first need to revisit some calculus terminology:

- _Gradient of a function C(x_1, x_2, …, x_m) in point x is a vector of the_ [_partial derivatives_](https://en.wikipedia.org/wiki/Partial_derivative) _of C in x._

![](https://miro.medium.com/v2/resize:fit:720/1*o1TgzZMHMWBUDamAtjKs2w.png)

Equation for derivative of C in x

- [_The derivative of a function C measures the sensitivity to change of the function value (output value) with respect to a change in its argument x (input value)_](https://en.wikipedia.org/wiki/Derivative)_. In other words, the derivative tells us the direction C is going._
- ==_The gradient shows how much the parameter x needs to change (in positive or negative direction) to minimize C._==

Compute those gradients happens using a technique called [chain rule](https://en.wikipedia.org/wiki/Chain_rule).

For a single weight _(w_jk)^l,_ the gradient is:

![](https://miro.medium.com/v2/resize:fit:1400/1*RiYDrF5DgmbNubMq9x_czA.png)

Equations for derivative of C in a single weight _(w_jk)^l_

Similar set of equations can be applied to _(b_j)^l_:

![](https://miro.medium.com/v2/resize:fit:1400/1*Xpco_RAhSlM9z5q6VSdy6Q.png)

Equations for derivative of C in a single bias _(b_j)^l_

The common part in both equations is often called _“local gradient”_ and is expressed as follows:

![](https://miro.medium.com/v2/resize:fit:828/1*WQz6hHI1ymFlVCYwtIBdaQ.png)

Equation for local gradient

The _“local gradient”_ can easily be determined using the chain rule. I won’t go over the process now but if you have any questions, please comment below.

The gradients allow us to optimize the model’s parameters:

![](https://miro.medium.com/v2/resize:fit:1188/1*I_qw7AQwKvwfLuOHc7e4fg.png)

Algorithm for optimizing weights and biases (also called “Gradient descent”)

- Initial values of _w_ and _b_ are randomly chosen.
- Epsilon (_e_) is the [learning rate](https://machinelearningmastery.com/understand-the-dynamics-of-learning-rate-on-deep-learning-neural-networks/). It determines the gradient’s influence.
- _w_ and _b_ are matrix representations of the weights and biases. Derivative of _C_ in _w_ or _b_ can be calculated using partial derivatives of _C_ in the individual weights or biases.
- Termination condition is met once the cost function is minimized.

I would like to dedicate the final part of this section to a simple example in which we will calculate the gradient of _C_ with respect to a single weight _(w_22)²_.

Let’s zoom in on the bottom part of the above neural network:

![](https://miro.medium.com/v2/resize:fit:1400/1*CxdjKFrE-Vww0KmI-3Z5sA.png)

Visual representation of backpropagation in a neural network

Weight _(w_22)²_ connects _(a_2)²_ and _(z_2)²_, so computing the gradient requires applying the chain rule through _(z_2)³_ and _(a_2)³:_

![](https://miro.medium.com/v2/resize:fit:1400/1*65rk0JpGEi6q0n2t6C688Q.png)

Equation for derivative of C in _(w_22)²_

Calculating the final value of derivative of _C_ in _(a_2)³_ requires knowledge of the function _C_. Since _C_ is dependent on _(a_2)³_, calculating the derivative should be fairly straightforward.

I hope this example manages to throw some light on the mathematics behind computing gradients. To further enhance your skills, I strongly recommend watching [Stanford’s NLP series where Richard Socher gives 4 great explanations of backpropagation](https://www.youtube.com/watch?v=isPiE-DBagM&list=PL3FW7Lu3i5Jsnh1rnUwq_TcylNr7EkRe6).

# Final remarks

In this article, I went through a detailed explanation of how backpropagation works under the hood using mathematical techniques like computing gradients, chain rule etc. _Knowing the nuts and bolts of this algorithm will fortify your neural networks knowledge and make you feel comfortable to take on more complex models. Enjoy your deep learning journey!_