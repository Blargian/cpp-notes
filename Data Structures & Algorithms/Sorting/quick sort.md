- comparison based algorithm
- running time: $O(nlogn)$ (on average)
- efficient in practice 
- not so efficient when there are many equal elements (few unique ones)

![[Pasted image 20231019131517.png]]
Partition the array with respect to $x = A[1]$ where x is now in it's final position : 

![[Pasted image 20231019131626.png]]

We then sort the two parts (red part and purple part) recursively: 

![[Pasted image 20231019131733.png]]

Pseudocode: 
```pseudo
\begin{algorithm}
\caption{QuickSort}
\begin{algorithmic}
\Procedure{QuickSort}{$A,l,r$}
\If{$l \ge r$}
\Return
\EndIf
\State $m \gets $ Partition($A,l,r$)
\State QuickSort($A,l,m-1$)
\State QuickSort($A,m+1,r$)
\EndProcedure
\end{algorithmic}
\end{algorithm}
```
Visually, the algorithm is working like this: 

![[Pasted image 20231019145728.png]]

Partitioning works as follows: 

- pivot is $x = A[l]$
- move $i$ from $l+1$ to $r$ maintaining the following invariant:
	-  $A[k] \le x$ for all $l+1 \le k \le j$ 
	- $A[k] \gt x$ for all $j+1 \le k \le i$ 

For brevity's sake, we begin not from the beginning but at some point in the process. 

We have a _red region_ which is $A[k] \le x$ for all $l+1 \le k \le j$  and also a _blue region_ which is $A[k] \gt x$ for all $j+1 \le k \le i$ 

![[Pasted image 20231019150127.png]]

We extend i by 1 from the blue region 

![[Pasted image 20231019150235.png]]

$9 \ge 6$ so it becomes part of the blue region and we extend i by 1 more to 4. 

![[Pasted image 20231019150312.png]]
This time $4 \lt 6$ and so we swap it with the first element of the blue region and it becomes part of the red region. 

![[Pasted image 20231019150339.png]]
4 is now part of the red region and the 9 we swapped with it is at the end of the blue region

![[Pasted image 20231019150403.png]]
we extend i by one more to 7 

![[Pasted image 20231019150428.png]]
$7 \gt 6$ so it remains as part of the blue region and we extend i once more 

![[Pasted image 20231019150456.png]]
Now we have the situation where $6 \ge x$ and so 6 gets swapped with the first element of the blue region and becomes part of the red region. 

![[Pasted image 20231019150524.png]]
We move i forward once more to 1
![[Pasted image 20231019150536.png]]
again $1 \le x$ so we swap 1 with the first element of the blue region 9 and 1 becomes part of the red region. 

![[Pasted image 20231019150553.png]]
Lastly we swap $x$ which is 6 and the last element of the red region $j$ 

![[Pasted image 20231019150634.png]]

In pseudocode the Partition function looks like this: 

```pseudo
\begin{algorithm}
\caption{Selection Sort}
\begin{algorithmic}
\Procedure{Partition}{$A,l,r$}
\State $x \gets A[l]$
\State $j \gets l$
\For{i from $l+1$ to $r$}
\If{$A[i] \le x$}
\State $j \gets j+1$
\State swap $A[j]$ and $A[i]$
\EndIf
\EndFor
\State swap $A[j]$ and $A[i]$
\Return $j$
\EndProcedure
\end{algorithmic}
\end{algorithm}
```
---
## Proof / Runtime analysis

This part of the lecture was not very clear to me. 
### unbalanced partitions 

Let's consider the case that we select the minimum value of the subarray and partition the subarray with respect to this first element. i.e) we have two arrays, one is empty and one is not (_unbalanced partition_). The following recurrence relation is satisfied, where `n` is our pivot point: 

$$
\begin{aligned}
T(n) &= n + T(n-1): \\
    T(n)  &= n +(n-1)+(n-2)+...=\Theta(n^2)
\end{aligned}
$$
This is an arithmetic series so we know it grows quadratically (_not quick_)

With a different case, partition such that one sub array has size 5 and the other size 4. (_another unbalanced partition_)

$$
\begin{aligned}
T(n) & = n+T(n-5)+T(4): \\
T(n) & \ge n+(n-5)+(n-10)+...=\Theta(n^2)
\end{aligned}
$$
we replaced $T(n-5)$ with $(n-5)+T(n-10)$ and then replaced $T(n-10)$ with $(n-10)$ 

### balanced partitions 

Assume we partition into two equal parts. We get the following recurrence relation:

$$
\begin{aligned}
T(n) &= 2T(\frac{n}{2})+n: \\
    T(n)  &= \Theta(nlogn)
\end{aligned}
$$
Which we recognise as the same one from the merge sort. (we spend a linear amount of time, $n$, at each level of the tree, and there are $logn$ levels)

With unbalanced partitions: 

$$
\begin{aligned}
T(n) &= T\left(\frac{n}{10}\right)+ T\left(\frac{9n}{10}\right)+ O(n)
\end{aligned}
$$

![[Pasted image 20231020084232.png]]

All of this shows us that we want to pick a pivot element such that the two subarrays are balanced.  To do this we select the partition **randomly** ... 

**why random?**

![[Pasted image 20231020084924.png]]

Theorem: 
>Assume that all the elements of $A[1...n]$ are pairwise different. Then the average running time of RandomizedQuickSort(A) is $O(nlogn)$ while the worst case running time is $O(n^2)$

--- 
## Equal elements

We can partition into three regions, as shown below. $m1$ is the first pivot point and $m2$ the second pivot point.  

![[Pasted image 20231022083036.png]]