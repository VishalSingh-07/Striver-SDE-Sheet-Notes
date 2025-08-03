
**[114. Flatten Binary Tree to Linked List](https://leetcode.com/problems/flatten-binary-tree-to-linked-list/)**

Given the `root` of a binary tree, flatten the tree into a "linked list":

- The "linked list" should use the same `TreeNode` class where the `right` child pointer points to the next node in the list and the `left` child pointer is always `null`.
- The "linked list" should be in the same order as a [**pre-order** **traversal**](https://en.wikipedia.org/wiki/Tree_traversal#Pre-order,_NLR) of the binary tree.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/01/14/flaten.jpg)

```
Input: root = [1,2,5,3,4,null,6]
Output: [1,null,2,null,3,null,4,null,5,null,6]
```

**Example 2:**

```
Input: root = []
Output: []
```

**Example 3:**

```
Input: root = [0]
Output: [0]
```

**Constraints:**

- The number of nodes in the tree is in the range `[0, 2000]`.
- `-100 <= Node.val <= 100`

**Follow up:** Can you flatten the tree in-place (with `O(1)` extra space)?

***
### Note: 

- The sequence of nodes in the linked list should be the same as that of the **preorder traversal** of the binary tree.
- The linked list nodes are the same binary tree nodes. You are not allowed to create extra nodes.
- The right child of a node points to the next node of the linked list whereas the left child points to NULL.

**Example:**

![image.png](https://assets.leetcode.com/users/images/a6d51094-be06-45ea-a02a-84303228dcb6_1716135807.2583532.png)

---

### Brute Force Approach

### Complexity

- Time complexity: O(n)
    
- Space complexity: O(n)
    

#### Algorithm:

1. Define a preorder traversal function (`preorder`) that recursively traverses the binary tree and stores the values in a vector.
2. In the `flatten` function:
    - Check if the root is `nullptr`. If so, return.
    - Initialize an empty vector `arr` to store the preorder traversal.
    - Call the `preorder` function to populate the `arr` vector.
    - Initialize a pointer `current` to the root of the tree.
    - Iterate through the `arr` vector starting from index 1 (since the root value is already processed):
        - Set the left child of `current` to `nullptr`.
        - Set the right child of `current` to a new `TreeNode` with the value from the `arr` vector.
        - Update `current` to point to its right child.

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

// Brute Force Approach
// Time complexity -> O(n) and Space -> O(n)
class Solution {
    void preorder(TreeNode* root, vector<int> &arr) {
        if (root != nullptr) {
            arr.push_back(root->val);
            preorder(root->left, arr);
            preorder(root->right, arr);
        }
    }
public:
    void flatten(TreeNode* root) {
        if (root == nullptr) {
            return;
        }
        vector<int> arr;
        preorder(root, arr);
        
        TreeNode* current = root;
        for (int i = 1; i < arr.size(); ++i) {
            current->left = nullptr;
            current->right = new TreeNode(arr[i]);
            current = current->right;
        }
    }
};
```

### Recursive Approach [Recursion]

### Complexity

- Time complexity: O(n)
    
- Space complexity: O(n)
    

#### Algorithm:

The algorithm steps can be stated as: 

- If we observe, we are moving in a **reverse postorder** way : i.e  **right, left, root.** 
- We take a reference variable (say prev) to store the previous node( initialized to NULL).
- Whenever we visit a node, we set the right child to the prev and left child to NULL. 
- Next we assign this current node to prev.
- We perform the above two operations on all the nodes in the traversal.

#### Dry run:

The following illustrations will give a clear idea.

![image.png](https://assets.leetcode.com/users/images/50351ebb-864e-4fe4-950c-59efc0571f50_1716135900.9621422.png)

![image.png](https://assets.leetcode.com/users/images/a3686429-d452-41a9-b8de-3f883981fe62_1716135910.4717064.png)

![image.png](https://assets.leetcode.com/users/images/0099ee74-f6af-4074-a41a-8a48df87b6a8_1716135914.8829556.png)

![image.png](https://assets.leetcode.com/users/images/ed315f05-7423-4a8b-8118-e5485fae762a_1716135919.3364415.png)

![WhatsApp Image 2024-05-19 at 22.00.03_cc5c2944.jpg](https://assets.leetcode.com/users/images/27aac397-60aa-46e2-b925-20a2603ba907_1716136322.0098388.jpeg)

![WhatsApp Image 2024-05-19 at 22.00.03_f97677dc.jpg](https://assets.leetcode.com/users/images/599748cf-714a-4825-a30b-301720ef55be_1716136360.6509328.jpeg)

![WhatsApp Image 2024-05-19 at 22.00.04_3c6c5e72.jpg](https://assets.leetcode.com/users/images/dd4c68d6-eba6-4ea8-9321-7b3e2acbb5e2_1716136340.6479561.jpeg)

### Code

```cpp
// Recursive Approach [Recursion]
// Time complexity -> O(n) and Space -> O(n)
class Solution {
public:
    TreeNode* prev=nullptr;
    void flatten(TreeNode* root) {
        if (root == nullptr) {
            return;
        }
        flatten(root->right);
        flatten(root->left);

        root->right=prev;
        root->left=nullptr;
        prev=root;
    }
};
```

### Iterative Approach [Using Stack]

### Complexity

- Time complexity: O(n)
    
- Space complexity: O(n)
    

#### Algorithm:

The algorithm approach can be stated as:

- Take a stack and push the root node to it.
- Set a while loop till the stack is non-empty.
- In every iteration, take the node at the top of the stack( say cur) and pop the stack.
- If cur has a right child, push it to the stack.
- If cur has a left child, push it to the stack.
- Set the right child of cur to node at stack’s top.
- Set the left child of cur as NULL.

#### Dry Run:

![image.png](https://assets.leetcode.com/users/images/0524c75b-3317-400a-a002-0999c8c3cc4e_1716135970.0090675.png)

![image.png](https://assets.leetcode.com/users/images/a70254b5-a3a8-40ee-9b5d-a17aa0ddb853_1716135974.031349.png)

![WhatsApp Image 2024-05-19 at 22.00.05_13873ec7.jpg](https://assets.leetcode.com/users/images/d3ad6ae4-3e1a-4d08-9935-d67876ed2017_1716136391.7679403.jpeg)

![WhatsApp Image 2024-05-19 at 22.00.05_42b6c1d5.jpg](https://assets.leetcode.com/users/images/7542aab3-0dcd-407b-972f-b7ca717d792e_1716136406.8506908.jpeg)

### Code

```cpp
//  Iterative Approach [using Stack]
// Time complexity -> O(n) and Space -> O(n)
class Solution {
public:
    TreeNode* prev=nullptr;
    void flatten(TreeNode* root) {
        if (root == nullptr) {
            return;
        }
        stack<TreeNode*> st;
        st.push(root);
        while(!st.empty()){
            TreeNode *curr=st.top();
            st.pop();
            if(curr->right!=nullptr){
                st.push(curr->right);
            }
            if(curr->left!=nullptr){
                st.push(curr->left);
            }
            if(!st.empty()){
                curr->right=st.top();
            }
            curr->left=nullptr;
        }
    }
};
```

### Optimized Approach [Morris Preorder Traversal]

### Complexity

- Time complexity: O(n)
    
- Space complexity: O(1)
    

#### Algorithm:

The algorithm can be described as:

- At a node(say cur) if there exists a left child, we will find the rightmost node in the left subtree(say prev).
- We will set prev’s right child to cur’s right child,
- We will then set cur’s right child to it’s left child.
- We will then move cur to the next node by assigning cur it to its right child
- We will stop the execution when cur points to NULL.

#### Dry Run:

![image.png](https://assets.leetcode.com/users/images/e42a1dec-d96f-466b-9059-857d3de5d4cf_1716136050.747643.png)

![image.png](https://assets.leetcode.com/users/images/1599605f-56c8-4911-a136-7346f3a90209_1716136055.918787.png)

![WhatsApp Image 2024-05-19 at 22.00.04_27fd360a.jpg](https://assets.leetcode.com/users/images/7f91e4e8-676d-4356-ad84-1e09bd0d6137_1716136432.0002177.jpeg)

![WhatsApp Image 2024-05-19 at 22.00.05_9ac499da.jpg](https://assets.leetcode.com/users/images/f03ee508-64d5-4b85-a78d-a7ce77065279_1716136447.0011916.jpeg)

![WhatsApp Image 2024-05-19 at 22.00.02_fdcf3b2c.jpg](https://assets.leetcode.com/users/images/7c6bdabf-7c9f-4841-8cd9-87e00cf0d228_1716136479.093157.jpeg)

![WhatsApp Image 2024-05-19 at 22.00.03_908bad03.jpg](https://assets.leetcode.com/users/images/6a54685c-2403-4d15-b680-8679281234bf_1716136491.2894964.jpeg)

### Code

```cpp
// Optimized Approach [Morris Preorder Traversal]
// Time complexity -> O(n) and Space -> O(1)
class Solution {
public:
    void flatten(TreeNode* root) {
        if (root == nullptr) {
            return;
        }
        TreeNode *curr=root;
        while(curr!=nullptr){
            if(curr->left!=nullptr){
                TreeNode *prev=curr->left;
                while(prev->right!=nullptr){
                    prev=prev->right;
                }
                prev->right=curr->right;
                curr->right=curr->left;
                curr->left=nullptr;
            }
            curr=curr->right;
        }
    }
};
```


**Important Link **
1. **[Video Link](https://youtu.be/sWf7k1x9XR4?si=ghp8OzBBGlbZN7w3)**
2. **[Solution Link](https://leetcode.com/problems/flatten-binary-tree-to-linked-list/solutions/5180333/4-approach-best-c-solution-brute-force-recursion-iterative-optimized-approach)**
3. **[Detailed Solution](https://takeuforward.org/data-structure/flatten-binary-tree-to-linked-list/)**