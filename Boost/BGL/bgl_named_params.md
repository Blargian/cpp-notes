What the heck is `bgl_named_params` you ask? Excellent question! 
Allows the user to provide parameters in any order, and matches arguments to parameters based on parameter names. Each named parameter is separated by `.` a period, and not a comma. 

For instance:

```c++
bool r = boost::bellman_ford_shortest_paths(g, int(N),
     boost::weight_map(weight).
     distance_map(&distance[0]).
     predecessor_map(&parent[0]));
```

Here we passed three parameters which were a `weight_map`, a `distance_map` and a `predecessor_map`. 