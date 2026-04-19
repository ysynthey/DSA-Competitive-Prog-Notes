# Selection Sort (C++)

**Complexity:** $O(n^2)$

### Brief Overview 
Sort elements by scanning for the element with the least value in an unsorted index then moving it to a sorted position until fully sorted.

### Sample Code (in Ascending Order)

```cpp
#include <iostream>
#include <vector>
using namespace std;

int Selection(vector<double>& arr) {
    int n = arr.size();
    
    for (int i = 0; i < n - 1; i++) { //using n - 1 to dynamically set how many iterations to do depending on array/vector size
        int minIndex = i; //starting at element 1
        for (int j = i + 1; j < n; j++) { //j starts at element 2, hence i + 1
            if (arr[j] < arr[minIndex]) { //comparing the target element to the first element
                minIndex = j; //if true, that becomes the new least element
            }
        }
        
        if (minIndex != i) { //checks if the first element isnt already the least and then swap if they aren't
            double temp = arr[i]; //set up temp variable to store previous index
            arr[i] = arr[minIndex];  //move the smallest element to the first index
            arr[minIndex] = temp; //take the temporary element then set that as the minimum
        }
    }
    return -1;
}
int main() {
    vector<double> doubles = {2.22, 1.11, 3.33, 5.55, 7.77, 4.44, 9.99, -1.11, -5.55, 0};

    Selection(doubles);
    
    for (double x: doubles) {
        cout << x << " ";
    }

    return 0;
}
```

```
Output:
-5.55 -1.11 0 1.11 2.22 3.33 4.44 5.55 7.77 9.99
```

If you want to sort in descending order, simply go to:
```cpp
if (arr[j] < arr[minIndex]) {
  minIndex = j;
}
```

and change to >.
