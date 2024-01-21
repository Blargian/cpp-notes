An enum is a convenient way to 'label' integer values. For instance:

```c++
enum NoteValues{

  whole = 1,

  half = 2,

  quarter = 4,

  eigth = 8,

  sixteenth = 16,

  dotted_eigth = 12,

  dotted_sixteenth = 24

};
```

Now if you write `whole` it will evaluate to 1. 

You also get a [[scoped enum]] which is `enum class NoteValues {}`. It now has a namespace and you have to write `NoteValues::whole` instead of `whole`. Not until C++20 can you use `using namespace NoteValues`. 