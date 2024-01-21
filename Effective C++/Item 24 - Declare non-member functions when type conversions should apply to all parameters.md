It's generally a bad idea to have classes support [[implicit conversion]]. (see pg 70-72) but sometimes you do need to do it. The question is then _should I have a member function, a non-member function or a non-member friend?_

>If you need type conversions on all parameters to a function (including the one pointed to by the _this_ pointer), the function must be a non-member. 

The example given, a class for a rational number: 

```c++
class Rational
{
public:
	Rational(int numerator=0,int denominator=1);
	int numerator() const;
	int denominator() const;
private:
};
```

It is fair to assume that we might want to implicitly convert integers to rationals. We could make `operator*` a member-function: 

```c++
class Rational
{
public:
... 
	const Rational operator*(const Rational& rhs) const; 
}
```

This design lets us multiply _rationals_ with _rationals_. 

```c++
Rational oneEighth(1,8);
Rational oneHalf(1,2);
Rational result = oneEighth*oneHalf; //fine 
result = result*oneEighth; //fine 
```

What if we want to multiply _ints_ and _rationals_? 

```c++
result = oneHalf*2; //fine
result = 2*oneHalf; // thrwows error 
```

We get an error something like: "no match for ‘operator*’ (operand types are ‘int’ and ‘Rational’)". To make it clearer write out the operator in it's functional form: 

```c++
result = oneHalf.operator*(2); //-> an integer is passed yet it is fine? 
result = 2.operator*(oneHalf); //-> integer 2 has no such operator* member function
```

Here we have [[implicit conversion]] going on! (from an _int_ to a _Rational_). If the _ctor_ is marked `explicit` then this will not work. 

We want to support mixed-mode arithmetic, i.e_ able to multiply an int and a rational in any order. In the code snippet above why does one compile and not the other? 

>parameters are eligible for implicit conversion only if they are listed in the parameter list.

I.e, only the thing in the brackets can be implicitly converted. The way around this is to declare the operator a _non member_ function. 

```c++ 
class Rational {
...
};

const Rational operator*(const Rational& lhs, const Rational& rhs) 
{
  return Rational(
    lhs.numerator()*rhs.numerator(),
    lhs.denominator()*rhs.denominator()  
  )
}
```

and now you can happily do this: 

```c++
Rational oneFourth(1,4);
Rational result;
result = oneFourth*2;  
result = 2*oneHalf; //-> integer 2 has no such operator* member function
```

We *do not* declare the operator a `non member friend` because we can implement it with `Rational`s public interface, so there is no need. 

>Don't assume that a non-member function need be a friend. Avoid friend functions whenever you can unless you really need them. 