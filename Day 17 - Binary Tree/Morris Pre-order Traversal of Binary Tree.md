
**[144. Binary Tree Preorder Traversal](https://leetcode.com/problems/binary-tree-preorder-traversal/description/)**

Given the `root` of a binary tree, return _the preorder traversal of its nodes' values_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/09/15/inorder_1.jpg)

```
Input: root = [1,null,2,3]
Output: [1,2,3]
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

### Brute Force Approach [Recursive Approach]

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

// Brute Fore Approach [Recursive Approach]
// Time complexity -> O(n) and Space -> O(n)
class Solution {
private:
    void preorder(TreeNode* root,vector<int> &ans)
    {
        if(root==NULL)
        {
            return;
        }
        ans.push_back(root->val);
        preorder(root->left,ans);
        preorder(root->right,ans);
    }
public:
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> ans;
        preorder(root,ans);
        return ans;
    }
};
```

### Better Approach [Iterative Approach]

### Complexity

- Time complexity: O(n)
    
- Space complexity: O(n)
    

### Code

```cpp
// Optimized Approach [Iterative Approach]
// Time complexity -> O(n) and Space -> O(n)
class Solution {
public:
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> ans;
        stack<TreeNode*> st;
        while(root!=NULL || !st.empty())
        {
            if(root!=NULL)
            {
                ans.push_back(root->val);
                st.push(root);
                root=root->left;
            }
            else
            {
                root=st.top();
                st.pop();
                root=root->right;
            }
        }
        return ans;
    }
};
```

### Optimized Approach [Morris Traversal]

### Complexity

- Time complexity: O(n)
    
- Space complexity: O(1)
    

#### Explanation:

A prerequisite to this problem is Morris Inorder Traversal of Binary Tree. We extend Morris Inorder Traversal to Preorder Morris Traversal and modify the algorithm to print the current node’s value before moving to the left child when the right child of the inorder predecessor is null.

This change ensures that the nodes are processed in the desired order for Preorder Traversal. The basic structure of Morris Traversal remains intact, but the printing step is adjusted, resulting in a Preorder Traversal that is still in-place and has a constant space complexity.

![image.png](https://assets.leetcode.com/users/images/e822b76a-3db7-44ef-a915-da3bc41f2d71_1715011149.80447.png)

In Morris Inorder Traversal, we are traversing the tree in the way: Left, Root, Right. In Morris Preorder traversal we want to traverse the tree in the way: Root, Left, Right. Therefore, the following code changes are required:

**When the current node has a left child:**

In Morris Inorder Traversal, a new thread is created by establishing a temporary link between the current node and its in-order predecessor. In Morris Preorder Traversal, we want to print the root before visiting the left child. Therefore, after setting the thread (establishing the link), we print the current node's value before moving it to its left child.

image.png  
![image.png](https://assets.leetcode.com/users/images/2efd6394-29a8-433b-a8d5-87d3beb3e0ca_1715011161.8936114.png)

**When the current node has no left child:**

This case remains unchanged from Morris Inorder Traversal. If the current node has no left child, there is nothing to visit on the left side. In both Inorder and Preorder traversals, we want to print the current node's value and move to the right child. Therefore, there is no code modification needed for this scenario.

![image.png](https://assets.leetcode.com/users/images/3aeee012-cc8d-41f4-930a-83541d7c4c14_1715011168.1622467.png)

#### Algorithm:

**Step 1:**Initialise a current to traverse the tree. Set current to the root of the Binary Tree.

**Step 2:** While the current is not null: If the current node has no left child, print the current node's value and move to the right child ie. set current to its right child.

![image.png](https://assets.leetcode.com/users/images/8a020f4e-624b-485e-89c3-0c1d249dcc55_1715011181.8730679.png)

**Step 3:** If the current node has a left child, we find the in-order predecessor of the current node. This in-order predecessor is the rightmost node in the left subtree or the left subtree's rightmost node.

**If the right child of the in-order predecessor is null:**

1. Set the right child to the current node.
2. Print the value of the current node as preorder traverses the tree in the inorder: Root, Left then Right.
3. Move to the left child (i.e., set current to its left child).

**If the right child of the in-order predecessor is not null:**

1. Revert the changes made in the previous step by setting the right child as null.
2. Move to the right child (i.e., set current to its right child).

Repeat steps 2 and 3 until the end of the tree is reached.

![image.png](https://assets.leetcode.com/users/images/1d18fbf6-3e25-493f-8c2d-62f80556d787_1715011193.873259.png)

### Code

```cpp
// Optimized Approach 
// Time complexity -> O(n) and Space -> O(1)
class Solution {
public:
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> preorder;
        TreeNode *curr=root;
        while(curr!=nullptr){
            if(curr->left==nullptr){
                preorder.push_back(curr->val);
                curr=curr->right;
            }
            else{
                TreeNode *prev=curr->left;
                while(prev->right!=nullptr && prev->right !=curr){
                    prev=prev->right;
                }
                if(prev->right==nullptr){
                    prev->right=curr;
                    preorder.push_back(curr->val);
                    curr=curr->left;
                }
                else{
                    prev->right=nullptr;
                    curr=curr->right;
                }
            }
        }
        return preorder;
    }
};
```


**Take Reference for Detail Solution:** [Binary Tree In-order Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/solutions/4381728/3-approach-best-c-solution-brute-force-better-and-optimized-approach)

**Important Link**
1. **[Solution Link](https://leetcode.com/problems/binary-tree-preorder-traversal/solutions/4609371/3-approach-best-c-solution-brute-force-better-and-optimized-approach)**
2. **[Video Link](https://youtu.be/80Zug6D1_r4?si=r50k4rbrbJwsHLss)**