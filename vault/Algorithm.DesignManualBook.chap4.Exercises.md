---
id: 6b9c2b74-68aa-468e-a8fb-44925c159f75
title: Exercises
desc: ''
updated: 1609062959723
created: 1608733098626
---

# Exercises

* **4.4** - Counting sort

* **4-11** Design an O(n) algorithm that, given a list of n elements, finds all the elements that appear more than n/2 times in the list. Then, design an O(n) algorithm that, given a list of n elements, finds all the elements that appear more than $$n/4$$ times.
We can get the solution using something similar to tetris Game. Credits: [GoG](https://www.geeksforgeeks.org/given-an-array-of-of-size-n-finds-all-the-elements-that-appear-more-than-nk-times/).  we can solve for any n/k in O(nk) time. Here is the intuition:
  * create a temp array of size k-1
  * iterate over the elements of the array. For each element add it into temp array and increment its count
  * when the temp array is filled and a new element comes, delete the count of each entry in the temp array and ignore the element.
  * follow the above steps till the end.
  * now user needs to verify for each element y in temp,  iterating over the array. to make sure each element occurs more than n/k times.


```cpp
void moreThanNdK(int arr[], int n, int k)
{
    // k must be greater than
    // 1 to get some output
    if (k < 2)
        return;
 
    /* Step 1: Create a temporary
       array (contains element
       and count) of size k-1. 
       Initialize count of all
       elements as 0 */
    struct eleCount temp[k - 1];
    for (int i = 0; i < k - 1; i++)
        temp[i].c = 0;
 
    /* Step 2: Process all 
      elements of input array */
    for (int i = 0; i < n; i++) 
    {
        int j;
 
        /* If arr[i] is already present in
           the element count array, 
           then increment its count
         */
        for (j = 0; j < k - 1; j++) 
        {
            if (temp[j].e == arr[i]) 
            {
                temp[j].c += 1;
                break;
            }
        }
 
        /* If arr[i] is not present in temp[] */
        if (j == k - 1) {
            int l;
 
            /* If there is position available 
              in temp[], then place arr[i] in 
              the first available position and 
              set count as 1*/
            for (l = 0; l < k - 1; l++)
            {
                if (temp[l].c == 0) 
                {
                    temp[l].e = arr[i];
                    temp[l].c = 1;
                    break;
                }
            }
 
            /* If all the position in the 
               temp[] are filled, then decrease 
               count of every element by 1 */
            if (l == k - 1)
                for (l = 0; l < k; l++)
                    temp[l].c -= 1;
        }
```