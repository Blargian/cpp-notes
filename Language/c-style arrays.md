```c++
int melody[] = {};
```

to get the `sizeof` you need to do this: `size_t size = sizeof(melody)/sizeof(melody[0]) `
