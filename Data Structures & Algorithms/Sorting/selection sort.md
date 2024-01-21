Main idea: keep growing the sorted part of an array 

1. Find a minimum by scanning the array 
2. Swap it with the first element 
3. Forget about that element
4. Repeat with the remaining part of the array

![[Pasted image 20231019095333.png]]

Notice how the sorted region is grown! (the blocks in grey).

Pseudocode: 

```pseudo
\begin{algorithm}
\caption{Selection Sort}
\begin{algorithmic}
\Procedure{SelectionSort}{A[1...n]}
\For{i from 1 to n}
 \State $minIndex \gets $i
  \For{j from i+1 to n}
   \If{A[j] < A[minIndex]}
      \State $minIndex \gets $j
    \EndIf
    \State swap(A[i],A[minIndex])
  \EndFor
\EndFor
\EndProcedure
\end{algorithmic}
\end{algorithm}
```

Properties: 
- pessimistic running time of $O(n^2)$  due to the two loops 