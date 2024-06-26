---
tags:
  - Note
---

Tags : [[Advanced Algorithms]], [[Linear Programming]]
# Linear Programming
---
>[!definition]
>Linear objective function: Minimise $c_1x_1 + \dots + c_nx_n = c^Tx$ subject to
>linear constraints:
 >   $a_{11}x_1 + \dots a_{1n}x_n \geq b_1$
>   .
>   .
>   .
>    $a_{m1}x_1 + \dots a_{mn}x_n \geq b_m$
>    $x_i \geq 0$
>
>Variables: $x_i$
>Every solution $x$ is a point in $\mathbb{R}^n$.
## Properties
---
- The feasible region is a convex polyhedron in $\mathbb{R}^n$.
- The optimum is always attained at a vertex/extreme point of the feasible region.
- Linear programs can be solved in polytime.

## Facts
---
- Polytope: bounded polyhedron, intersection of half spaces, convex hull of its vertices
- Face $f$ of a polytope $P \in\mathbb{R}^{n}$: $$	f=\{ x \in P\ |\ \alpha^{T}x=\beta \},\quad\forall y \in P, \alpha^{T}y\leq\beta.	$$
Faces have dimensions $-1,0,\dots,n-1$. In particular, if $v$ is a vertex of $P$, then $\exists \vec{\alpha},\vec{\beta}\in\mathbb{R}^{n}$ s.t. $\alpha^{T}v=\beta$, $\forall u \in P, u\neq v,\alpha^{T}u<\beta$.
-  A vertex of a polytope $P$ cannot be written as a convex combination of two or more points in $P$.

## Integrality Gap
---
For a given problem instance, there might be a difference in the optimal value that the LP for that problem gives us, and the optimal value that the *integral* LP gives. We define the highest (in a minimisation problem) such gap to be the integrality gap (as a ratio).
For an approximation algorithm, the best approximation ratio that we can get is bounded by this gap.

For example, in the [[Max Independent Set]] problem, given the complete graph as the instance, the $OPT(ILP)$ would be $1$, because we can have at most $1$ vertex in an independent set, while the $OPT(LP)$ would be $n$ by assigning all the vertices $\frac{1}{n}$. Here, the integrality gap is $\frac{1}{n}$, and thus we can't get a better approximation than $\frac{1}{n}$, an in fact, it is very difficult to find good approximation algorithms for max independent set instances.

$OPT(LP)\le OPT(ILP)\le$ our solution

**Integrality gap** $=\max_\limits{\text{all instances}}\frac{OPT(ILP)}{OPT(LP)}$
integrality gap $\le$ approximation ratio

---
# References
-> [[(Weighted) Vertex Cover using LP]]
-> [[Equational form of LP]]
-> [[Solution of an LP]]