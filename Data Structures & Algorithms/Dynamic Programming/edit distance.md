Is a [[dynamic programming]] problem. 

Given strings $A[1..n]$ and B[1...m] what is an optimal alignment (one resulting in minimum edit distance) of an $i$-prefix $A[1...i]$ of the first string and a $j$-prefix $B[1...j]$ of the second string?

The last column of an alignment can be either:
- an $\color{lightblue}insertion$
- a $\color{lightgreen}deletion$
- a $\color{purple}mismatch$
- a $\color{orange}match$

![[Pasted image 20231228105634.png]]

Let $D(i,j)$ be the edit distance of an $i$-prefix $A[1...i]$ and a $j$-prefix $B[1...j]$ 

The recurrence below corresponds to the figure about and is given as:

$$
\begin{equation}
D(i,j) = \min 
\begin{cases}  
\color{lightblue} D(i,j-1) +1 \\
\color{lightgreen} D(i-1,j) +1 \\ 
\color{purple} D(i-1,j-1) +1 \color{white}\text{ if } A[i] \ne B[j]\\ \\
\color{orange} D(i-1,j-1) +1 \color{white}\text{ if } A[i] = B[j]\\
\end{cases}
\end{equation}
$$
Now we want to compute all $D(i,j)$ :

![[Pasted image 20231228110325.png]]

Starting from the top left node we can compute each $D(i,j)$ by looking at the node and choosing the minimum from a node left, top or diagonal:

![[Pasted image 20231228110937.png]]

Eventually filling the entire matrix:

![[Pasted image 20231228111116.png]]

```pseudo
\begin{algorithm}
\caption{EditDistance}
\begin{algorithmic}
\Procedure{EditDistance}{$A[1...n],B[1...n]$)}
\State $D(i,0) \gets i \text{ and } D(0,j) \gets j \text{ for all } i,j$
\For{$j \text{ from } 1 \text{ to } m$}
\For{$i \text{ from } 1 \text{ to } n$}
\State $\color{lightblue}insertion$ $\gets D(i,j-1)+1$
\State $\color{lightgreen}deletion$ $\gets D(i-1,j)+1$
\State $\color{purple}match$ $\gets D(i-1,j-1)$
\State $\color{orange}mismatch$ $\gets D(i-1,j-1)+1$
\If{$A[i] = B[j]$}
\State $D(i,j) \gets$ min($\color{lightblue}insertion,\color{lightgreen}deletion,\color{orange}match$)
\Else 
\State $D(i,j) \gets$ min($\color{lightblue}insertion,\color{lightgreen}deletion,\color{purple}mismatch$)
\EndIf
\EndFor
\EndFor 
\Return $D(n,m)$
\EndProcedure
\end{algorithmic}
\end{algorithm}
```
Now that we have this matrix we can use it to find the optical alignment. 
Any path in the matrix above from $(0,0)$ to $(i,j)$ is some alignment of prefixes $A[1...i]$ and $B[1...j]$  

For example: 

![[Pasted image 20231228112429.png]]

To find the optimal alignment we use backtracking pointers from the bottom right cell along. 

```pseudo
\begin{algorithm}
\caption{OutputALignment}
\begin{algorithmic}
\Procedure{OutputAlignment}{($i,j$)}
\If{$i=0$ and $j=0$}
\State return
\EndIf
\If{backtrack($i,j$) = $\color{lightgreen} \downarrow$}
\State OutputAlignment(i-1,j)
\State print $\frac{A[i]}{-}$
\Elif{backtrack($i,j$) = $ \color{lightblue}\rightarrow$}
\State OutputAlignment(i,j-1)
\State print $\frac{-}{B[j]}$
\Else
\State OutputAlignment(i-1,j-1)
\State print $\frac{A[i]}{B[j]}$
\EndIf
\EndProcedure
\end{algorithmic}
\end{algorithm}
```
Or if you want to save space by not having to store pointers, a modified version:

```pseudo
\begin{algorithm}
\caption{OutputALignment}
\begin{algorithmic}
\Procedure{OutputAlignment}{($i,j$)}
\If{$i=0$ and $j=0$}
\State return
\EndIf
\If{$\color{lightgreen}i > 0 \text{ and }\color{lightgreen}D(i-1,j) + 1$}
\State OutputAlignment(i-1,j)
\State print $\frac{A[i]}{-}$
\Elif{$\color{lightblue}j > 0 \text{ and } D(i,j)=D(i,j-1)+1$}
\State OutputAlignment(i,j-1)
\State print $\frac{-}{B[j]}$
\Else
\State OutputAlignment(i-1,j-1)
\State print $\frac{A[i]}{B[j]}$
\EndIf
\EndProcedure
\end{algorithmic}
\end{algorithm}
```
