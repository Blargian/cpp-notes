C++ implements genericity with templates 
- resolved at compile time 
- no runtime checks 

Why?
Write a class or function once. 

- Example - average, largest, smallest.
- Type safe collections.
- Often rely on operator overloads

> much of the standard library is template-based. It even used to be called "the standard template library". 

### template functions 

```c++
template <class T>
T max(T const& t1, T const& t2)
{
  return t1 < t2 ? t2: t1;
};
```
we take them by `const` reference as we could be taking in some big object or some basic type like an int. 

then we can use it: 

```c++
max(33,34);
max(x,0);
max(s1,s2); //eg strings "hello" and "world" returns "world" as w > h
max(p1,p2); //eg person objects but only if you have operator< on that object
max<double>(33,2.0) //will do a double version
```

### template classes

```c++
template <class T>
class Accum
{
private:
  T total;
public:
  Accum(T start): total(start) {};
  T operator+=(T const&t) 
  {return total = total+t;}
  T GetTotal() const {return total;}
};
```

### template specialization

sometimes a template won't work for a particular class
example - your class doesn't have the operator that's needed. 