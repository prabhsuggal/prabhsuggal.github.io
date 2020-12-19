---
id: 05774b2e-ebf7-4bbc-8171-ad191ba0ae0a
title: Chapter 3
desc: ''
updated: 1608359495587
created: 1598457956604
stub: false
---

# Chapter 3

## LeetCode

* [Count of Smaller Numbers After Self](https://leetcode.com/problems/count-of-smaller-numbers-after-self/)

We have to see how many numbers are smaller to self on the right.


**Naive**:
Just interate for each element and check how many elements are smaller on the right for a given index  - **$$O(n^2)$$**

**Merge Sort** :
Posting an example for more [clarity](https://leetcode.com/problems/count-of-smaller-numbers-after-self/discuss/76607/C++-O(nlogn)-Time-O(n)-Space-MergeSort-Solution-with-Detail-Explanation)

```cpp
void MergeSort(vector<int> &nums, vector<int> &indices, vector<int> &results, int start, int end){
        int count = end-start;
        if(count > 1){
            int mid = start + count/2;
            MergeSort(nums,indices, results, start, mid);
            MergeSort(nums, indices, results, mid, end);
            vector<int> tmp;
            tmp.reserve(count);
            int idx1 = start, idx2 = mid;
            int smallcount=0;
            while(idx1 < mid || idx2 < end){
                if((idx2 == end) || (idx1 < mid &&
                        nums[indices[idx1]] <= nums[indices[idx2]])){
                    tmp.push_back(indices[idx1]);
                    results[indices[idx1]] += smallcount;
                    idx1++;
                }
                else{
                    tmp.push_back(indices[idx2++]);
                    smallcount++;
                }
            }
            move(tmp.begin(), tmp.end(), indices.begin()+start);
        }
    }
```