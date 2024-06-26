---
tags:
  - Note
---
202403221203

Tags : [[Games on Graphs]]
# Winning Arena for Büchi Games
---
## Algorithm
```
Let Z(0) = V
until Z(i) stabilizes:
  X(i) = Attr_E(A, Z(i))
  Y(i) = pre_E(X(i))
  Z(i+1) = Y(i) /\ G
end until at n
return Attr_0(A, Z(n))
```

Where $G$ is the set of good nodes and `pre_E` is also defined in [[Winning Arena for Reachability Games]]. The output for this algorithm will be $A_{E}$

---
## Explanation
### Taking a closer look at `Attr_E` and `pre_E`
Given the following definition of `Attr_E`
![[Winning Arena for Reachability Games#^693834]]
We can see that `Attr_E` is built in a step by step manner.
- First we start with the target point
- Then we add nodes that imply a 1 step victory
- Then we add nodes that imply a 2 step victory or a 1 step victory
- we keep going forever but the computation can be stopped as a fixed point is reached
Thus we can think of the result of `Attr_E` as a union of some finite(or infinte) sets that fit the definitions of the bullet points.

Looking at the algorithm, we see that `Attr_E` is always followed by a `pre_E`. To look at their composition as a single function we think of `Attr_E` as the union of sets described by the bullets, since `pre_E` distributes over union we just distribute if over all bullet points and get
- First we start with nodes that imply a 1 step victory
- Then we add nodes that imply a 2 step or a 1 step victory
- Then we add nodes that imply a 3 step or a 2 step or a 1 step victory
- we keep going forever but the computation can be stopped as a fixed point is reached.
So `pre_E(Attr_E(A, X))` precisely gives us the set of points that have a path to `X` of length of at least 1, i.e, removing the points in `X` never come back to it from `Attr_E(A, X)`
### The Algorithm
>[!idea] 
>- In the first step we eliminate all dead ends for ***Elster***, which would just mean an instant loss
>- In the next step we start will all the good states that are not dead ends. And we look at the subset of good states that can be visited from there : point being, the ones not in the new subset are not the states that are visited infintely many times, so we can remove them from our target good set.
>- We keep repeating the process and shrinking the target good set in the same manner, if a vertex is removed this it cannot be forced to visit infinitely many times
>- Finding a fix point means that, once we are in that good set, we can always get back to it in finite steps and and find a winning game for ***Elster***.

`Attr_E` is almost the perfect function for "finding the set that goes to our target" except that it includes point in the target, which will leave the target and never come back, to get rid of those points exactly we do the `pre_E` after it.

In the first iteration we remove all the dead ends for ***Elster***, This is handled by the `pre_E` on the entire set.

Then we start with almost the entire good set, and look at all the points it in that come back to the same set. All other points will never reach the good set, hence they we can consider them as "losing" points, the only possible winning points can be inside that set.

In the next iteration, we look at points from that "winning" set, and see how which of them come back. Once that don't go to the losing zone, hence themselves are losing, so we restrict the winning set. Now the winning set contains points from which we can find a path that gets to the winning states at least twice.

Therefore `Z(n)` is the set of points that can be forced to visit the good states at least `n` times. Thus our goal is to find `Z(infinity)` which will just be the fixed point of the algorithm.

---
## Proof
>[!Theorem] Lemma
>$\forall n,Z(n+1)\subseteq Z(n), X(n+1)\subseteq X(n), Y(n+1)\subseteq Y(n)$

*Proof*: Proof is by induction

- Base Case
	- Since $Z(0) = X(0)=V$ we just need to prove for $Y$
	$$
    Y(1) = \text{pre}_{E}(X(1)) \subseteq \text{pre}_E(X(0))=Y(0)
	$$
- Induction step
	- The same argument words for $Y$.
	- $Z(i+2) = Y(i+1)\cap G \subseteq Y(i)\cap G = Z(i+1)$
	- $X(i+2) =\text{Attr}_{E}(A, Z(i+2)) \subseteq\text{Attr}_{E}(A, Z(i+1))=X(i+1)$

This shows that the algorithm must reach a fixed point in finitely many steps as $Z$ is decreasing, so it either decreases or gives a fixed point, hence the algorithm must terminate.

---
# References
[[Winning Arena for Reachability Games]]
[[Winning Strategy for Reachability Games]]
[[Winning Strategy for Büchi Games]]