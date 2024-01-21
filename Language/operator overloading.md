
Difference between ++prefix and postfix++:

```c++
operator++()         => Prefix Increment
operator--()         => Prefix Decrement

operator++(int)      => Postfix Increment
operator--(int)      => Postfix Decrement
```

Overloading comparison operators:

```c++
struct Record
{
    std::string name;
    unsigned int floor;
    double weight;
 
    friend bool operator<(const Record& l, const Record& r)
    {
        return [std::tie](l.name, l.floor, l.weight)
             < [std::tie](r.name, r.floor, r.weight); // keep the same order
    }
};
```