---
layout: post
category: AlgorithmDesignBook
tags: [AlgorithmDesignBook]
title: Algorithm Design Book - Chapter 5
---

* [Leetcode Solutions]({% post_url 2021-11-13-AlgorithmDesignManualBook-chap5-Leetcode %})

### Divide And Conquer

This is one of those things which can come handy during unusual times. Binary search is a well known algorithm which has a lot of power. But sometimes it can be tricky to see all its usecases. I will discuss some of them here.

### Binary Search
```cpp
int binarySearch(int arr[], int l, int r, int x)
{
    while (l <= r) {
        int m = l + (r - l) / 2;
        // Check if x is present at mid
        if (arr[m] == x)
            return m;
        // If x greater, ignore left half
        if (arr[m] < x)
            l = m + 1;
        // If x is smaller, ignore right half
        else
            r = m - 1;
    }

    // if we reach here, then element was
    // not present
    return -1;
}
```

Above algorithm is useful when we have single instance of x in array. Suppose we have multiple instances in the array. In this case, we will be more interested in getting the bounds b/w which the values appear. In that case, we don't need to exit the loop. we can iterate till we reach one of the bounds.
```cpp
/* if x is present in arr[] then returns the index of
FIRST occurrence of x in arr[0..n-1], otherwise
returns -1 */
int first(int arr[], int x, int n)
{
    int low = 0, high = n - 1, res = -1;
    while (low <= high) {
        // Normal Binary Search Logic
        int mid = (low + high) / 2;
        if (arr[mid] > x)
            high = mid - 1;
        else if (arr[mid] < x)
            low = mid + 1;

        // If arr[mid] is same as x, we
        // update res and move to the left
        // half.
        else {
            res = mid;
            high = mid - 1;
        }
    }
    return res;
}

/* if x is present in arr[] then returns the index of
LAST occurrence of x in arr[0..n-1], otherwise
returns -1 */
int last(int arr[], int x, int n)
{
    int low = 0, high = n - 1, res = -1;
    while (low <= high) {
        // Normal Binary Search Logic
        int mid = (low + high) / 2;
        if (arr[mid] > x)
            high = mid - 1;
        else if (arr[mid] < x)
            low = mid + 1;

        // If arr[mid] is same as x, we
        // update res and move to the right
        // half.
        else {
            res = mid;
            low = mid + 1;
        }
    }
    return res;
}
```

### Recurrence Relations

These relations are useful for Divide and conquer. The recurrences are of the form.
$$
T(n) = a · T(n/b) + f(n)
$$
1. If $$f(n) = O(n^{log_b(a - e)})$$ for some constant $$ e > 0$$, then $$T(n) = Θ(n^{log_b a})$$.
2. If $$f(n) = Θ(n^{log_b a})$$, then $$T(n) = Θ(n^{log_b a} lg n)$$.
3. If $$ f(n) = O(n^{log_b a + e})$$ for some constant $$e > 0$$, and if $$ a.f(n/b) [<=] c.f(n)$$ for some $$c [<] 1$$, then $$T(n) = Θ(f(n))$$.

### Fast Convolution

Divide and conquer can be used here as well. We can solve these kind of problems using FFT in O(log n)

### Parallelism

Divide and conquer is used widely because it can enable parallel processing. But It may not be that easy.
