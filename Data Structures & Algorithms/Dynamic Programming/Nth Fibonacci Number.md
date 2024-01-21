Write a function that returns nth Fibonacci number
$$
\begin{align} 
F_1 &= F_{2 = 1} \\
F_{n} &= F_{n-1} + F_{n-2}
\end{align}
$$
a simple recursive solution:
```python
def fib(n):
	if n <= 2:
		result = 1
	else:
		result = fib(n-1) + fib(n-2)
	return result
```

`fib(50)` will take a _really_ long time to finish. We end up reusing a lot of the same results for recursive calls to `fib(n)` 

We use [[memoization]] to improve the run time. 

```python
memo = {}
def fib(n):
    if n in memo:
	    return memo[n]
	if n <= 2:
		result = 1
	else:
		result = fib(n-1) + fib(n-2)
	memo[n] = result
	return result
```

