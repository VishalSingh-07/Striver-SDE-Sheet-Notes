
**[Binary Tree Zigzag Level Order Traversal](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/description/)**

Given the `root` of a binary tree, return _the zigzag level order traversal of its nodes' values_. (i.e., from left to right, then right to left for the next level and alternate between).

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/tree1.jpg)

```
Input: root = [3,9,20,null,null,15,7]
Output: [[3],[20,9],[15,7]]
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
- `-100 <= Node.val <= 100`


***


### Optimized Approach

### Complexity

- Time complexity: O(n)
    
- Space complexity: O(n)
    

where n: number of nodes in a binary tree

**The above idea, could be implemented with a queue.**

- We initially keep an empty queue and push the root node.
- We also need to keep the left to right bool variable that keeps check of the current level we are in.
- As we traverse nodes in the queue, we need to push them in a temporary array.
- If left to right is false we need to reverse the array and push it in our data structure or else, simply push it in our data structure
- In the end, when we have finished traversing the current level, we need to toggle our left to the right variable.

![WhatsApp Image 2024-03-15 at 20.59.53_dd94c667.jpg](https://assets.leetcode.com/users/images/1f209ad4-9446-4db1-97dd-b730e77b0337_1710516818.2527428.jpeg)

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
// Time complexity -> O(n) and Space -> O(n)
class Solution {
public:
    vector<vector<int>> zigzagLevelOrder(TreeNode* root) {
        vector<vector<int>> ans;
        if(root==nullptr){
            return ans;
        }
        queue<TreeNode*> q;
        q.push(root);
        bool leftToRight=true;
        while(!q.empty()){
            int s=q.size();
            vector<int> temp(s);
            for(int i=0;i<s;i++){
                TreeNode* node=q.front();
                q.pop();

                int index=(leftToRight)?i:(s-1-i);
                temp[index]=node->val;

                if(node->left!=nullptr){
                    q.push(node->left);
                }
                if(node->right!=nullptr){
                    q.push(node->right);
                }
            }
            leftToRight=!leftToRight;
            ans.push_back(temp);
        }
        return ans;
    }
};
```


**Important Link**
1. **[Solution Link](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/solutions/4879943/easy-c-solution-optimized-approach-with-explanation)**
2. **[Video Link](https://youtu.be/3OXWEdlIGl4)**