
**[Height of the Binary Tree or Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/description/)**


Given the `root` of a binary tree, return _its maximum depth_.

A binary tree's **maximum depth** is the number of nodes along the longest path from the root node down to the farthest leaf node.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/26/tmp-tree.jpg)

```
Input: root = [3,9,20,null,null,15,7]
Output: 3
```

**Example 2:**

```
Input: root = [1,null,2]
Output: 2
```

**Constraints:**

- The number of nodes in the tree is in the range `[0, 104]`.
- `-100 <= Node.val <= 100`

***

### Optimized Approach

### Complexity

- Time complexity: O(n)
    
- Space complexity: O(n)
    

### Code

```cpp
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
// Time Complexity -> O(n) and Space -> O(n)
// where n: the number of nodes in the binary tree.
class Solution {
private:
    int countHeight(TreeNode* root)
    {
        int x=0,y=0;
        if(root!=nullptr)
        {
            x=countHeight(root->left);
            y=countHeight(root->right);
            if(x>y)
            {
                return x+1;
            }
            else
            {
                return y+1;
            }
        }
        return 0;
    }
public:
    int maxDepth(TreeNode* root) {
        return countHeight(root);
    }
};
```

#### OR

#### Approach

- We start to travel recursively and do our work in Post Order.
-  Reason behind using Post Order comes from our intuition , that if we know the result of  left and right child then we can calculate the result using that. 
- This is exactly an indication of PostOrder, because in PostOrder we already calculated results for left and right children than we do it for current node.
- So for every node post order, we do Max( left result , right result ) + 1 and return it to the previous call.
- Base Case is when root == null so we need to return 0;

##### Explanation

#### Dry Run

In Post Order, we start to travel on the example given in the below diagram

![image.png](https://assets.leetcode.com/users/images/628216e3-4028-45b0-a2be-f122ec0fdcd8_1709827471.207229.png)

- Reach on **Node 10** , Left child = null so 0 , Right child = null so 0 & add 1 for node 10 so max depth till node 10 is max(0,0) + 1 = 1. 
- Reach on **Node 2** , Left child = null so 0 , Right child = will give 1 & add 1 for node 2 so max depth till node 2 is max(0,1) + 1 = 2.
- Reach on **Node 8** , Left child = null so 0 , Right child = null so 0 & add 1 for node 8 so max depth till node 8 is max(0,0) + 1 = 1.
- Reach on **Node 11** , Left child = null so 0 , Right child = null so 0 & add 1 for node 11 so max depth till node 11 is max(0,0) + 1 = 1.
- Reach on **Node 3** , Left child will give 1 , Right child = will give 1 & add 1 for node 3 so max depth till node 3 is max(1,1) + 1 = 2.
- Reach on **Node 4** , Left child = null so 0 , Right child = null so 0 & add 1 for node 4 so max depth till node 4 is max(0,0) + 1 = 1.
- Reach on **Node 5** , Left child will give 2 , Right child = will give 1 & add 1 for node 5 so max depth till node 5 is max(2,1) + 1 = 3.
- Reach on **Node 12** , Left child will give 2 , Right child = will give 3 & add 1 for node 12 so max depth till node 12 is max(2,3) + 1 = 4.
- Hence 4 is our final ans.

### Code

```cpp
class Solution {
public:
    int maxDepth(TreeNode* root) {
        if(root==nullptr)
        {
            return 0;
        }
        int lh=maxDepth(root->left);
        int rh=maxDepth(root->right);

        return 1+max(lh,rh);
    }
};
```

***

**Important Link**
1. **[Solution Link](https://leetcode.com/problems/maximum-depth-of-binary-tree/solutions/4838389/best-c-solution-optimized-approach-dry-run-detailed-explanation)**
2. **[Video Link](https://youtu.be/eD3tmO66aBA)**