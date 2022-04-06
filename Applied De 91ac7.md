# Applied Design and Computing

# Lecture 1 - Bézier Curves

### Constructing a Bézier Curve

Let us assue we have a 2D space. We first come up with a set of **control points.**

Then we are going to be using a **parametric curve** based on a parameter $0 ≤ t ≤ 1$.

![Screenshot 2022-04-05 at 23.07.49.png](Applied%20De%2091ac7/Screenshot_2022-04-05_at_23.07.49.png)

$B(t) = (B_x(t), B_y(t))$

In order to construct this parametric curve, we take our control points and combine them in a **linear combination** (sum of control points multiplied by weights that are also dependent on the parameter $t$.

In the example above: $\bm{B(t)} = \bm{a_0}b_{0,2}(t)+\bm{a_1}b_{1,2}(t)+\bm{a_2}b_{2,2}(t)$

We can then set those weights according to how we want our shape to be. From this example:

![Screenshot 2022-04-05 at 23.18.52.png](Applied%20De%2091ac7/Screenshot_2022-04-05_at_23.18.52.png)

In this case, we chose a function for $b_{0,2}(t)$ which has a large effect on our curve at $t=0$, but no effect when $t=1.$

Similarly, we chose a function for $b_{2,2}(t)$ which has a large effect on our curve at $t=1$, but no effect when $t=0$.

Finally, we chose a function for $b_{1,2}$ which has no influence on the curve at $t=0, t=1$, and a maximum influence when $t=0.5$

### Bernstein Polynomials

We then just turned the problem of finding a curve, to a problem of finding those functions. In order to deal with this issues, Bézier used a tool called **Bernstein Polynomials**:

![Screenshot 2022-04-05 at 23.33.09.png](Applied%20De%2091ac7/Screenshot_2022-04-05_at_23.33.09.png)

**Quadratic Bernstein Polynomials:**

$$
\begin{aligned} & b_{0,2}(t) = (1-t)^2 \\ & b_{1,2}(t) = 2t(1-t) \\ & b_{2,2}(t) = t^2 \end{aligned}
$$

With this tools, we can build **Quadratic Bézier curves**. An important property of Bernstein Polynomials is that they can be generalised to higher order functions.

So if you have more control points, for example four, you would use **Cubic Bernstein Polynomials** to construct **Cubic Bézier Curves**. Even at higher orders, those polynomials still have the property of going from 0 to 1 (or vice-versa).

![Screenshot 2022-04-05 at 23.40.27.png](Applied%20De%2091ac7/Screenshot_2022-04-05_at_23.40.27.png)

![Screenshot 2022-04-05 at 23.40.35.png](Applied%20De%2091ac7/Screenshot_2022-04-05_at_23.40.35.png)

More generally, if you have an arbitrary number of control points, you can use n-th order Bernstein Polynomials to construct n-th order Bézier curves.

$$
\bm{B(t)} =\sum_{i=0}^{n} \bm{a}_ib_{i,n}(t)
$$

$$
b_{i,n}(t) = \binom{n}{i}t^i(1-t)^{n-1}
$$

<aside>
✨ **Tip**: you can calculate the binomial coefficient $\binom{n}{i}$ using the **scypi** function scipy.special.binom(n, k)

</aside>

### Properties of Bernstein Polynomials

- The weights $b_{i,n}(t)$ add up to 1 (i.e. they are **barycentric**)

$$
\sum_{i=0}^{n}b_{i,n}(t)=1, \forall t
$$

($\forall t$ means **for all** values of t)

- The curve is always contained within the **control polygon** (convex hull). It is the largest polygon you can construct with the control points.

![Untitled](Applied%20De%2091ac7/Untitled.png)

![Untitled](Applied%20De%2091ac7/Untitled%201.png)

- The curve always passes through the two endpoints. Therefore the tangent of the point where $t=0$ (coincident with $\bm{a_0}$) is the line between $\bm{a_0}$ and $\bm{a_1}$. And the same applies to the final control point.

![Untitled](Applied%20De%2091ac7/Untitled%202.png)

### Rational Bézier Curves

An issue we face with the previous definition of Bézier Curves is that once that you have fixed your control points, theres not much left to do, in order to tweak your curve.

![Untitled](Applied%20De%2091ac7/Untitled%203.png)

To solve this issue, we introduce one additional **weight** per control point, and use it to change the relative importance of different control points **.** 

$$
\bm{B(t)} = \frac{\sum_{i=0}^{n}w_i\bm{a}_ib_{i,n}(t)}{\sum_{i=0}^{n}w_ib_{i,n}(t)}
$$

For example we have three control points where $\bm{a_0}$ and  $\bm{a_2}$ are fixed, and we can vary the weight of $\bm{a_1}$.

![Untitled](Applied%20De%2091ac7/Untitled%204.png)

Sources: Images from lecture slides by Prof. Davide Lasagna.