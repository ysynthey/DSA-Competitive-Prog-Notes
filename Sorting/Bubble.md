# Bubble Sort (C++)

**Complexity:** $O(n^2)$

### Brief Overview
Sort elements by continuously pushing, comparing, and moving larger elements to the right side or highest indices of a vector/array.

### Sample Code (in Ascending Order)

```cpp
#include <iostream>
#include <vector>
using namespace std;

int bubble(vector<int>& arr) { // Sort in ascending order
    int n = arr.size();

    for (int i = 0; i < n - 1; i++) { // Sets how many times we will traverse the vector
        for (int j = 0; j < n - i - 1; j++) { // Prevents the comparison from breaking and trying to access nonexistent indices
            if (arr[j] > arr[j + 1]) { // Checks if the current element is larger than the element 1 index to the right
                
                int stored = arr[j]; // Stores the current element's index being compared
                arr[j] = arr[j + 1]; // Moves target element to next position if true
                arr[j + 1] = stored; // Stores the next element
            }
        }
    }
    return -1;
}

int main() {
    vector<int> numbers = {5, 6, 7, 1, 21, 87, 67, 98, -12, 0};

    bubble(numbers);

    for (int x : numbers) {
        cout << x << " ";
    }

    return 0;
}
```

```
Output:
-12 0 1 5 6 7 21 67 87 98
```
If you want to sort in descending order, simply go to:
if (arr[j] > arr[j + 1])

and change to:
if (arr[j] < arr[j + 1])

```
Output:
98 87 67 21 7 6 5 1 0 -12
```
