A default swap implementation looks something like this: 

```c++
namespace std{
  template<typename T>
  void swap(T& a, T&b)
  {
    T temp(a);
    a=b;
    b=temp;
  }
}
```

As long as your types support copy constructing this is fine. However, we have three copies here which may not be ideal for _some_ types. Amongst these types are ones consisting primarily of a pointer to another type that contains the real data. eg - PIMPL ([[Item 31]]) 

```c++
class WidgetImpl {
  public:
    ...
  private:
   int a,b,c;
   std::vector<double> v;
};
```

```c++
class Widget {
  public:
    Widget(const Widget& rhs);
    Widget& operator=(const Widget& rhs)
    {
      *pImpl=*(rhs.pImpl);
    }
    
  private:
    WidgetImpl *pImpl;
}; 
```

`Swap` by default does not know that it doesn't need to make a copy of `Widget` three times, it just needs to swap out the pointers. We can fix this by specializing `std::swap`

```c++
namespace std {
  template<>
  void swap<Widget>(Widget& a, 
                    Widget& b)
  {
    swap(a.pImpl,b.pImpl);
  }
}
```

In this state it won't compile because we are missing public getters for the private `pImpl`.  "template<>" is called a [[total template specialization]]. Together with `<Widget>` after the function name this lets us decide the implementation for when the template is applied to `Widget`. 

To solve this the convention is to implement the total template specialization by having it call the member function. 

```c++
class Widget {
 public:
   void swap(Widget& other)
   {
     using std::swap;
     swap(pimpl,other.pimpl); 
   }
};

namespace std {
  template<>
  void swap<Widget>(Widget& a,
                    Widget& b)
  {
    a.swap(b); //this calls the member function swap which has access to private pimpl
  }
}
```

This is consistent with how it is done in the standard template library. 
