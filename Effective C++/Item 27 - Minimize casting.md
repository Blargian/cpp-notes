- approach casting with great respect in C++ 

old style C++ casts:
- `(T)expression`
- `T(expression)`

new style C++ casts (which are _preferable_):

- `const_cast<T>(expression)` $\to$ used to cast away constness  
- `dynamic_cast<T>(expression)` $\to$ used to perform "safe downcasting". May have a significant runtime cost. 
- `reinterpret_cast<T>(expression)` $\to$ rare outside of low-level code
- `static_cast<T>(expression)` $\to$ used to force implicit conversions

```c++
class Base {...};
class Derived: public Base {...};
Derived d;
Base *pb = &d; //implicitly convert Derived* = Base*
```

sometimes the pointer values will not be the same. When that's the case, an offset is applied at _runtime_ to the Derived* pointer to get the correct Base* pointer value. 

In C++ a single object might have more than one address. 
- it's address when pointed to by a Base* pointer 
- It's address when pointed to by a Derived* pointer
