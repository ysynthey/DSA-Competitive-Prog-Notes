# Selection Sort (C++)

**Complexity:** $O(n^2)$

### Brief Overview
Sort elements accordingly in ascending/descending order by creating gaps between indices by shifting right and leftward, then inserting an element to fill in that gap.

Suppose you work at a library and is tasked with sorting each book in a certain shelf (array/vector) by their ID number which we will assume is a 7-digit integer starting at 0000000.
At the beginning, every book is of course, unsorted and you might be thinking of moving them one by one until it is all sorted.

But we can apply the principle of Insertion Sort in this scenario, where instead we will be moving books left and right, 
creating gaps between them, and inserting a book we pulled out between them until it is fully sorted.

### Sample Code (in Ascending Order)

```cpp
#include <iostream>
#include <vector>
using namespace std;

void insertion(vector<int>& arr) {
	int n = arr.size();
		// For insertion sort, we would want to start at index 1 or element #2
	for (int i = 1; i < n; i++) {
		// Create a variable based on index i before it incremenets, which is what we "insert"
		int key = arr[i];
		// Inner Loop initialization denoted by the leftward or previous element
		int j = i - 1;
		
			// Inner While loop handles the actual sorting
			while (j >= 0 && arr[j] > key) {
				
				//Shift the element being checked rightward by 1
				arr[j + 1] = arr[j];
				//Moving Leftward
				j = j - 1;
			}
			
			//Insert the key element into the correct "gap"
			arr[j + 1] = key;
	}
}
int main() {
    vector<int> numbers = {41, 56, 67, 43, 12, 56, -100, 0, 24};

    insertion(numbers);

for (int x : numbers) {
	cout << x << " ";
}
	
	
	return 0;
}

```
