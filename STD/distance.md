`std::distance` defined in `<iterator>`

*NB - `std::distance(it, somevector.begin())` will not work as expected. You need to have the beginning iterator first, because the function counts the hops. Like this:

```c++
std::distance(somevector.begin(), it)
```



