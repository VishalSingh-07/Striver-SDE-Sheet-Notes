
**[Boundary Traversal of binary tree](https://www.geeksforgeeks.org/problems/boundary-traversal-of-binary-tree/1)**


Given a Binary Tree, find its Boundary Traversal. The traversal should be in the following order: 

1. **Left boundary nodes:** defined as the path from the root to the left-most node ie- the leaf node you could reach when you always travel preferring the left subtree over the right subtree. 
2. **Leaf nodes:** All the leaf nodes except for the ones that are part of left or right boundary.
3. **Reverse right boundary nodes:** defined as the path from the right-most node to the root. The right-most node is the leaf node you could reach when you always travel preferring the right subtree over the left subtree. Exclude the root from this as it was already included in the traversal of left boundary nodes.

**Note:** If the root doesn't have a left subtree or right subtree, then the root itself is the left or right boundary.   
  
**Example 1:**

**Input:**
```
        1 
      /   \
     2     3  
    / \   / \ 
   4   5 6   7
      / \
     8   9
```
   
**Output:** 1 2 4 8 9 6 7 3

**Explanation:**
**![](https://media.geeksforgeeks.org/wp-content/uploads/20211103204119/graph4-300x300.png)**

**Example 2:**

**Input:**
```
            1
           /
          2
        /  \
       4    9
     /  \    \
    6    5    3
             /  \
            7     8
```
**Output:** 1 2 4 6 5 7 8

**Explanation:**
[![](https://media.geeksforgeeks.org/wp-content/uploads/20211103204646/graph1-300x300.png)](https://contribute.geeksforgeeks.org/wp-content/uploads/boundary.png)

As you can see we have not taken the right subtree. 

**Your Task:**  
This is a function problem. You don't have to take input. Just complete the **function boundary()** that takes the root node as input and returns an array containing the boundary values in anti-clockwise.

**Expected Time Complexity:** O(N).   
**Expected Auxiliary Space:** O(Height of the Tree).

**Constraints:**  
1 ≤ Number of nodes ≤ 105  
1 ≤ Data of a node ≤ 105

*** 

### Optimized Approach

### Complexity

- Time complexity: O(n)
    
- Space complexity: O(n)
    
where n is the number of nodes in the binary tree.


**Approach:** Boundary traversal in an anti-clockwise direction can be described as a traversal consisting of three parts:

1. **Part 1:** Left Boundary of the tree (excluding the leaf nodes).
2. **Part 2:** All the leaf nodes travelled in the left to right direction.
3. **Part 3:** Right Boundary of the tree (excluding the leaf nodes), traversed in the reverse direction.

We take a simple data structure like a vector/Arraylist to store the Boundary Traversal. The root node is coming from both the boundaries (left and right). Therefore, to avoid any confusion, we push it on our list at the very start.

![image](../Screenshots/Boundary%20Traversal%20of%20Binary%20Tree_1.png);



We will now see the approach to finding these three parts.

**Part 1:**  Left Boundary

![image](../Screenshots/Boundary%20Traversal%20of%20Binary%20Tree_2.png);

To traverse the left boundary, we can set a simple iteration. Initially, we make the cur pointer point to the root’s left. In every iteration, if the cur node is not a leaf node, we print it. Then we always try to move left of the cur pointer. If there is no left child, then we move to the right of cur and in the next iteration, again try to move to the left first. We stop our execution when cur is pointing to NULL. 

![image](../Screenshots/Boundary%20Traversal%20of%20Binary%20Tree_3.png);

**Part 2:** Leaf nodes

![image](../Screenshots/Boundary%20Traversal%20of%20Binary%20Tree_4.png);

To print the leaf nodes, we can do a simple preorder traversal, and check if the current node is a leaf node or not. If it is a leaf node just print it.

Please note that we want the leaves to come in a specific order which is bottom-left to top-right, therefore a level order traversal will not work because it will print the upper-level leaves first. Therefore, we use a preorder traversal.

![image](../Screenshots/Boundary%20Traversal%20of%20Binary%20Tree_5.png);

**Part 3:** Right Boundary

![image](../Screenshots/Boundary%20Traversal%20of%20Binary%20Tree_6.png);

We need to print the right boundary in the **Reverse** direction. It is very similar to the left boundary traversal. We initialize our cur pointer to the right child of the root node and set an iterative loop. To achieve the reverse direction, we take an auxiliary list. In every iteration, we check if the current node is not a leaf node then we push it to the auxiliary list. Then we first try to move right of cur, if there is no right child only then we move left. We stop our execution once cur points to NULL.

Now the auxiliary list contains the nodes of the right boundary. We iterate from the end to start off this list and in every iteration, push the value to our main boundary traversal list. This way we get the nodes in the reverse direction.

![image](../Screenshots/Boundary%20Traversal%20of%20Binary%20Tree_6.png);



![image](../Screenshots/Boundary%20Traversal%20of%20Binary%20Tree_7.png);

### Code

```cpp

// } Driver Code Ends
/* A binary tree Node
struct Node
{
    int data;
    Node* left, * right;
}; */

// Optimized Approach
// Time complexity -> O(n) and Space -> O(n)
// where n: number of nodes in a binary tree
class Solution {
    
    // Helper function to check if a given node is a leaf node
    bool isLeafNode(Node* root) {
        if (root->left == nullptr && root->right == nullptr) {
            return true;
        }
        return false;
    }

    // Helper function to add the left boundary nodes to the answer vector
    void addLeftBoundary(Node* root, vector<int>& ans) {
        Node* curr = root->left;
        while (curr != nullptr) {
            // Add non-leaf nodes to the answer vector
            if (!isLeafNode(curr)) {
                ans.push_back(curr->data);
            }
            // Traverse to the left child if it exists
            if (curr->left != nullptr) {
                curr = curr->left;
            } else {
                // Otherwise, go to the right child
                curr = curr->right;
            }
        }
    }

    // Helper function to add the leaf nodes to the answer vector
    void addLeafNodes(Node* root, vector<int>& ans) {
        if (isLeafNode(root)) {
            // If the current node is a leaf, add it to the answer vector
            ans.push_back(root->data);
            return;
        }
        // Recursively traverse left subtree
        if (root->left != nullptr) {
            addLeafNodes(root->left, ans);
        }
        // Recursively traverse right subtree
        if (root->right != nullptr) {
            addLeafNodes(root->right, ans);
        }
    }

    // Helper function to add the right boundary nodes to the answer vector
    void addRightBoundary(Node* root, vector<int>& ans) {
        Node* curr = root->right;
        vector<int> temp;
        while (curr != nullptr) {
            // Add non-leaf nodes to the temporary vector
            if (!isLeafNode(curr)) {
                temp.push_back(curr->data);
            }
            // Traverse to the right child if it exists
            if (curr->right != nullptr) {
                curr = curr->right;
            } else {
                // Otherwise, go to the left child
                curr = curr->left;
            }
        }
        // Add the elements from the temporary vector to the answer vector in reverse order
        for (int i = temp.size() - 1; i >= 0; i--) {
            ans.push_back(temp[i]);
        }
    }

public:
    // Main function to return the boundary nodes of a binary tree
    vector<int> boundary(Node* root) {
        // Initialize the answer vector
        vector<int> ans;
        
        // If the tree is empty, return empty vector
        if (root == nullptr) {
            return ans;
        }
        
        // Add the root node if it's not a leaf node
        if (!isLeafNode(root)) {
            ans.push_back(root->data);
        }
        // Add the left boundary nodes
        addLeftBoundary(root, ans);
        
        // Add the leaf nodes
        addLeafNodes(root, ans);
        
        // Add the right boundary nodes
        addRightBoundary(root, ans);
        
        return ans;
    }
};

```


****

**Important Link**
1.  **[Video Link](https://youtu.be/0ca1nvR0be4)**

