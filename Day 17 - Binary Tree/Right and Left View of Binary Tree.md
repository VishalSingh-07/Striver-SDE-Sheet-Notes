
**[Right View of Binary Tree](https://leetcode.com/problems/binary-tree-right-side-view/description/)**

Given the `root` of a binary tree, imagine yourself standing on the **right side** of it, return _the values of the nodes you can see ordered from top to bottom_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/14/tree.jpg)

```
Input: root = [1,2,3,null,5,null,4]
Output: [1,3,4]
```

**Example 2:**

```
Input: root = [1,null,3]
Output: [1,3]
```

**Example 3:**

```
Input: root = []
Output: []
```

**Constraints:**

- The number of nodes in the tree is in the range `[0, 100]`.
- `-100 <= Node.val <= 100`


***
## Right Side View of Binary Tree

### Optimized Approach

### Complexity

- Time complexity: O(n)
    
- Space complexity: O(h)
    

where **h** : the height of the binary tree and **n** : the number of nodes in the binary tree.

##### Approach

- Create an vector data structure inside the right side view function
- Call for the recursive_right function with the (root,level,vector). Here level will be initially passed as 0.
- Return the vector.
- Now in the recursive_right function
    - If vector size is equal to the level then push_back its node value to the vector data structure.
    - Otherwise call recursive_right for (node->right,level+1,vector)
    - Call recursive_right for (node->left,level+1,vector)

![WhatsApp Image 2024-03-07 at 22.31.58_d332f3c4.jpg](https://assets.leetcode.com/users/images/3bb94fd3-989d-4404-82b7-5fe52edfc91f_1709830975.818786.jpeg)

![WhatsApp Image 2024-03-07 at 22.31.58_200024c7.jpg](https://assets.leetcode.com/users/images/c8b4393b-303a-48aa-8a93-94e39ab0dc01_1709830964.7485032.jpeg)

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
// Time Complexity: O(n) and Space Complexity: O(h)
// where h : the height of the binary tree and n : the number of nodes in the binary tree.
class Solution {
private:
    void rightView(TreeNode* root, int level, vector<int> &ans)
    {
        if(root==nullptr)
        {
            return;
        }
        if(ans.size()==level)
        {
            ans.push_back(root->val);
        }
        rightView(root->right,level+1,ans);
        rightView(root->left,level+1,ans);
    }
public:
    vector<int> rightSideView(TreeNode* root) {
        vector<int> ans;
        rightView(root,0,ans);
        return ans;
    }
};
```

---

## Left Side View of Binary Tree

**[Left View of Binary Tree](https://www.geeksforgeeks.org/problems/left-view-of-binary-tree/1)**

Given a Binary Tree, return Left view of it. Left view of a Binary Tree is set of nodes visible when tree is visited from Left side. The task is to complete the function **leftView()**, which accepts root of the tree as argument. If no left view is possible, return an empty tree.

Left view of following tree is 1 2 4 8.
```
          1  
       /     \  
     2        3  
   /   \    / \  
  4     5   6    7  
   \  
     8   
```

**Example 1:**

**Input:**
```
   1
 /  \
3    2
```

**Output:** 1 3


**Example 2:**

**Input:**
![](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20190221103723/leftview.jpg)

**Output:** 10 20 40

**Your Task:**  
You just have to **complete** the function **leftView()** that returns an array containing the nodes that are in the left view. The newline is automatically appended by the driver code.  

**Expected Time Complexity:** O(N).  
**Expected Auxiliary Space:** O(N).

**Constraints:**  
0 <= Number of nodes <= 100  
0 <= Data of a node <= 1000

****
### Optimized Approach

### Complexity

- Time complexity: O(n)
    
- Space complexity: O(h)
    

where **h** : the height of the binary tree and **n** : the number of nodes in the binary tree.

##### Approach

- Create an vector data structure inside both the left side view function
- Call for the recursive _left function with the (root,level,vector). Here level will be initially passed as 0.
- Return the vector.
- Now in the recursive_left function
    - If vector size is equal to the level then push_back its node value to the vector data structure.
    - Otherwise call recursive_left for (node->left,level+1,vector)
    - Call recursive_left for (node->right,level+1,vector)

![WhatsApp Image 2024-03-07 at 22.31.58_182e7771.jpg](https://assets.leetcode.com/users/images/118d511b-6613-4755-9125-b96ccfc9dc55_1709830953.9657454.jpeg)

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
// Time Complexity: O(n) and Space Complexity: O(h)
// where h : the height of the binary tree and n : the number of nodes in the binary tree.
class Solution {
private:
    void leftView(TreeNode* root, int level, vector<int> &ans)
    {
        if(root==nullptr)
        {
            return;
        }
        if(ans.size()==level)
        {
            ans.push_back(root->val);
        }
        leftView(root->left,level+1,ans);
        leftView(root->right,level+1,ans);
        
    }
public:
    vector<int> leftSideView(TreeNode* root) {
        vector<int> ans;
        leftView(root,0,ans);
        return ans;
    }
};
```

**Important Link**
1. **[Solution Link](https://leetcode.com/problems/binary-tree-right-side-view/solutions/4838732/best-c-solution-optimized-approach-left-right-view-of-binary-tree-with-explanation)**
2. **[Video Link](https://youtu.be/KV4mRzTjlAk)**




