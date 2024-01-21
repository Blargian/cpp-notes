> You'll almost always want to override C++'s default hiding of inherited names

You do this with [[using]] declarations

```c++
class Base {
private:
  int x;
public:
  virtual void mf1() = 0; //pure virtual 
  virtual void mf1(int);
  
  virtual void mf2(); //impure virtual
  
  void mf3();
  void mf3(double);
}

class Derived : public Base {
public:
  using Base::mf1; //makes all things in Base named mf1 and mf3
  using Base::mf3; //visible (and public) in Derived's scope.

  virtual void mf1();
  void mf3();
  void mf4();
}
```

without `using Base::mf1` we would get an error in the following code:

```c++
Derived d;
int x;

d.mf1(); //okay because it's declared in Derived
d.mf1(x); //error! Derived::mf1 hides Base::mf1
```

This should technically never occur because public inheritance is a 'is-a' relationship... i.e) the derived class *is* the base class, so with public inheritance you should never want to only inherit _some_ of the public members of the base class. 

It does make sense with *[[private inheritance]]* however the technique is different. We use a simple [[forwarding function]]

```c++
class Base {
public:
  virtual void mf1() = 0;
  virtual void mf1(int);
};

class Derived : private Base {
public:
  virtual void mf1() 
  { Base::mf1(); }
};
```
## Things to remember

- Names in derived classes hide names in base classes. Under public inheritance, this is never desirable. 
- To Make hidden names visible again, employ using declarations or forwarding functions. 