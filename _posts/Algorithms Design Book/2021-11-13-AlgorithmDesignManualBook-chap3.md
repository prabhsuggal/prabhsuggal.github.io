---
layout: post
category: AlgorithmDesignBook
tags: [AlgorithmDesignBook]
title: Algorithm Design Book - Chapter 3
---

### LeetCode

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


* [Construct Binary Tree from Preorder and Inorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)

Two approaches:
   1. **Recursive**:
        Here we keep adding preorder entries into a tree. To differentiate b/w entries which will be in left/right subtree is done on the basis of Inorder vector. Seems $$O(n^2)$$ as we need to find the inorder entry idx for each preorder idx.

```cpp
private:
    TreeNode* build(vector<int> &preorder, vector<int>& inorder, int start, int end, int& idx){
        if(start > end){
            return NULL;
        }

        TreeNode* node = new TreeNode(preorder[idx++]);
        int it = find(inorder.begin()+start, inorder.end(), preorder[idx-1]) - inorder.begin();

        node->left = build(preorder, inorder, start, it-1, idx);
        node->right = build(preorder, inorder, it+1, end, idx);
        return node;
    }

public:
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        int idx=0;
        return build(preorder, inorder, 0, inorder.size()-1, idx);
    }
```

   2. **Stack** :
        This is new for me. $$O(n)$$.
        Here is the initution:

        We know that preorder transversal is as follows:
        * node
        * node->left
        * node->right

        So we always transverse a left node in preorder until there are none left(I hope you got the pun). How do we know that there is no left subtree after a point? **Answer** from Inorder transversal

        The inorder transversal can be shown as follows:
        * node->left
        * node
        * node->right

        so We store the left most node of the tree in the beginning. then the second most and the list goes on.
        so what we can do is:
        1. Make a stack of nodes with the first entry as preorder[0]
        2. Keep assuming that the next entry is a left child until the top of the stack matches the inorder[0]. this means we have reached the left mode node
        3. now pop the stack until we have s.top() == inorder[j] or s.empty().
        4. Once this is done, we can see that the left most node of the remaining tree is part of the right subtree of the node.
        5. So we will assign the next node as right child.
        6. to keep track of the right child we can keep a flag which resets after assigning the next node as right child.

```cpp
public:
TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {

    if(!preorder.size())
        return NULL;

    stack<TreeNode*> st;
    TreeNode* root = new TreeNode(preorder[0]);
    st.push(root);

    int i=1, j=0, flag=0;
    TreeNode* t = root;

    while(i < preorder.size()){
        if(!st.empty() && st.top()->val == inorder[j]){
            t = st.top();
            flag = 1;
            st.pop();
            j++;
        }
        else{
            if(flag){
                flag=0;
                t->right = new TreeNode(preorder[i++]);
                t = t->right;
                st.push(t);
            }
            else{
                t->left = new TreeNode(preorder[i++]);
                t = t->left;
                st.push(t);
            }
        }
    }

    return root;
}
```



