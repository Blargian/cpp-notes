Compute the number of inversions in a sequence of integers

eg) given `[3,2,5,9,4]`, the function should return `3` which is an inversion from 3 to 2, from 5 to 4 and from 9  to 4. 

The brute force approach is simple: 

```c++
//O(n^2) time complexity solution -> naive 
long long get_number_of_inversions_naive(const std::vector<int> &a) {
  long long number_inversions = 0;

  for (auto it_outer = a.begin(); it_outer < a.end(); it_outer++) {
    for (auto it_inner = it_outer+1; it_inner < a.end(); it_inner++) {
      if ( *it_inner < *it_outer)
        number_inversions++;
    }
  }

  return number_inversions;

}
```

However to speed this up we can use a trick of modifying the merge sort to count inversions. 

