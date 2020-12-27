---
id: fe757956-ec54-49f4-a59c-87a93281efef
title: Chapter 4
desc: ''
updated: 1609062694141
created: 1608634937073
---

# Sorting

## Heap Sort

Constructing a heap takes O(n) time. removing min/max element causes O(log n) which turn to O(nlog n) for n elements. 

**Selection Sort** - we partition the input array into sorted and unsorted regions. To find the smallest item, we performed a linear sweep through the unsorted portion of the array. The smallest item is then swapped with the $$ith$$ item in the array before moving on to the next iteration. Selection sort performs n iterations, where the average iteration takes $$n/2$$ steps, for a total of $$O(n^2)$$ time. 

Heap Sort can be seen as improved version of selection sort. We are just using a better data structure. In selection sort, swap takes $$O(1)$$ time. but getting minimum item takes $$O(n)$$. But we can use a data structure like priority queues/ BST which has $$O(n)$$ search time which reduces time complexity to $$O(nlog n)$$ 

## Merge Sort

The most important thing to remember here is that divide and conquer is your friend. It's always useful. so keep it in mind when going through the problems. you can use it a lot of times. Not just for Sorting.

## Quick Sort

Have read this too many times. But now comes the intuition. One thing which is important is elements less than p are in range [0, firsthigh) so firsthigh is never part of that bunch. So when we swap s[i] and s[firsthigh], we are just swaping s[i](< p) with s[firsthigh](>= p). also we don't include pivot element in the loop because it won't make a change as for i=p, s[i] = s[p].
```c
p = h; /* select last element as pivot */
firsthigh = l;
for (i = l; i < h; i++) {
    if (s[i] < s[p]) {
        swap(&s[i], &s[firsthigh]);
        firsthigh++;
    }
}
swap(&s[p], &s[firsthigh]);
```

### Randomized Algorithms
Quicksort can be improved upon by randomizing the input set. This can still give the worst case but it won't be dependent on the input itself. Such randomization can help us in preventing worst case for a certain input.

## Wiggle Sort
This can be done in O(n) time by doing a single traversal of given array. The idea is based on the fact that if we make sure that all even positioned (at index 0, 2, 4, ..) elements are greater than their adjacent odd elements, we don’t need to worry about odd positioned element. 
```cpp
// This function sorts arr[0..n-1] in wave form, i.e., arr[0] >=  
// arr[1] <= arr[2] >= arr[3] <= arr[4] >= arr[5] .... 
void sortInWave(int arr[], int n) 
{ 
    // Traverse all even elements 
    for (int i = 0; i < n; i+=2) 
    { 
        // If current even element is smaller than previous 
        if (i>0 && arr[i-1] > arr[i] ) 
            swap(&arr[i], &arr[i-1]); 
  
        // If current even element is smaller than next 
        if (i<n-1 && arr[i] < arr[i+1] ) 
            swap(&arr[i], &arr[i + 1]); 
    } 
}
```