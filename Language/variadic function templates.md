Use a [[parameter pack]]
```c++
#include <iostream>

template <typename T>
T Sum(T arg) {
    return arg;
}

template <typename T, typename... Args>
T Sum(T start, Args... args){
    return start + Sum(args...);
}

int main() {
    std::cout << Sum<int>(1,2,3,4,5) << std::endl;
    return 0;
}
```