specifier `final`
## used with a class or member function

```c++
struct Base
{
	virtual void foo();
};

struct A : Base
{
	void foo() final; // Base foo is overwritten and A foo is the final override
	void bar() final; // Error - can only be used with virtual functions
};

struct B final : A
{
	void foo() override; // Erro: foo cannot be overwritten as it is final in A
};

struct C : B {}; // Error B is final, cannot inherit from it
```

Example: 

In ClickHouse Formats that inherit from `IRowInputFormat` are marked `final`

```c++
class TSKVRowInputFormat final : public IRowInputFormat
{
// ... stuff
}
```