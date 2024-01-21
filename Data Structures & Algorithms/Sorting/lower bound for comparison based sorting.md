- Any _comparison based sorting algorithm_ (one that does so by comparing pairs of them) is at least `nlog(n)` 

we will prove: 

> Any comparison based sorting algorithm performs $\Omega(nlog(n))$ comparisons in the worst case.

We can represent any algorithm as a _decision tree_ such as this, for sorting three objects: 

![[Pasted image 20231019115542.png]]

- We know that the number of leaves $l$ in the tree must be at least $n!$ (the total number of permutations).  
$$n! = n \times (n-1) \times (n-2) \times  ... \ 1$$
So for the example above $3! = 6$ 

- We know that the worst-case running time of the algorithm (the number of comparisons made) is at least the depth $d$ 

so we want to prove this: 

> $d \ge log_2l$ or equivalently $2^{d} \ge l$

![[Pasted image 20231019121003.png]]

So if we draw a complete binary tree then we see that the number of leaves is indeed equal to $2^d$ so we have shown this to be true intuitively (it can be done formally as well). 

So if our decision tree has at least $n!$ leaves and we know that the worst case running time is equal to the depth $d$ of the tree then we can say that the running time is: 

$$d \ge log_2(n!)$$
where $l=n!$ 

and we know from our [[Asymptotic Notation]] that if something is bounded below then it is $\Omega$ notation. So therefore: 

$$log_{2(n!)}= \Omega(nlogn)$$
This is our lemma. The proof follows: 

$$\begin{equation} 
 \begin{aligned}
 log_{2}(n!) & = log_{2}(1 \cdot 2 \cdot 3 \cdot ... n) \\ & = log_{2}1+ log_{2}2+ ... + log_{2}n
 \\ & \ge log_{2}\frac{n}{2} + ...log_{2}n
 \\ & \ge \frac{n}{2} log_{2}\frac{n}{2} 
 \\ & = \Omega(nlogn)
 \end{aligned}
\end{equation}
$$
here in the third line we take the upper half of the summation and say that the total summation is greater than or equal to the upper half. This allows us to conclude that the whole sum is at least $\frac{n}{2}log_{2}\frac{n}{2}$. If we multiply half of the sum by $\frac{n}{2}$ it will still be less than if we multiply the entire sum by $\frac{n}{2}$ and finally this is the same as $\Omega(nlogn)$ because we ignore constants such as $\frac{1}{2}$. 

This only applies to _comparison based algorithms_ but we can do marginally better if we have [[Non-Comparison Based Sorting Algorithms]] 