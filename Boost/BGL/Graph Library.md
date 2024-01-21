two main choices for representation:
- Adjacency list
- EdgeList

```c++
struct VertexData {
  std::string first_name;
  int num;
}

struct EdgeData {
  std::string edge_name;
  double dist;
}

void example0()
{

// define the graph type
typedef boost::adjacency_list<boost::vecS,boost::vecS,boost::directedS,boost::no_property,boost::no_property> MyGraphType
}

// adding vertices and edges to the graph
MyGraphType G;
auto v1 = add_vertex(G);
auto v2 = add_vertex(G);
auto e = add_edge(v1, v2, G);

// looping through the vertices
auto vpair = vertices(G);
for(auto iter=vpair.first; iter!=vpair.second; iter++) {
std::cout << "vertex " < *iter << std::endl;
}

// looping through the edges
auto epair = edges(G);
for(auto iter = epair.first; iter!=epair.second; iter++) {
std::cout << "edge " << source(*iter,G) << " - " << target(*iter,G) << std::endl;
}
```

Creating a graph can be done in two ways:

1. `auto g = std::make_shared<Graph>(number_of_vertices);` and then calling `add_vertex` and `add_edge`
2. `Graph g(edge_array, edge_array + sizeof(edge_array) / sizeof(Edge), num_vertices);` -> typically more efficient

We can access all of the vertices of the graph using `vertices(G)` which returns a pair where `first` is equal to the beginning iterator and `second` to an iterator past the end. The same is true for `edges(G)` however to access the vertex at the source you write `source(*iter, G)` and to get the vertex at the destination write `target(*iter,G)` 

The signature of `adjacency_list`:

`adjacency_list<OutEdgeList, VertexList, Directed,VertexProperties, EdgeProperties,GraphProperties, EdgeList>`

- `VertexList` template parameter controls what kind of container is used to represent the outer two-dimensional structure. 
- `OutEdgeList` template parameter controls what kind of container is used to control what kind of container is used to represent the EdgeLists.

