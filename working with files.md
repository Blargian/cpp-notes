You can read in a file using `<fstream>` library

```c++
 std::ifstream datafile("tiny-ewg.txt");

 if (!datafile) {
   std::cerr << "tiny-ewg.txt was not found" << std::endl;
   return EXIT_FAILURE;
 };
```

you can use `std::getline` to read line by line. The default delimitor is `\n`

```c++
std::string line;
std::getline(datafile, line);
```

