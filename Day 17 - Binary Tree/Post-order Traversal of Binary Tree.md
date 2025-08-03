
**[145. Binary Tree Post-order Traversal](https://leetcode.com/problems/binary-tree-postorder-traversal/description/)**


Given the `root` of a binary tree, return _the post-order traversal of its nodes' values_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/09/15/inorder_1.jpg)

```
Input: root = [1,null,2,3]
Output: [3,2,1]
```

**Example 2:**

```
Input: root = []
Output: []
```

**Example 3:**

```
Input: root = [1]
Output: [1]
```


**Constraints:**

- The number of nodes in the tree is in the range `[0, 100]`.
- `-100 <= Node.val <= 100`

**Follow up:** Recursive solution is trivial, could you do it iteratively?

***

### Brute Force Approach [Recursive]

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

// Brute Force [Recursive Method]
// Time complexity -> O(n) and Space -> O(n)
class Solution {
private:
    void PostOrder(TreeNode *root, vector<int> &ans)
    {
        if(root!=nullptr)
        {
            PostOrder(root->left,ans);
            PostOrder(root->right,ans);
            ans.push_back(root->val);
        }
    }
public:
    vector<int> postorderTraversal(TreeNode* root) {
        vector<int> ans;
        PostOrder(root,ans);
        return ans;      
    }
};
```

### Optimized Approach [Iterative]

### Complexity

- Time complexity: O(n)
    
- Space complexity: O(n)
    

### Code

```cpp
// Optimized Approach [Iterative Method]
// Time complexity -> O(n) and Space -> O(n)
class Solution {
public:
    vector<int> postorderTraversal(TreeNode* root) {
        vector<int> ans;
        stack <TreeNode *> st1,st2;
        if (root == nullptr) {
            return ans;
        }
        st1.push(root);
        while(!st1.empty())
        {
            root=st1.top();
            st1.pop();
            st2.push(root);

            if(root->left!=nullptr)
            {
                st1.push(root->left);
            }
            if(root->right!=nullptr)
            {
                st1.push(root->right);
            }
        }
        while(!st2.empty())
        {
            root=st2.top();
            st2.pop();
            ans.push_back(root->val);
        }    
        return ans;
    }
};
```


**Important Link**
1. **[Solution Link](https://leetcode.com/problems/binary-tree-postorder-traversal/solutions/4785902/easy-c-solution-2-approach-brute-force-and-optimized-approach)**
