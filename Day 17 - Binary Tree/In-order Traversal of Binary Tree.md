**[94. Binary Tree In-order Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/description/)**

Given the `root` of a binary tree, return *the inorder traversal of its nodes' values*.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/09/15/inorder_1.jpg)

```
Input: root = [1,null,2,3]
Output: [1,3,2]
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

---

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

// Brute Force Approach [Recursive Approach]
//Time complexity -> O(n) and Space -> O(n)
class Solution {
    private:
    void Inorder(TreeNode* root,vector<int> &ans)
    {
        if(root!=NULL)
        {
            Inorder(root->left,ans);
            ans.push_back(root->val);
            Inorder(root->right,ans);
        }
    }
public:
    vector<int> inorderTraversal(TreeNode* root) {

        vector<int> ans;
        Inorder(root, ans);
        return ans;
    }
};
```

### Better Approach [Iterative Approach]

### Complexity

- Time complexity: O(n)
- Space complexity: O(n)

#### Steps

![image.png](https://assets.leetcode.com/users/images/7d3105d2-5085-4ae3-8065-a24d52fa575c_1702118922.9351509.png)

![image.png](https://assets.leetcode.com/users/images/10403830-4f46-4eb9-885c-c57d5750b9e1_1702118939.0800176.png)

![image.png](https://assets.leetcode.com/users/images/2db0e9e1-c00a-4b9c-9103-517ccacdf778_1702118956.7192302.png)

![image.png](https://assets.leetcode.com/users/images/a549836a-a3fe-4eeb-a87c-caabf1d07688_1702118964.770063.png)

![image.png](https://assets.leetcode.com/users/images/fbd9b092-de5c-4f50-a8da-378c6b0969eb_1702118971.018674.png)

![image.png](https://assets.leetcode.com/users/images/5e1736af-47a1-4e9e-9e1a-5279350eea0b_1702118981.054723.png)

![image.png](https://assets.leetcode.com/users/images/5fd462f6-2059-4ccf-9ae8-eab2287e1eec_1702119005.3028944.png)

![image.png](https://assets.leetcode.com/users/images/e0ecdbf0-4ffb-494c-81f7-81cf9e77fbd1_1702119013.7666466.png)

![image.png](https://assets.leetcode.com/users/images/cef4d4de-bc3a-4c67-bb7c-23ba57a85605_1702119026.9231899.png)

![image.png](https://assets.leetcode.com/users/images/8df21537-1d96-4a7e-85d7-126cb9d1974a_1702119036.6274981.png)

![image.png](https://assets.leetcode.com/users/images/4f4d20a5-5856-41e7-9df0-2d0cb7294522_1702119045.2828753.png)

![image.png](https://assets.leetcode.com/users/images/f601285d-0be9-4d95-b270-c02155ac7eb6_1702119054.682994.png)

![image.png](https://assets.leetcode.com/users/images/06d45c25-18cd-4f8e-bae1-a71db4910ec1_1702119063.450512.png)

![image.png](https://assets.leetcode.com/users/images/d63fa647-9934-41a7-bdfc-7b1fc047aaa0_1702119071.3484025.png)

### Code

```cpp
// Optimized Approach [Iterative Approach]
// Time complexity -> O(n) and Space -> O(n)
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {

        vector<int> ans;
        stack <TreeNode* > st;

        while(root!=NULL || !st.empty())
        {
            if(root!=NULL)
            {
                st.push(root);
                root=root->left;
            }
            else
            {
                root=st.top();
                st.pop();
                ans.push_back(root->val);
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

Morris Traversal is a tree traversal algorithm that allows for an in-order traversal of a binary tree without using recursion or a stack. It uses threading to traverse the tree efficiently. The key idea is to establish a temporary link between the current node and its in-order successor

![image.png](https://assets.leetcode.com/users/images/9089b004-bda3-4314-ae3d-c56e1afb83cf_1715012107.2027977.png)

The inorder predecessor of a node is the rightmost node in the left subtree. So when we traverse the left subtree, we encounter a node whose right child is null, this is the last node in that subtree.Hence, we observe a pattern whenever we are at the last node of a subtree such that the right child is pointing to none, we move to the parent of this subtree./p>

![image.png](https://assets.leetcode.com/users/images/b22bef23-4fdc-44d8-a12d-429d7ffbb23f_1715012113.800128.png)

When we are currently at a node, the following cases can arise:

**Case 1: The current node has no left subtree.**

1. Print the value of the current node.
2. Then to the right child of the current node.

![image.png](https://assets.leetcode.com/users/images/854c69ca-8769-4a46-b610-a23010dbc9c8_1715012119.058446.png)

If there is no left subtree, we simply print the value of the current node because there are no nodes to traverse on the left side. After that, we move to the right child to continue the traversal.

**Case 2: There is a left subtree, and the right-most child of this left subtree is pointing to null.**

1. Set the right-most child of the left subtree to point to the current node.
2. Move to the left child of the current node.

![image.png](https://assets.leetcode.com/users/images/3f74c456-7587-4665-a284-ebe83eb8b0f2_1715012126.2745411.png)

In this case, we haven't visited the left subtree yet. We establish a temporary link from the rightmost node of the left subtree to the current node. This link helps us later to identify when we've completed the in-order traversal of the left subtree. After setting the link, we move to the left child to explore the left subtree.

**Case 3: There is a left subtree, and the right-most child of this left subtree is already pointing to the current node.**

1. Print the value of the current node.
2. Revert the temporary link (set it back to null).
3. Move to the right child of the current node.

![image.png](https://assets.leetcode.com/users/images/c3b6c995-dfb4-4cb2-af27-c943ec1a9b95_1715012161.9317102.png)

This case is crucial for maintaining the integrity of the tree structure. If the right-most child of the left subtree is already pointing to the current node, it means we've completed the in-order traversal of the left subtree. We print the value of the current node and then revert the temporary link to restore the original tree structure. Finally, we move to the right child to continue the traversal.

Note: The temporary links added in Case 2 are essential for identifying the completion of the left subtree in Case 3. It's critical to revert these links to avoid altering the original structure of the tree.

#### Algorithm:

**Step 1:** Initialise a current to traverse the tree. Set current to the root of the Binary Tree.

**Step 2:** While the current is not null: If the current node has no left child, print the current node's value and move to the right child ie. set the current to its right child.

![image.png](https://assets.leetcode.com/users/images/67a4cc7b-8b87-4498-a7ca-200e03ffdab7_1715012178.1502812.png)

**Step 3:** If the current node has a left child, we find the in-order predecessor of the current node. This in-order predecessor is the rightmost node in the left subtree or the left subtree's rightmost node.

**If the right child of the in-order predecessor is null:**

1. Set the right child to the current node.
2. Move to the left child (i.e., set current to its left child).

**If the right child of the in-order predecessor is not null:**

1. Revert the changes made in the previous step by setting the right child as null.
2. Print the current node's value.
3. Move to the right child (i.e., set current to its right child).

Repeat steps 2 and 3 until the end of the tree is reached.

![image.png](https://assets.leetcode.com/users/images/3b946260-d98d-4b17-ac61-8a70ac7b1ec8_1715012189.2825584.png)

### Code

```cpp
// Optimized Approach [Morris Traversal]
// Time complexity -> O(n) and Space -> O(1)
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> inorder;
        TreeNode *curr=root;
        while(curr!=nullptr){
            if(curr->left==nullptr){
                inorder.push_back(curr->val);
                curr=curr->right;
            }
            else{
                TreeNode *prev=curr->left;
                while(prev->right!=nullptr && prev->right !=curr){
                    prev=prev->right;
                }
                if(prev->right==nullptr){
                    prev->right=curr;
                    curr=curr->left;
                }
                else{
                    prev->right=nullptr;
                    inorder.push_back(curr->val);
                    curr=curr->right;
                }
            }
        }
        return inorder;
    }
};
```

**Important Link**

1. **[Solution Link](https://youtu.be/80Zug6D1_r4?si=r50k4rbrbJwsHLss)**
