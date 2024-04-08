Reference: https://www.youtube.com/watch?v=EhinJ94emf8&list=PLvv0ScY6vfd8j-tlhYVPYgiIyXduu6m-L&index=38

For classes you get by default compiler generated:
- a default constructor
- a default destructor
- a default [[copy constructor]]
- a [[copy-assignment operator]]

The default constructor and destructor can be overwritten when we want to implement our own logic on construction or destruction. There can be more than one constructor:

```c++
class Student
{
public:
    Student();
    Student(std::string name);
private:
    std::string m_name;
}
```

In modern C++ we have the [[member-initialization list]] as a common way of declaring constructors. 

