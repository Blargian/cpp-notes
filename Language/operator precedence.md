
| Precedence | Operator |
| ---- | ---- |
| 1 | :: |
| 2 | `a++ a--`<br>`type() type{}`<br>`a()`<br>`a[]`<br>`. ->` |
| 3 | `++a --a`<br>`+a -a` |
|  |  |
Mistakes I've made before: 

`return MinNumCoins[money-1]` $\rightarrow$ incorrect because `[]` is higher precedence than `-a` 