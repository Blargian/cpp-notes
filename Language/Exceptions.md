- Not every action succeeds 
	- some are predictable
	- some are not 
	- different errors should be handled in different ways 

expected errors $\to$ test for them, handle them immediately. 

Problem:
>Sometimes the code that finds the problem can't deal with it. We could return true or false if everything goes okay, but sometimes we don't want to do this because we're already returning something else or else we can't return anything eg) from the constructor. Often developers forget to deal with these issues.  

With exceptions we _transfer the flow of execution_ 
[[stack unwinding]]

1. Wrap code that might throw in a try block which is as small as possible
2. Add one or more catch blocks after the try 
3. Catch more specific exceptions first 
4. Catch exceptions by reference 

In the example below we catch `out_of_range& oor` first because it derives from `exception& e`. If we put the more specific catch block first, we would never reach it. 

```c++
try 
{
  //some risky stuff
}
catch (out_of_range& oor)
{
  //react 
}
catch (exception& e)
{
  //react 
}
```

A more practical example: 

```c++
using namespace std
#include <iostream>
#include <exception>
using std::cout 
using std::exception;
using std::out_of_range;

int main()
{
  std::vector<int> v;
  v.push_back(1);
  try 
  {
    int j = v.at(99);
  }
  catch (out_of_range& e)
  {
    cout << " out of range exception " << e.what();
  }
  catch (exception& e)
  {
    cout << e.what();
  }
  return 0;
}
```

The syntax is simple but knowing what to throw is tricky in C++ because you can throw anything... you can even throw an int. 

`std::exception` has two main derived classes ([[marker class]]):
- `logic_error` 
- `runtime_error`  

---
### noexcept

you can mark a function `noexcept` - appears to mean that the function won't throw, but it's just saying "this is a function not worth throwing". 

What happens if a function marked `noexcept` does throw? 

- App terminates
- No [[stack unwinding]]

When would you use this? For instance when you can't even construct four bytes. 

---
### Enabling moves with noexcept 

if a move operation throws, the enclosing operation can't be rolled back.

> some moving operations in std:: will only call noexcept functions. eg) Move ctor, move op=, swap




