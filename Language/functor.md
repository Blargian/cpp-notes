A functor is basically a class which defines `operator()`. Functors let you create *objects* which _look_ like functions, but are in fact objects. 

For example: 

```c++
struct add_x {
  add_x(int val) : x(val) {}; //constructor (member init list)
  int operator()(int y) const { return x + y; };
  private:
  int x;
}

// usage:

add_x add42(42);
int i = add42(8);
assert(i == 50); //true 
```