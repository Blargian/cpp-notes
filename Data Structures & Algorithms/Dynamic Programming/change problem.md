*input*: integer money and positive integers representing coin denominations `coin1,...,coind`
*output*: Minimum number of coins with denominations `coin1,...,coind` that changes money. 

### Greedy approach 
This is the approach that a cashier in a shop would take: 
```pseudo
\begin{algorithm}
\caption{GreedyChange(money)}
\begin{algorithmic}
\Procedure{GreedyChange}{$money$}
\State $Change \gets$ empty collection of coins
\While{$money > 0$}
\State $coin \gets$ largest denomination that does not exceed money
\State add $coin$ to $Change$
\State $money \gets money - coin$
\EndWhile
\Return $Change$
\EndProcedure
\end{algorithmic}
\end{algorithm}
```
eg ) 40 cents = 25 + 10 +5 in the US; 40 cents = 20 + 20 cents (Tanzania). 

### Recursive Change 

Given the denominations `6,5,1`, what is the minimum number of coins needed to change 9 cents? 

$$
\begin{equation}
MinNumCoins(9) = \min 
\begin{cases}  
\text{MinNumCoins(3)+1} \\
\text{MinNumCoins(4)+1} \\ 
\text{MinNumCoins(8)+1} \\
\end{cases}
\end{equation}
$$
Well we can break this problem down into smaller problems. Let's examine just one denomination - 3 cents. We know that we will have to give back at least one coin, so we want to work out $MinNumCoins(9-3)$ which will give us some value at least 1. We can repeat this for all of the denominations. Finally we need to take the minimum of these sub problems to find our answer. 

```pseudo
\begin{algorithm}
\caption{RecursiveChange(money,coins)}
\begin{algorithmic}
\Procedure{RecursiveChange}{money,coins}
\If{money = 0} 
\Return 0
\EndIf
\State MinNumCoins $\gets \infty$
\For{i from 1 to $|coins|$}
\If{money $ \ge coin_i$}
    \State NumCoins $\gets$ RecursiveChange(money-$coin_i$,coins)
    \If{NumCoins + 1 $\lt$ MinNumCoins}    
    \State MinNumCoins $\gets$ NumCoins+1
    \EndIf        
  \EndIf  
\EndFor
\Return MinNumCoins
\EndProcedure
\end{algorithmic}
\end{algorithm}
```
Our base case for which we will stop recursing is when $money = 0$. What will happen is that there will be $n$ recursive calls in which money will decrease by the coin denomination each time. 

For instance, if $money=10$ and denomination is $1$, we will have:
$$\begin{align}
\newline RecursiveChange(9-1)
\newline RecursiveChange(8-1)
\newline RecursiveChange(7-1)
\newline ...
\newline RecursiveChange(1-1)
\end{align}
$$
at this point money is 0 and we start to 'unwind' back up. On the way back up $MinNumCoins$ increases by one value of the denomination for each of the denominations. This repeats for however many $n$ calls of $RecursiveChange$ deep we are. When the condition of $NumCoins + 1 < MinNumCoins$ is no longer met $MinNumCoins$ is returned.

The program is elegant but it will take a very long time to finish. You can see below that we have repeated calls for certain sub problems. 

![[Pasted image 20231227160010.png]]

This is where [[dynamic programming]] comes in - we can compute the result only once, store it and then use it later instead of having to calculate it again. 

### Dynamic Programming Solution 

With dynamic programming we take a bottom up approach and we compute every value from 0 to $money$ and we'll store all of these values in an array so that we can use them later. 

We end up computing the following table:

![[Pasted image 20231227160435.png]]

```pseudo
\begin{algorithm}
\caption{DPChange(money,coins)}
\begin{algorithmic}
\Procedure{DPChange}{money,coins}
\State $MinNumCoins(0) \gets 0$
\For{m from 1 to $money$}
\State $MinNumCoins(m) \gets \infty$
\For{i from 1 to |$coins$|}
\If{$ m \geq coin_i$}
  \State $NumCoins \gets MinNumCoins(m-coin_{i})+ 1$
  \If{$NumCoins \lt MinNumCoins(m)$} 
  \State $MinNumCoins(m) \gets NumCoins$
  \EndIf
\EndIf
\EndFor
\EndFor
\Return $MinNumCoins(money)$
\EndProcedure
\end{algorithmic}
\end{algorithm}

```
