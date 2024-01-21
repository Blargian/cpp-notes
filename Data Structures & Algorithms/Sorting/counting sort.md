- sorts in $O(n+M)$ 

![[Pasted image 20231019125737.png]]

Ideas: 

- Assume that all elements of $A[1 ...n]$ are integers from $1$ to $M$ 
- By scanning the array $A$ once, we count the number of occurrences of each $1 \le k \le M$ in the array $A$ and store it in $Count[k]$. 
- Using this information, fill in the sorted array $A'$ 