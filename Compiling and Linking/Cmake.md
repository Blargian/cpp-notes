https://cliutils.gitlab.io/modern-cmake/chapters/intro/dodonot.html

```
mkdir build
cd build
cmake ..
```

### Minimum Version

In `CMakeLists.txt` the first line will be

```cmake
cmake_minimum_required(VERSION 3.1)
```

This is important because policies are different with different versions of CMake.

### Setting a Project

```CMake
project(MyProject VERSION 1.0
                  DESCRIPTION "this is my project"
                  LANGUAGES CXX)
```

language options are `C`,`CXX`,`Fortran`,`ASM`,`CUDA` (CMake 3.8+), `CSharp`, `SWIFT`

comments are made with `#`


[targets] in CMake are [executables], [libraries] and [utilities] build by CMake. 
### Making an executable

```cmake
add_executable(one two.cpp three.h)
```
### Making a library

```CMake
add_library(one STATIC two.cpp three.h)
```
options are `STATIC`, `SHARED`, `MODULE` and if you don't fill this in then `BUILD_SHARED_LIBS` will be used to pick between `STATIC` and `SHARED`. 

we then specify information about those targets 

```CMake
target_inlcude_directories(one PUBLIC include)
```

```cmake
add_library(another STATIC another.cpp another.h)
target_link_libraries(another PUBLIC one)
```

`target_link_libraries` takes a target (first argument) and adds a dependency if a target is given (remaining arguments). If no target of that name exists, then it adds a link to a library of that name. 

### Local Variables

local variables are set like this 

```cmake
set(MY_VARIABLE "value")
```

You can then access that variable by writing `${MY_VARIABLE}`

```cmake
set(MY_LIST "one" "two")
set(MY_LIST "one;two")
```

are the exact same. Never write `${MY_PATH}` but always `"${MY_PATH}"` 

### Default Build Type

```cmake
set(default_build_type "Release")
if(NOT CMAKE_BUILD_TYPE AND NOT CMAKE_CONFIGURATION_TYPES)
  message(STATUS "Setting build type to '${default_build_type}' as none was specified.")
  set(CMAKE_BUILD_TYPE "${default_build_type}" CACHE
      STRING "Choose the type of build." FORCE)
  # Set the possible values of build type for cmake-gui
  set_property(CACHE CMAKE_BUILD_TYPE PROPERTY STRINGS
    "Debug" "Release" "MinSizeRel" "RelWithDebInfo")
endif()
```

### Copying across DLLs

```cmake
# Copy across .dlls for windows users
get_target_property(SFML_TYPE sfml-graphics TYPE)
if(SFML_TYPE STREQUAL "SHARED_LIBRARY")
  message(STATUS "Copying DLLs to ${CMAKE_CURRENT_BINARY_DIR}/$<CONFIG>")
  add_custom_command(
    TARGET sorting-visualizer POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy
    $<TARGET_FILE:sfml-graphics>
    ${CMAKE_CURRENT_BINARY_DIR}/$<CONFIG>)
endif()
```

What is going on here? 
- `add_custom_command`
- generator expressions `$$<TARGET_FILE:sfml-graphics>` evaluates true if the target file exists

### Copying across files

```CMake
add_custom_command(
        TARGET foo POST_BUILD
        COMMAND ${CMAKE_COMMAND} -E copy
                ${CMAKE_SOURCE_DIR}/test/input.txt
                ${CMAKE_CURRENT_BINARY_DIR}/input.txt)
```

You can choose between `PRE_BUILD`, `PRE_LINK`, `POST_BUILD`