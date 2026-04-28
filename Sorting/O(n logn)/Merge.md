# Merge Sort (C++)

**Complexity:** $O(nlog n)$

### Brief Overview
Another algorithm following a divide and conquer approach (hence why it is logarithmic).
It divides the array/vector you want to be sorted into halves, sort these subarrays or halves, then "merges" them back to the main target array until every element has been properly sorted in whatever order you want.

Have you ever played or at least seen playing cards? You may have used them in Poker, or some other game, or even just shuffled them for show. Now let's take that shuffled deck of 52 cards of all suits (Spade, Club, Heart, and Diamond)
and try to actually sort them accordingly for Bridge in which the ranking goes as is (1 is highest and 4 is lowest):

* 1. Spades 
* 2. Hearts 
* 3. Diamonds 
* 4. Clubs 
 
Following that, if you were to sort the cards: {Ace of Clubs, 10 of Spades, 3 of Diamonds, and 7 of Spades}, you would want to put the ace first, followed by the sole diamond, then the 7 and 10 of spades, respectively.

But what if you had the full 52 deck? Would it still be optimal to check for every single card and suit individually, one by one, moving things around like performing an insertion sort? Are you willing to spend that much time?

We can move on to Merge Sort, and by following its principle: we can split the deck (array) by, lets say, 4 which accounts for each suit (subarray), it hardly matters which suit you work on first, as long as you manage to sort each
of their cards respectively, then simply following the order given earlier, "merging" them back to the full deck (main array) or the box you want to store them in, basically breaking down into more manageable bits, then building back up.

```cpp
#include <iostream>
using namespace std;

//Create a function to perform the merging of the subarrays
void merger(int arr[], int left, int mid, int right) {
    int firstHalf = mid - left + 1; //set the size of the left half
    int secondHalf = right - mid;   //set the size of the right half
    
    //Create the actual subarrays to store data per half
    int storeLeft[firstHalf], storeRight[secondHalf];
    
    //Copy the taken data to these subarrays
    for (int i = 0; i < firstHalf; i++) {
        storeLeft[i] = arr[left + i];
    }
    
    for (int j = 0; j < secondHalf; j++) {
        storeRight[j] = arr[mid + 1 + j];
    }
    
    //Perform the merging back into the array
    int i = 0;    // Initial index of first sub-array
    int j = 0;    // Initial index of second sub-array
    int k = left; // Initial index of merged sub-array
    
    while (i < firstHalf && j < secondHalf) {
        if (storeLeft[i] <= storeRight[j]) {
            arr[k] = storeLeft[i];
            i++;
        } else {
            arr[k] = storeRight[j];
            j++;
        }
        k++;
    }
    
    //Merge back remaining elements per half
    while (i < firstHalf) {
        arr[k] = storeLeft[i];
        i++;
        k++;
    }
    
    while (j < secondHalf) {
        arr[k] = storeRight[j];
        j++;
        k++;
    }
}

//Function that handles dividing into subarrays
void divider(int arr[], int left, int right) {
    if (left < right) {
        int middle = left + (right - left) / 2;

        //Recursion handling each half
        divider(arr, left, middle);
        divider(arr, middle + 1, right); 
        
        merger(arr, left, middle, right); 
    }
}

int main() {
    int numbersArr[] = {67, 100, -21, 23, 65, 98, 23112, -3232, 0, 74};
    int n = sizeof(numbersArr) / sizeof(numbersArr[0]);
    
    divider(numbersArr, 0, n - 1);
    
    for (int x = 0; x < n; x++) {
        cout << numbersArr[x] << " "; 
    }
    
    return 0;
}
```

Output: 
```
-3232 -21 0 23 65 67 74 98 100 23112
```
Runtime: * 0.09005 seconds *
