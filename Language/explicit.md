Specifies that a constructor is [[explicit]] meaning that it cannot be used for [[implicit conversion]] and [[copy-initialization]] 

```c++
explicit CTor(int var) {};
```

For instance, you might have some class which represents a Rational number. see [[Item 24 - Declare non-member functions when type conversions should apply to all parameters]] 

The _Rational_ has an `operator*` of the following signature `const Rational operator*(const Rational& rhs) const;`

In the following code 

```c++
Rational oneHalf(1,2);
Rational result=oneHalf*2
```

This line will only compile if the constructor of `Rational` is not declared explicit. Why? Because the compiler treats the code above effectively as this: 

```c++
Rational temp = Rational(2); 
Rational result = oneHalf*temp; //operator* taking a rational is found
```

but if we have an explicit constructor then the compiler sees that it cannot implicitly convert an int to a type Rational. 