

## GFG

**[Root to Leaf Paths](https://www.geeksforgeeks.org/problems/root-to-leaf-paths/1)**

Given a Binary Tree of size N, you need to find all the possible paths from the root node to all the leaf nodes of the binary tree.

**Example 1:**

**Input:**
```
       1
    /     \
   2       3
```

**Output:** 
```
1 2   
1 3
``` 

**Explanation:** 
```
All possible paths:
1->2
1->3
```

**Example 2:**

**Input:**
```
         10
       /    \
      20    30
     /  \
    40   60
```

**Output:** 
```
10 20 40   
10 20 60   
10 30
``` 

**Your Task:**  
Your task is to complete the function **Paths()** which takes the root node as an argument and returns all the possible paths. (All the paths are printed in new lines by the driver's code.)

**Expected Time Complexity:** O(N).  
**Expected Auxiliary Space:** O(H).  
**Note:** H is the height of the tree.

**Constraints:**  
1<=N<=104
***

### Optimized Approach

### Complexity

- Time complexity: O(n)
    
- Space complexity: O(n)
    
where n: number of nodes in a binary tree


#### Algorithm

1. Initialize an empty vector of vectors `result` to store all the paths found in the binary tree.
2. Initialize an empty vector `path` to store the current path being traversed.
3. Call the recursive function `findAllPaths` with the root of the binary tree, `path`, and `result`.
4. In the `findAllPaths` function:
   a. If the current node is `nullptr`, return.
   b. Push the value of the current node onto the `path` vector.
   c. If the current node is a leaf node (i.e., it has no left or right children), push the `path` vector into the `result`.
   d. Recursively call `findAllPaths` for the left and right children of the current node.
   e. Backtrack by popping the last element from the `path` vector.
5. Return the `result` vector containing all the paths found in the binary tree.

This algorithm traverses each node of the binary tree exactly once, so the time complexity is O(n), where 'n' is the number of nodes in the binary tree. Additionally, the space complexity is O(n) because the `path` vector can hold up to 'n' elements in the worst case, and `result` can also store up to 'n' paths.


### Code
```cpp
// Optimized Approach
// Time complexity -> O(n) and Space -> O(n)
// where n: number of nodes in a binary Tree
class Solution {
    void findAllPaths(Node *root, vector<int> &path,vector<vector<int>> &result){
        if(root==nullptr){
            return;
        }
        path.push_back(root->data);
        if(root->left==nullptr && root->right==nullptr){
            result.push_back(path);
        }
        findAllPaths(root->left,path,result);
        findAllPaths(root->right,path,result);
        // Backtrack: remove the current node from the path
        path.pop_back();
    }
  public:
    vector<vector<int>> Paths(Node* root) {
        // code here
        vector<vector<int>> result;
        vector<int> path;
        findAllPaths(root,path,result);
        return result;
    }
};
```


***
***

## Leetcode

**[Binary Tree Paths](https://leetcode.com/problems/binary-tree-paths/)**

Given the `root` of a binary tree, return _all root-to-leaf paths in **any order**_.

A **leaf** is a node with no children.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/03/12/paths-tree.jpg)

```
Input: root = [1,2,3,null,5]
Output: ["1->2->5","1->3"]
```

**Example 2:**

```
Input: root = [1]
Output: ["1"]
```

**Constraints:**

- The number of nodes in the tree is in the range `[1, 100]`.
- `-100 <= Node.val <= 100`

***

### Optimized Approach

### Complexity

- Time complexity: O(nl)
    
- Space complexity: O(n)
    

where n: number of nodes in a binary tree

#### Algorithm

1. Start with an empty vector `ans` to store all the paths found in the binary tree.
2. Check if the given `root` is nullptr.
   - If yes, return an empty vector `ans`.
3. Define a recursive function `findAllPaths` that takes three parameters:
   - `root`: pointer to the current node being traversed.
   - `ans`: reference to the vector of strings to store the paths.
   - `path`: string representing the current path from the root to the current node.
4. In the `findAllPaths` function:
   a. If the current node `root` is `nullptr`, return.
   b. Append the string representation of the value of the current node `root->val` to the `path`.
   c. If the current node is a leaf node (i.e., it has no left or right children), push the `path` string into the `ans`.
   d. Recursively call `findAllPaths` for the left child of the current node, appending "->" to the `path`.
   e. Recursively call `findAllPaths` for the right child of the current node, appending "->" to the `path`.
5. Call the `findAllPaths` function with the root node, `ans`, and an empty string `""`.
6. Return the vector `ans` containing all the paths found in the binary tree.
### Code

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
// Optimized Approach
// Time complexity -> O(n) and Space -> O(n)
// where n: number of nodes in Binary Tree
class Solution {
    void findAllPaths(TreeNode* root, vector<string> &ans, string path){
        if(root==nullptr){
            return;
        }
        path+=to_string(root->val);
        if(root->left==nullptr && root->right==nullptr){
            ans.push_back(path);
        }
        findAllPaths(root->left,ans,path + "->");
        findAllPaths(root->right,ans,path + "->");
    }
public:
    vector<string> binaryTreePaths(TreeNode* root) {
        vector<string> ans;
        if(root==nullptr){
            return ans;
        }
        findAllPaths(root,ans,"");
        return ans;
    }
};
```


***

**Important Link**
1. **[Solution Link](https://leetcode.com/problems/binary-tree-paths/solutions/4958320/optimized-approach-with-explanation-best-c-solution-beats-100-00-of-users-with-c)**