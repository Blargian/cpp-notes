A [struct] works similarly to a class, however it's members are *public* by default. We use it to group related variables into one _structure_

In the code below we declare a struct called S: 

```c++
struct {
  int x;
  bool b;
} S; 
```

The common idiom is to combine `typedef` ([[typedef]]) with struct like this:

```c
typedef struct S { 
    int x; 
} S;
```

They are different definitions. To make the discussion clearer I will split the sentence:

```c
struct S { 
    int x; 
};

typedef struct S S;
```

In the first line you are defining the identifier `S` within the struct name space (not in the C++ sense). You can use it and define variables or function arguments of the newly defined type by defining the type of the argument as `struct S`:

```c
void f( struct S argument ); // struct is required here
```

The second line adds a type alias `S` in the global name space and thus allows you to just write:

```c
void f( S argument ); // struct keyword no longer needed
```
