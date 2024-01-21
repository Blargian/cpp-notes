## Namespaces 
- use namespaces whenever possible
- do not use `using` directives 
## Constructor Initializer Lists

all on one line or with subsequent lines indented four spaces 

```c++
MyClass::MyClass(int var) : some_var_(var) {
	DoSomething();
}

//signature and initializer list not on the same line:

MyClass::MyClass(int var)
	: some_var_(var), some_other_var_(var +1) {
  DoSomething();
}

// When the list spans multiple lines, put each member on its own line
// and align them 

MyClass:MyClass(int var)
	: some_var_(var),
	  some_other_var_(var+1) {
  DoSomething();
}
  
```

