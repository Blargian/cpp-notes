is a [[dynamic programming]] problem 

> Given two strings, remove all symbols from two strings in such a way that the number of points is maximized: 

```
A T G T T A T A
A T C G T C C
```

Scoring: 

- Remove the 1st symbol from *both* strings:
	- 1 point if the symbols match
	- 0 points if they don't match
- Remove the 1st symbol from one of the strings:
	- 0 points

When you remove a symbol the string symbols shift left each time. We can insert a '-' whenever we remove a character from the string. In this way we get a sequence alignment matrix.

![[Pasted image 20231228085011.png]]
match: +1
mismatch: $-\textmu$ 
indel: -$\sigma$

Alignment score: $\text{no.matches} - \mu .\text{no.mismatches} - \sigma . \text{indels}$

Minimizing [[edit distance]] = maximizing [[alignment score]]
