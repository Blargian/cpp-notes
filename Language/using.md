[using keyword] `using` can be used to alias a type, such as 

```c++
using vertex_iter = graph_traits<Graph>::vertex_iterator;
``` 

You can prefer `using` to [[typedef]] which is from C and has weird syntax. The same thing using a typedef would look like: 

```c++
typedef graph_traits<Graph>::vertex_iterator vertex_iter;
```



`