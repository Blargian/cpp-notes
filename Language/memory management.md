The heap is technically called the "free store" (for longer lived variables). The terms "heap" and "free" store are used interchangeably. 

- Returns a [[pointer]] to the object or instance
- Uses a constructor to initialize the object
```c++
new
```
- Releases the memory
- Uses the destructor to do clean up
```c++
delete
```

for raw arrays:: 

```c++
new[]
delete[]
```

A good habit, is to set variables to a nullptr once you have called delete on them. 

```c++
Resource* pResource = new Resource();
delete pResource;
pResource = nullptr; //good habit 
```

