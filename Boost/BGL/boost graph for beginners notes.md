### Boost.Graph for Beginners Presentation

Found [this](https://www.youtube.com/watch?v=uYvBH7TZlFk) video helpful. 

- most important class is `adjacency_list`
- has core search algorithms
	- `void breadth_first_search`
	- `void depth_first_search` 
- note that those algorithms are void, so we pass 'visitors' into those algorithms. 

simplest graph possible - four vertices for top-left, top-right, bottom-left, bottom-right. With edges going either clockwise or anticlockwise.

```c++
#include <boost/graph/adjacency_list.hpp>
#include <boost/graph/adjacency_list.hpp>
#include <iostream>
#include <utility>

using namespace boost;

adjacency_list<> g;

adjacency_list<>::vertex_descriptor v1 = add_vertex(g);
adjacency_list<>::vertex_descriptor v2 = add_vertex(g);
adjacency_list<>::vertex_descriptor v3 = add_vertex(g);
adjacency_list<>::vertex_descriptor v4 = add_vertex(g);
```

almost all functions are implemented as 'global' functions (`add_vertex(g)`). Global to the namespace boost. 

```c++
typedef adjacency_list<>::vertex_iterator iterator;
std::pair<iterator,iterator> p = vertices(g);

//prints vertices: 0, 1, 2, 3
for (auto it = pfirst, it != p.second; ++it)
  std::cout << *it << std::endl;
```

to connect vertices

```c++
std::pair<adjacency_list<>::edge_descriptor,bool> p;

// adds four edges to the graph
p = add_edge(v1,v2,g);
p = add_edge(v2,v3,g);
p = add_edge(v3,v4,g);
p = add_edge(v4,v1,g);

// accesses and prints the edges (0,1), (1,2), (2,3), (3,0)
auto e = edges(g);
for (auto it = e.first; it != e.second; ++it)
  std::cout << *it << std::endl;
```

starting over, a little bit more advanced: 

```c++
adjacency_list<vecS,vecS,undirectedS> g; //vecS = vectorSelector
enum {topLeft, topRight, bottomRight, bottomLeft};

add_edge(topLeft,topRight,g);
add_edge(topRight,bottomRight,g);
add_edge(bottomRight,bottomLeft,g);
add_edge(bottomLeft,topLeft,g);
```

now to do something with the graph: 

- Core vs specialized algorithms
- Named vs non-named parameters
- Internal vs external properties 
	- Internal: Lists vs. bundled

Algorithms have both named (you can pass only some of them) and non-named parameters (you must pass the listed parameters). 

Example: for the *non-named parameter* version of breadth-first search, documentation provides: 

```c++
// non-named parameter version_
template <class Graph, class Buffer, class BFSVisitor,
 class ColorMap>
void breadth_first_search(const Graph& g,
 typename graph_traits<Graph>::vertex_descriptor s,
 Buffer& Q, BFSVisitor vis, ColorMap color);
```

and an example of how this is used: 

```c++
queue<graph::vertex_descriptor> q;
// null visitor which doesn't do anything
bfs_visit<null_visitor> vis;
// graph has 4 vertices - colormap needs 4 elements
std::array<default_color_type,4> colormap;

// pointer is automatically used as a property map
breadth_first_search(g, topLeft, q, vis, colormap.data());
```

and the other version is the *named parameter* version which has signature:

```c++
// named parameter version_
template <class Graph, class P, class T, class R>
void breadth_first_search(Graph& G,
 typename graph_traits<Graph>::vertex_descriptor s,
 const bgl_named_params<P, T, R>& params);
```

and we use it like this: 

```c++
//null visitor which doesn't do anything
bfs_visitor<null_visitor> vis;
breadth_first_search(g, topLeft, visitor(vis));
```

