
**[Same Tree or (Check if two trees are identical or not)](https://leetcode.com/problems/same-tree/description/)**

Given the roots of two binary trees `p` and `q`, write a function to check if they are the same or not.

Two binary trees are considered the same if they are structurally identical, and the nodes have the same value.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/12/20/ex1.jpg)

```
Input: p = [1,2,3], q = [1,2,3]
Output: true
```

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/12/20/ex2.jpg)

```
Input: p = [1,2], q = [1,null,2]
Output: false
```

**Example 3:**

![](https://assets.leetcode.com/uploads/2020/12/20/ex3.jpg)

```
Input: p = [1,2,1], q = [1,1,2]
Output: false
```

**Constraints:**

- The number of nodes in both trees is in the range `[0, 100]`.
- `-104 <= Node.val <= 104`

***
### Optimized Approach

### Complexity

- Time complexity: O(n)
    
- Space complexity: O(h)
    

Where **n:** number of nodes in the tree and **h:** height of the tree

##### Algorithm

1. **Base Case:**
    - If both trees are empty (`nullptr`), return true.
2. **Node Comparison:**
    - If values of current nodes are equal, recursively compare left and right subtrees.
3. **Return Result:**
    - Return true only if base case is met or if values are equal and recursive comparisons are true; otherwise, return false.

### Code

```kotlin
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
 
// Optimized Approach
// Time Complexity -> O(n) and Space -> O(h)
// Where n: number of nodes in the tree and h: height of the tree
class Solution {
public:
    bool isSameTree(TreeNode* p, TreeNode* q) {
        // Base Case
        if(!p && !q)
        {
            return true;
        }
        if(p!=nullptr && q!=nullptr && p->val==q->val)
        {
            return (isSameTree(p->left,q->left) && isSameTree(p->right,q->right));
        }
        return false;
    }
};
```

### OR

```kotlin
class Solution {
public:
    bool isSameTree(TreeNode* p, TreeNode* q) {
        if(p==nullptr || q==nullptr){
            return (p==q);
        }
        return (p->val==q->val) 
                && isSameTree(p->left,q->left) 
                && isSameTree(p->right,q->right);
    }
};
```


**Important Link**
1. **[Solution Link](https://leetcode.com/problems/same-tree/solutions/4783870/best-c-solution-optimized-approach-beats-100-00-of-users-with-c-with-explanation)**
2. **[Video Link](https://youtu.be/BhuvF_-PWS0)** 