Choices of these parameters impact the time and space complexity. Details found [using adjacency list](https://www.boost.org/doc/libs/1_75_0/libs/graph/doc/using_adjacency_list.html)

- Graph types can be: `directedS`,`undirectedS`,`bidirectionalS`.

It is possible to associate properties with the vertexes and edges. For instance if you want to add an associated weight/cost to each edge then you can use `boost::property<boost::edge_weight_t,double>`

see [property_types](https://www.boost.org/doc/libs/1_75_0/libs/graph/doc/using_adjacency_list.html#sec:adjacency-list-properties) for a list of the property types available. Typedefs cannot be templated. 

### Property Map 

What is a property map? Often times we just want to work with the graph without having to also work with the data associated with that graph all the time. For instance we might need to store information about the graph colouring only when running a certain algorithm. We use property maps to associate properties with vertices or edges.  

Properties on a graph can be 
1. internally stored (properties attached for the lifetime of the graph)
2. externally stored (properties which can be temporarily used)

Properties are attached to the vertices or edges of a graph via the property interface on adjacency_list where `VertexProperties` or `EdgeProperties` are specified -> `adjacency_list<OutEdgeList, VertexList, Directed,VertexProperties, EdgeProperties,GraphProperties, EdgeList>`. 

These can be attached in two ways: with [bundled properties] or with [property lists]. 

with property lists:

```c++
typedef property <vertex_distance_t,float,property<vertex_name_t,std::string>> VertexProperty;
typedef property<edge_weight_t, float> EdgeProperty;
typedef adjacency_list<mapS, vecS, undirectedS,
                         VertexProperty, EdgeProperty> Graph;
  Graph g(num_vertices); // construct a graph object
```

We then read and write property values using property maps. For internal properties we can get the property map using the `get` function. 

There are two different kinds of `get()` functions.

1. Takes parameters relative to the graph and return to you a property map `get(boost::edge_weight_t(),*g);`
2. Takes a property map and instead of a graph reference takes an edge or vertex reference and returns to you the value of that property. `get(weightMap, e)`

#### Exterior Properties 

How to construct exterior property maps:
1. using the adapter class `iterator_property_map`

### Out Edges and Inner Edges

`out_edges` returns the out going edges of some vertex. `in_edges` returns the inner edges. These are only relevant if the graph is `directed`, otherwise in an undirected graph both `out_edges` and `in_edges` will return all the edges connecting to the node in question. 
### Own Examples

Code for reading in edges with associated weights: 

```c++
#include <iostream>
#include <memory>
#include <vector>
#include <boost/graph/properties.hpp>
#include <boost/graph/graph_traits.hpp>
#include <boost/graph/adjacency_list.hpp>
#include <boost/property_map/property_map.hpp>

// 8
// 16
// 4 5 0.35
// 4 7 0.37
// 5 7 0.28
// 0 7 0.16
// 1 5 0.32
// 0 4 0.38
// 2 3 0.17
// 1 7 0.19
// 0 2 0.26
// 1 2 0.36
// 1 3 0.29
// 2 7 0.34
// 6 2 0.40
// 3 6 0.52
// 6 0 0.58
// 6 4 0.93

int main() {
    const int number_of_vertices = 8;
    const int number_of_edges = 16; 

    using Edge = std::pair<int,int>;
    const std::vector<double> weights = {0.35,0.37,0.28,0.16,0.32,0.38,0.17,0.19,0.26,0.36,0.29,0.34,0.40,0.52,0.58,0.93};
    const std::vector<Edge> edges = {
        Edge(4,5),
        Edge(4,7),
        Edge(5,7),
        Edge(0,7),
        Edge(1,5),
        Edge(0,4),
        Edge(2,3),
        Edge(1,7),
        Edge(0,2),
        Edge(1,2),
        Edge(1,3),
        Edge(2,7),
        Edge(6,2),
        Edge(3,6),
        Edge(6,0),
        Edge(6,4)
    };

      using VertexProperties = boost::no_property;
    //using EdgeProperties = boost::property<boost::edge_weight_t,double>;
      struct EdgeProperties {
        double weight;
      };

    using Graph = boost::adjacency_list<
      boost::vecS, // OutEdgeList type
	  boost::vecS, // VertexList type
	  boost::directedS, // type of graph (directed)
	  VertexProperties,
	  EdgeProperties
    >;

    Graph g = Graph(number_of_edges);
    auto weight = boost::get(&EdgeProperties::weight,g); //property map for weight
    
    for(int i=0; i < number_of_edges; i++) {
        boost::add_edge(edges[i].first,edges[i].second,{weights[i]},g);
    };

    boost::graph_traits<Graph>::edge_iterator ei, ei_end;
    for (boost::tie(ei,ei_end) = boost::edges(g); ei != ei_end; ei++) {
        std::cout << "(" << boost::source(*ei,g) << " , " << boost::target(*ei,g) << ") : " << weight[*ei] << "\n";
    }
}
```

which outputs: 

```console
(0 , 7) : 0.16
(0 , 4) : 0.38
(0 , 2) : 0.26
(1 , 5) : 0.32
(1 , 7) : 0.19
(1 , 2) : 0.36
(1 , 3) : 0.29
(2 , 3) : 0.17
(2 , 7) : 0.34
(3 , 6) : 0.52
(4 , 5) : 0.35
(4 , 7) : 0.37
(5 , 7) : 0.28
(6 , 2) : 0.4
(6 , 0) : 0.58
(6 , 4) : 0.93
```

### Dijkstras example with own explanations 

```c++
#include <boost/config.hpp>
#include <iostream>
#include <fstream>

#include <boost/graph/graph_traits.hpp>
#include <boost/graph/adjacency_list.hpp>
#include <boost/graph/dijkstra_shortest_paths.hpp>
#include <boost/property_map/property_map.hpp>

using namespace boost;

int main(int,char*[])
{
    typedef adjacency_list<listS, vecS, directedS, no_property, property<edge_weight_t,int>> graph_t;
    typedef graph_traits<graph_t>::vertex_descriptor vertex_descriptor;
    typedef std::pair<int,int> Edge;

    const int num_nodes = 5;
    enum nodes 
    {
      A,B,C,D,E
    };
    char name[] = "ABCDE";
    Edge edge_array[] = {Edge(A,C), Edge(B,B), Edge(B,D), Edge(B,E),Edge(C,B),Edge(C,D),Edge(D,E),Edge(E,A),Edge(E,B)};
    int weights[] = {1,2,1,2,7,3,1,1,1};
    int num_arcs = sizeof(edge_array)/sizeof(Edge);

    graph_t g(edge_array, edge_array + num_arcs, weights, num_nodes);
    property_map<graph_t,edge_weight_t>::type weightmap = get(edge_weight,g);
    std::vector<vertex_descriptor> p(num_vertices(g));
    std::vector<int> d(num_vertices(g));
    vertex_descriptor s = vertex(A,g); //descriptor of vertex A i.e starting point

dijkstra_shortest_paths
 (
  g, 
  s,
  predecessor_map (
   make_iterator_property_map(
    p.begin(),
    get(vertex_index,g)
   )
  ).distance_map (
   make_iterator_property_map(
     d.begin(),
     get(boost::vertex_index,g)
   )
  )
  );   
}
```

The call to Dijkstra can be a little confusing

```c++
dijkstra_shortest_paths
 (
  g, 
  s,
  predecessor_map (
   make_iterator_property_map(
    p.begin(),
    get(vertex_index,g)
   )
  ).distance_map (
   make_iterator_property_map(
     d.begin(),
     get(boost::vertex_index,g)
   )
  )
  );  
```

the first parameter `g` is the graph. `s` is a descriptor of a vertex that you want as your starting point. The third parameter is a `# bgl_named_params<Param, Type, Rest>` [[bgl_named_params]]. 

`predecessor_map` and `distance_map` come from the documentation and are the required named parameters. They are used as a kind of 'wrapper' around the actual property map because the order you pass them in doesn't matter. 

`predecessor_map().distance_map()` and `distance_map().predecessor_map()` will yield the same results. 

Therefore we pass the actual parameter map into these "wrappers" so that the function knows "okay, this parameter map is the predecessor_map" or "okay, this parameter map is the distance_map". 

`make_iterator_property_map` is a function for conveniently creating an iterator map. We use the first of the two calls below in the example above:

```c++
template <class RAIter, class OffsetMap>
  iterator_property_map<RAIter, OffsetMap,
    typename std::iterator_traits<RAIter>::value_type,
    typename std::iterator_traits<RAIter>::reference
    >
  make_iterator_property_map(RAIter iter, OffsetMap omap)
```
or 
```c++
  template <class RAIter, class OffsetMap, class ValueType>
  iterator_property_map<RAIter, OffsetMap,
    typename std::iterator_traits<RAIter>::value_type,
    typename std::iterator_traits<RAIter>::reference
    >
  make_iterator_property_map(RAIter iter, OffsetMap omap, ValueType dummy_arg)
```
