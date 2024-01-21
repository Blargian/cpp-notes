Use the keyword `typename` if you have a qualified name that refers to a type and depends on a template parameter. 

For example: 

```c++
template<class T> class A
{
T::x(y); //ambiguous
typedef char C; //alias
A::C d; //illformed
}
```

The statement `T::x(y)` is ambiguous. It could be a function call to `x` with a nonlocal argument `y` or it could be a declaration of variable `y` with type `T::x`. C++ will interpret this statement as a function call, so in order for it to be interpreted as a declaration you need to add `typename T::x(y)`. 

The statement `A::C d` is ill-formed. The class A also refers to `A(T)` and thus depends on a template parameter. You must therefore add `typename A::C d;`

To understand this a bit better read [dependent names](https://en.cppreference.com/w/cpp/language/dependent_name)
