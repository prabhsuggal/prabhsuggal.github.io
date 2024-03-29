---
layout: post
category: AlgorithmDesignBook
tags: [AlgorithmDesignBook]
title: Algorithm Design Book - Chapter 4[Coding Problems]
---

### LeetCode

### Binary Index Tree/ Fenwick Tree

This is useful for cases when we need to perform two types of operation on an array:
* updating arr[i]
* operation which involves arr[0],..., arr[i] eg: sum(0, a[i]), max(0, a[i])

We can see that in normal case, update step takes O(1) time and 2nd operation takes O(n) time. Using BIT, we can run both these steps at O(log n). Same is the use case for segment trees.

Here we will consider BIT tree where the 2nd operation is sum. First step is the update step. Here is the code(credits:[GOG](https://www.geeksforgeeks.org/binary-indexed-tree-or-fenwick-tree-2/)):
```cpp
// Returns sum of arr[0..index]. This function assumes
// that the array is preprocessed and partial sums of
// array elements are stored in BITree[].
int getSum(int BITree[], int index)
{
    int sum = 0; // Initialize result

    // index in BITree[] is 1 more than the index in arr[]
    index = index + 1;

    // Traverse ancestors of BITree[index]
    while (index>0)
    {
        // Add current element of BITree to sum
        sum += BITree[index];

        // Move index to parent node in getSum View
        // Intuition:
        // index = a1b (where b are all zeros and 1 represents the least set bit)
        // we have -index = 2's complement of index i.e. a'0b' + 1 = a'1b
        //index & (-index) = a1b & a'1b = 010 (least set bit of index)
        // in this step we are removing the last set bit of index in each iteration
        // index & (-index)
        index -= index & (-index);
    }
    return sum;
}

// Updates a node in Binary Index Tree (BITree) at given index
// in BITree. The given value 'val' is added to BITree[i] and
// all of its ancestors in tree.
void updateBIT(int BITree[], int n, int index, int val)
{
    // index in BITree[] is 1 more than the index in arr[]
    index = index + 1;

    // Traverse all ancestors and add 'val'
    while (index <= n)
    {
    // Add 'val' to current node of BI Tree
    BITree[index] += val;

    // Update index to that of parent in update View
    index += index & (-index);
    }
}
```