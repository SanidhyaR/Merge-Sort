#**Merge Sort**

__Donald Knuth__
>Everyday life is like programming, I guess. If you love something you can put beauty on it. -Donald Knuth__

There are a lot of sorting techniques out there but those which are easy to understand are not efficient whereas those which are efficient are not easy to understand. But one technique falls between this conundrum; Merge sort is a very easy-to-understand and efficient algorithm for sorting.

It is based on divide and conquer algorithm in which a problem is divided into smaller sub-problems using recursion and after solving all these sub-problems all the solutions are combined.

To master merge sort, you need to focus only on the three main things happening:

1.	Divide: Here the array is split into two halves from the midpoint.

2.	Sort: Here we sort the both the sub array ‘s

3.	Combine: Here after sorting we combine both the sub array.


Okay, now that we have caught a gist of this topic, lets dive deeper into the algorithm.

For Simplicity I’ve added a table defining variables:

Abbreviation | Full Form
-------------|------------
arr |	array
l |	Left/starting index of array
m	| Midpoint of the array
r	| Right/last index of array


Merge Sort is a Divide and Conquer algorithm. It divides the input array into two halves, calls itself for the two halves until it reaches the base case of l==r or the size of array is one, and then merges the two sorted halves. The merge() function is used for merging two halves. The merge(arr, l, m, r) is a key process that assumes that arr[l..m] and arr[m+1..r] are sorted and merges the two sorted sub-arrays into one. See the following implementation for details.

```MergeSort(arr[], l,  r)
If r > l
     1. Find the middle point to divide the array into two halves:  
             middle m = l+ (r-l)/2
     2. Call mergeSort for first half:   
             Call mergeSort(arr, l, m)
     3. Call mergeSort for second half:
             Call mergeSort(arr, m+1, r)
     4. Merge the two halves sorted in step 2 and 3:
             Call merge(arr, l, m, r)
```
As an example for better understanding, I’ve added a diagram which shows the whole process.
		 



The Merge Step:
Every recursive algorithm is dependent on a base case and the ability to combine the results from base cases. Merge sort is no different. The most important part of the merge sort algorithm is, you guessed it, merge step.
The merge step is the solution to the simple problem of merging two sorted arrays to build one large sorted array.		

    Have we reached the end of any of the arrays?
     No:
        Compare current elements of both arrays 
        Copy smaller element into sorted array
        Move pointer of element containing smaller element
    Yes:
        Copy all remaining elements of non-empty array
To convert this to code, lets discuss how you should approach the problem.

    •	Create a function which takes the array, left index, mid index, right index as parameters

    •	Create copies of sub arrays, LEFT[l->m], RIGHT[m+1->r]

    •	Create 3 iterators, 2 for arrays LEFT and RIGHT starting from 0, and 1 for main array starting from left because it maintains the current index of the main   array.

    •	Create a while loop until we reach the end of either of the sub arrays, pick the larger element from LEFT or RIGHT and place them in the correct position in main array.

    •	When we run out of element in either LEFT or RIGHT, pick up the remaining element from the sub array which still has elements left and put them in the main array.


Now that we have understood the concept let us look at the coding implementation in C++:

```// C++ program for Merge Sort
#include <stdc++.h>
using namespace std;
 
// Merges two subarrays of arr[].
// First subarray is arr[l..m]
// Second subarray is arr[m+1..r]
void merge(int arr[], int l, int m, int r)
{
    int n1 = m - l + 1;
    int n2 = r - m;
 
    // Create temp arrays
    int L[n1], R[n2];
 
    // Copy data to temp arrays L[] and R[]
    for (int i = 0; i < n1; i++)
        L[i] = arr[l + i];
    for (int j = 0; j < n2; j++)
        R[j] = arr[m + 1 + j];
 
    // Merge the temp arrays back into arr[l..r]
 
    // Initial index of first subarray
    int i = 0;
 
    // Initial index of second subarray
    int j = 0;
 
    // Initial index of merged subarray
    int k = l;
 
    while (i < n1 && j < n2) {
        if (L[i] <= R[j]) {
            arr[k] = L[i];
            i++;
        }
        else {
            arr[k] = R[j];
            j++;
        }
        k++;
    }
 
    // Copy the remaining elements of
    // L[], if there are any
    while (i < n1) {
        arr[k] = L[i];
        i++;
        k++;
    }
 
    // Copy the remaining elements of
    // R[], if there are any
    while (j < n2) {
        arr[k] = R[j];
        j++;
        k++;
    }
}
 
void mergeSort(int arr[],int l,int r){
    if(l>=r){
        return;
    }
    int m =l+ (r-l)/2;
    mergeSort(arr,l,m);
    mergeSort(arr,m+1,r);
    merge(arr,l,m,r);
}
 
// UTILITY FUNCTIONS
// Function to print an array
void printArray(int A[], int size)
{
    for (int i = 0; i < size; i++)
        cout << A[i] << " ";
}
 
// Driver code
int main()
{
    int arr[] = { 12, 11, 13, 5, 6, 7 };
    int arr_size = sizeof(arr) / sizeof(arr[0]);
 
    cout << "Given array is \n";
    printArray(arr, arr_size);
 
    mergeSort(arr, 0, arr_size - 1);
 
    cout << "\nSorted array is \n";
    printArray(arr, arr_size);
    return 0;
}
```

Let’s discuss the efficiency of Merge Sort:
    1.	Time-Complexity: Sorting arrays on different machines. Merge Sort is a recursive algorithm and time complexity can be expressed as following recurrence relation. 
T(n) = 2T(n/2) + θ(n).  The above recurrence can be solved either using the Recurrence Tree method or the Master method. It falls in case II of Master Method and the solution of the recurrence is θ(nLogn). Time complexity of Merge Sort is  θ(nLogn) in all 3 cases (worst, average and best) as merge sort always divides the array into two halves and takes linear time to merge two halves.
    2.	Auxiliary Space: O(n), O(1) with Linked list.

**Conclusion:**

We have understood merge sort, now lets talk about its practical uses:
    •	Better for sorting Linked List
    •	Inversion Count Problem
    •	Used in External sorting

Apart from its great benefits, merge sort also has some drawbacks:
    •	Slower comparative to the other sort algorithms for smaller tasks.
    •	Merge sort algorithm requires additional memory space of 0(n) for the temporary array 
    •	It goes through the whole process even if the  array is sorted.

I hope, now that you’ve understood merge sort you will apply it whenever you think it will be fitting. We all can agree it’s one of the most efficient and easy to understand algorithm.

Thanks for reading!

Happy Coding :smile:
