
**[662. Maximum Width of Binary Tree](https://leetcode.com/problems/maximum-width-of-binary-tree/)**

Given the `root` of a binary tree, return _the **maximum width** of the given tree_.

The **maximum width** of a tree is the maximum **width** among all levels.

The **width** of one level is defined as the length between the end-nodes (the leftmost and rightmost non-null nodes), where the null nodes between the end-nodes that would be present in a complete binary tree extending down to that level are also counted into the length calculation.

It is **guaranteed** that the answer will in the range of a **32-bit** signed integer.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/05/03/width1-tree.jpg)

```
Input: root = [1,3,2,5,3,null,9]
Output: 4
Explanation: The maximum width exists in the third level with length 4 (5,3,null,9).
```

**Example 2:**

![](https://assets.leetcode.com/uploads/2022/03/14/maximum-width-of-binary-tree-v3.jpg)

```
Input: root = [1,3,2,5,null,null,9,6,null,7]
Output: 7
Explanation: The maximum width exists in the fourth level with length 7 (6,null,null,null,null,null,7).
```

**Example 3:**

![](https://assets.leetcode.com/uploads/2021/05/03/width3-tree.jpg)

```
Input: root = [1,3,2,5]
Output: 2
Explanation: The maximum width exists in the second level with length 2 (3,2).
```

**Constraints:**

- The number of nodes in the tree is in the range `[1, 3000]`.
- `-100 <= Node.val <= 100`



*****
### Intuition

To determine the maximum width of a tree, an effective strategy would be to assign and identify indexes for the leftmost and rightmost nodes at each level. Using these indexes, we can calculate the width for each level by subtracting the index of the leftmost node from that of the rightmost node.

![image.png](https://assets.leetcode.com/users/images/13db7540-ae57-49ec-85ac-81b611949626_1716202113.2618709.png)

Start by assigning an index to the root node as 0. For each level, the left child gets an index equal to 2 * parent index, and the right child gets an index equal to 2 * parent index + 1. Using a level order traversal, we use the leftmost and rightmost nodes at each level and using their indices, get the width at that level. Keep track of the maximum width encountered during the traversal. Whenever a wider level is found, update the maximum width.

![image.png](https://assets.leetcode.com/users/images/a809de4d-22b7-42f3-a340-53e1aceeaf74_1716202119.2555408.png)

### Optimized Approach

### Complexity

- Time complexity: O(n)
    
- Space complexity: O(n)
    

where n: number of nodes in a binary tree

### Algorithm:

**Step 1:** Initialize a variable `ans` to store the maximum width. If the root is null, `return 0` as the width of an empty tree is zero.

**Step 2:** Create a queue to perform level-order traversal and each element of this queue would be a pair containing a node and its vertical index. Push the root node and its position `(initially 0)` into the queue.

**Step 3:** While the queue is not empty, perform the following steps:

1. Get the number of nodes at the current level (size).
2. Get the position of the front node in the current level which is the leftmost minimum index at that level.
3. Initialize variables first and last to store the first and last positions of nodes in the current level.

**Step 4: Backtracking:** For each node in the current level:

1. Calculate the current position relative to the minimum position in the level.
2. Get the current node (node) from the front of the queue.
3. If this is the first node in the level, update the first variable.
4. If this is the last node in the level, update the last variable.
5. Enqueue the left child of the current node with index: `2 x current index - 1`.
6. Enqueue the right child of the current node with index: `2 x current index + 1`.

![image.png](https://assets.leetcode.com/users/images/322c4c06-d8d1-4367-8344-52448f30b2bb_1716202213.2436912.png)

**Step 5:** Update the maximum width (ans) by calculating the difference between the first and last positions, and `adding 1`.

**Step 6:** Repeat the `level-order traversal` until all levels are processed. The final value of `ans` represents the maximum width of the binary tree, return it.

![WhatsApp Image 2024-05-20 at 16.13.22_61f433c7.jpg](https://assets.leetcode.com/users/images/9d18c70f-a2c3-4281-a2dc-acde7d8b9ada_1716202293.007015.jpeg)

![WhatsApp Image 2024-05-20 at 16.13.23_c92675f0.jpg](https://assets.leetcode.com/users/images/f2d8209d-02c6-44d0-bfa6-991ebf50ee4d_1716202302.2202027.jpeg)

![WhatsApp Image 2024-05-20 at 16.13.23_778a0dad.jpg](https://assets.leetcode.com/users/images/a5357af2-a828-43bf-ba3b-721c644e6f14_1716202313.910823.jpeg)

![WhatsApp Image 2024-05-20 at 16.13.21_f49f77b6.jpg](https://assets.leetcode.com/users/images/20ee21ed-94a8-4133-8e90-7838da983b97_1716202323.7772486.jpeg)

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
// where n: number of nodes in a binary tree
class Solution {
public:
    int widthOfBinaryTree(TreeNode* root) {
        if(root==nullptr){
            return 0;
        }
        int ans=0;
        queue<pair<TreeNode*,int>> q;
        q.push({root,0});
        while(!q.empty()){
            int sz=q.size();
            int mmin=q.front().second;
            int first,last;
            for(int i=0;i<sz;i++){
                int currentId=q.front().second - mmin;
                TreeNode *node=q.front().first;
                q.pop();
                if(i==0){
                    first=currentId;
                }
                if(i==sz-1){
                    last=currentId;
                }
                if(node->left!=nullptr){
                    q.push({node->left,(long long)currentId*2+1});
                }
                if(node->right!=nullptr){
                    q.push({node->right,(long long)currentId*2+2});
                }
            }
            ans=max(ans,last-first+1);
        }
        return ans;
    }
};
```


**Important Link**
1. **[Video Link](https://youtu.be/ZbybYvcVLks?si=OglytVsdnCT_QTwg)**
2. **[Solution Link](https://leetcode.com/problems/maximum-width-of-binary-tree/solutions/5183861/optimized-approach-with-explanation-best-c-solution-striver-solution)**
3. **[For Detailed Solution](https://takeuforward.org/data-structure/maximum-width-of-a-binary-tree/)**