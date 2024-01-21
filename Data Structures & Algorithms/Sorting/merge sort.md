Merge sort is asymptotically optimal as we know from the [[lower bound for comparison based sorting]]
Based on the divide and conquer technique 

- split the array into two halves
- make a recursive call on those two halves 

Pseudocode: 
```pseudo
\begin{algorithm}
\begin{algorithmic}
\Procedure{MergeSort}{A[1...n]}
\If{n=1}
 \Return A
\EndIf
  \State $m \gets \lfloor n/2 \rfloor$
  \State $B \gets MergeSort(A[1...m])$
  \State $C \gets MergeSort(A[m+1...n])$
  \State $A' \gets Merge(B,C)$
  \Return $A'$
\EndProcedure
\end{algorithmic}
\end{algorithm}
```

```pseudo
\begin{algorithm}
\begin{algorithmic}
\Procedure{Merge}{$B[1...p],C[1...q]$}
\State $D \gets$ empty array of size p+q
\While{B and C are both non-empty}
  \State $b \gets$ the first element of B
  \State $c \gets$ the first element of C
  
  \If{b<=c}
    \State move b from B to the end of D
  \else
    \State move c from C to the end of D
  \EndIf
\EndWhile
\State move the rest of B and C to the end of D
\Return D
\EndProcedure
\end{algorithmic}
\end{algorithm}
```

![[Pasted image 20231019105734.png]]
The algorithm first splits the array down consecutively from size 4 to arrays of size 2 to arrays of size 1 and then it merges the arrays back eventually into a sorted array. 

- the running time is `O(nlogn)` 
- You can sort a sequence of 1 million elements on your laptop using a mergesort but not using a selection sort. 