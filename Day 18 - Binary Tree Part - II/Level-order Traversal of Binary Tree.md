
**[102. Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/description/)**

Given the `root` of a binary tree, return _the level order traversal of its nodes' values_. (i.e., from left to right, level by level).

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/tree1.jpg)

```
Input: root = [3,9,20,null,null,15,7]
Output: [[3],[9,20],[15,7]]
```

**Example 2:**

```
Input: root = [1]
Output: [[1]]
```

**Example 3:**

```
Input: root = []
Output: []
```


**Constraints:**

- The number of nodes in the tree is in the range `[0, 2000]`.
- `-1000 <= Node.val <= 1000`

***

### Optimized Approach

### Complexity

- Time complexity: O(n)
    
- Space complexity: O(n)
    

#### Algorithm

- Take a queue data structure and push the root node to the queue.
- Set a while loop that will run until our queue is non-empty.
- In every iteration:
    - Get the size of the current queue (`s`) and initialize an empty vector (`temp`) to store the values of nodes at the current level.
    - Run a loop for `i` from 0 to `s-1`:
        - Pop a node from the front of the queue and assign it to a variable (`tempNode`).
        - If `tempNode` has a left child, push it to the queue.
        - If `tempNode` has a right child, push it to the queue.
        - Add the value of `tempNode` to the `temp` vector.
    - Push the `temp` vector to the `ans` vector, representing the values of nodes at the current level.

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
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> ans;
        queue<TreeNode*> q;
        if(root==nullptr)
        {
            return ans;
        }
        q.push(root);
        while(!q.empty())
        {
            int s=q.size();
            vector<int> temp;
            for(int i=0;i<s;i++)
            {
                root=q.front();
                q.pop();
                if(root->left!=nullptr)
                {
                    q.push(root->left);
                }
                if(root->right!=nullptr)
                {
                    q.push(root->right);
                }
                temp.push_back(root->val);
            }
            ans.push_back(temp);   
        }
        return ans;
    }
};
```

**Important Link**
1. **[Solution Link](https://leetcode.com/problems/binary-tree-level-order-traversal/solutions/4786037/easy-c-solution-beats-100-00-of-users-with-c-optimized-approach-with-explanation)**
2. **[Video Link](https://youtu.be/EoAsWbO7sqg?si=eSCa22aTieH5E3Cz)**