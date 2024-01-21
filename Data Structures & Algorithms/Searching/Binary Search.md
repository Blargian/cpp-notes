Runs in $O(logn)$

C++ code: 

A recursive solution: 

```c++
int binarySearch(int arr[], int l, int r, int x)
{
    if (r >= l) {
        int mid = l + (r - l) / 2;
 
        // If the element is present at the middle
        // itself
        if (arr[mid] == x)
            return mid;
 
        // If element is smaller than mid, then
        // it can only be present in left subarray
        if (arr[mid] > x)
            return binarySearch(arr, l, mid - 1, x);
 
        // Else the element can only be present
        // in right subarray
        return binarySearch(arr, mid + 1, r, x);
    }
 
    // We reach here when element is not
    // present in array
    return -1;
}
```

or a non-recursive solution: 

```c++
int binary_search(const vector<int> &a, int x) {
  int left = 0, right = a.size()-1;
  while ( right >= left ) {
    int middle = (left+right)/2;
    if (a[middle] == x) {
      return middle;
    } else if ( a[middle] < x ) {
      left = middle + 1;
    } else {
      right = middle - 1;
    }
  }
  return -1;
}
```