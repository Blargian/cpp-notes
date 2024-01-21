
> Given an array `nums` with `n` objects colored red, white, or blue, sort them **[in-place](https://en.wikipedia.org/wiki/In-place_algorithm)** so that objects of the same color are adjacent, with the colors in the order red, white, and blue.
>We will use the integers `0`, `1`, and `2` to represent the color red, white, and blue, respectively.
>You must solve this problem without using the library's sort function.

**Example 1:**

**Input:** nums = [2,0,2,1,1,0]
**Output:** [0,0,1,1,2,2]

**Example 2:**

**Input:** nums = [2,0,1]
**Output:** [0,1,2]

- we use three pointers - low, mid and high

1. Everything left of the low pointer is low values
2. From low pointer to the left of the mid pointer are mid values
3. From mid pointer to the high pointer are unknown values
4. Everything right of the right pointer is high values

![[Pasted image 20231022101426.png]]


the implementation looks like this. We consider only if a value is 0, 1, 2:

```c++
class Solution {
public:
    void sortColors(std::vector<int>& nums) {
        
        int low = 0, middle = 0; 
        int high = nums.size()-1;
        int x = nums[high];

        while (middle <= high) {
        switch(nums[middle]) {
          case 0:
            std::swap(nums[low++],nums[middle++]);
            break;
          case 1:
            middle++;
            break;
          case 2:
            std::swap(nums[middle],nums[high--]);
            break;
          default:
            break;
        }     
    }
    };
};
```


---

## Partition3 (QuickSort Partition)

This algorithm can also be applied for partitioning an array into three areas to speed up [[quick sort]] for cases where there are few unique values. The only difference here is that we don't use a case statement for 0,1,2 but we just compare values against a pivot value, in this case. Again:

- for $<$ we swap low and mid, increment the start and middle pointers
- for $==$ we increment the middle pointer 
- for $>$ we swap middle and high, decrement -- 

```c++
void partition(int a[], int low, int high, int& i, int& j)
{
    // To handle 2 elements
    if (high - low <= 1) {
        if (a[high] < a[low])
            swap(&a[high], &a[low]);
        i = low;
        j = high;
        return;
    }
 
    int mid = low;
    int pivot = a[high];
    while (mid <= high) {
        if (a[mid] < pivot)
            swap(&a[low], &a[mid]);
            low++;
            mid++;
        else if (a[mid] == pivot)
            mid++;
        else if (a[mid] > pivot)
            swap(&a[mid], &a[high]);
            high--;
    }
 
    // update i and j
    i = low - 1;
    j = mid; // or high+1
}
```
