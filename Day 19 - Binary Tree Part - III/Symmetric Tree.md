
**[Symmetric Tree](https://leetcode.com/problems/symmetric-tree/description/)**

Given the `root` of a binary tree, _check whether it is a mirror of itself_ (i.e., symmetric around its center).

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/symtree1.jpg)

```
Input: root = [1,2,2,3,4,4,3]
Output: true
```

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/02/19/symtree2.jpg)

```
Input: root = [1,2,2,null,3,null,3]
Output: false
```

**Constraints:**

- The number of nodes in the tree is in the range `[1, 1000]`.
- `-100 <= Node.val <= 100`

**Follow up:** Could you solve it both recursively and iteratively?


***
### Optimized Approach [Recursive]

### Complexity

- Time complexity: O(n)
    
- Space complexity: O(n)
    

#### Algorithm

The algorithm steps can be summarized as follows::

- We take two variables root1 and root2 initially both pointing to the root.
- Then we use any tree traversal to traverse the nodes. We will simultaneously change root1 and root2 in this traversal function.
- For the base case, if both are pointing to NULL, we return true, whereas if only one points to NULL and other to a node, we return false.
- If both points to a node, we first compare their value, if it is the same we check for the lower levels of the tree.
- We recursively call the function to check the root1’s left child with root2’s right child; then we again recursively check the root1’s right child with root2’s left child.
- When all three conditions ( node values of left and right and two recursive calls) return true, we return true from our function else we return false.

![image.png](https://assets.leetcode.com/users/images/d4c16745-1d2c-435d-817c-1494db108aa4_1710609816.52026.png)

![WhatsApp Image 2024-03-16 at 22.58.06_d2897a6f.jpg](https://assets.leetcode.com/users/images/1ecdab4d-8bf4-4d25-a574-9af995e61e18_1710610109.5602133.jpeg)

![WhatsApp Image 2024-03-16 at 22.58.07_ec01d6df.jpg](https://assets.leetcode.com/users/images/008e46f3-15a0-4d15-b409-fb0b6c72061f_1710610098.2157366.jpeg)

### Code

```rust
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
// Time complexity -> O(n) and Space -> O(n)
class Solution {
    bool isSymmetricHelper(TreeNode* leftTree, TreeNode* rightTree){
        if(leftTree==nullptr || rightTree==nullptr){
            return leftTree==rightTree;
        }
        if(leftTree->val!=rightTree->val){
            return false;
        }
        return isSymmetricHelper(leftTree->left,rightTree->right)
            &&  isSymmetricHelper(leftTree->right,rightTree->left);
    }
public:
    bool isSymmetric(TreeNode* root) {
        return root==nullptr || isSymmetricHelper(root->left,root->right);
    }
};
```


### Optimized Approach [Iterative]

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

// Optimized Approach [Iterative Approach]
// Time complexity -> O(n) and Space -> O(n)
class Solution {
public:
    bool isSymmetric(TreeNode* root) {
        queue<TreeNode*> q;
        q.push(root->left);
        q.push(root->right);
        while(!q.empty()){
            TreeNode *leftNode=q.front();
            q.pop();
            TreeNode *rightNode=q.front();
            q.pop();

            if(leftNode==nullptr && rightNode==nullptr){
                continue;
            }
            if(leftNode==nullptr || rightNode==nullptr){
                return false;
            }
            if(leftNode->val!=rightNode->val){
                return false;
            }
            q.push(leftNode->left);
            q.push(rightNode->right);
            q.push(leftNode->right);
            q.push(rightNode->left);
        }
        return true;
    }
};
```



**Important Link**
1. **[Solution Link](https://leetcode.com/problems/symmetric-tree/solutions/4884765/easy-c-solution-optimized-approach-iterative-and-recursive-with-explanation)**
2. **[Video Link](https://youtu.be/nKggNAiEpBE)**
