When an exception is thrown
$\to$ If in a try, everything local to the try block goes out of scope
- Destructors go off 
- Control goes to the catch 
$\to$ If not, everything local to the function goes out of scope 
- control returns to where that function was called from 
- Recurse to "if in a try" above 

> Stack unwinding before going into a catch makes RAII such a powerful thing to do - without it we no longer have access to the thing in the try so that we can clean it up. 

