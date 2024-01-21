closely related to [[find_if]]
`find` searches for an element equal to value (using `operator==`).

```c++
 const auto v = {1, 2, 3, 4};
 
    for (const int n : {3, 5})
        (std::find(v.begin(), v.end(), n) == std::end(v)
            ? std::cout << "v does not contain " << n << '\n'
            : std::cout << "v contains " << n << '\n';
```
