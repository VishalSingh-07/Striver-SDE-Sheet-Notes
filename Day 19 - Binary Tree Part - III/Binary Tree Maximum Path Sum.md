
**[Binary Tree Maximum Path Sum](https://leetcode.com/problems/binary-tree-maximum-path-sum/description/)**

A **path** in a binary tree is a sequence of nodes where each pair of adjacent nodes in the sequence has an edge connecting them. A node can only appear in the sequence **at most once**. Note that the path does not need to pass through the root.

The **path sum** of a path is the sum of the node's values in the path.

Given the `root` of a binary tree, return _the maximum **path sum** of any **non-empty** path_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/13/exx1.jpg)

```
Input: root = [1,2,3]
Output: 6
Explanation: The optimal path is 2 -> 1 -> 3 with a path sum of 2 + 1 + 3 = 6.
```

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/10/13/exx2.jpg)

```
Input: root = [-10,9,20,null,null,15,7]
Output: 42
Explanation: The optimal path is 15 -> 20 -> 7 with a path sum of 15 + 20 + 7 = 42.
```

**Constraints:**

- The number of nodes in the tree is in the range `[1, 3 * 104]`.
- `-1000 <= Node.val <= 1000`


***

### Optimized Approach

### Complexity

- Time complexity: O(n)
    
- Space complexity: O(n)
    

#### Explanation

A brute force approach would be to generate all paths and compare them. Generating all paths will be a time-costly activity therefore we need to look for something else.

We first need to define what is the maximum path sum through a given node (when that node is acting as the root node/curving point). At a given node with a value, if we find the max leftSumPath in the left-subtree and the max rightSumPath in the right subtree, then the maxPathSum through that node is `value+(leftSumPath+rightSumPath)`.

![image.png](https://assets.leetcode.com/users/images/d74db8fa-9779-4c08-83db-6d437b64b509_1711108145.9294827.png)

Now we can apply this formula at every node by doing a simple tree traversal and storing the maximum value (our answer) in a reference variable.

For our recursion to work, it is very important to understand what value we return from our function. In our recursive function, we find and compare the maxPathSum from a given node when it is the root/turning point of the path. But what we return is the maxPathSum of that same node when it is NOT the root/turning point of the path. To find the latter maxPath, we no longer have the liberty to consider both leftMaxPath and rightMaxPath, we will simply take the maximum of the two and it to the value of the node.

![image.png](https://assets.leetcode.com/users/images/8fe84f82-558d-418c-a6ca-93af344bdb37_1711108185.3961444.png)

#### To summarize:

- Initialize a `maxi` variable to store our final answer.
- Do a simple tree traversal. At each node, find recursively its leftMaxPath and its rightMaxPath.
- Calculate the maxPath through the node as `val + (leftMaxPath + rightMaxPath)` and update `maxi` accordingly.
- Return the maxPath when node is not the curving point as `val + max(leftMaxPath, rightMaxPath)`.

![WhatsApp Image 2024-03-22 at 17.26.12_8d538ab4.jpg](https://assets.leetcode.com/users/images/e16a2dc1-25b3-470e-a8ec-95de284ea5d3_1711108632.0771055.jpeg)

![WhatsApp Image 2024-03-22 at 17.26.13_4eb66f9c.jpg](https://assets.leetcode.com/users/images/19a10aa6-7533-4032-9f9b-9f3d4e2e2131_1711108640.5074263.jpeg)

![WhatsApp Image 2024-03-22 at 17.26.12_33ec6fcc.jpg](https://assets.leetcode.com/users/images/dbd59836-eec2-4cbf-917d-b11da3bd37ed_1711108659.0318823.jpeg)

![WhatsApp Image 2024-03-22 at 17.26.13_444e9749.jpg](https://assets.leetcode.com/users/images/90992325-563f-478f-ac15-eec8b2075613_1711108649.5648232.jpeg)

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

    // Function to find the maximum sum of a path starting from the current node downwards.
    // It updates the 'maxi' variable with the maximum path sum found so far.
    int maxPathDown(TreeNode* node, int &maxi){

        // Base case: If the current node is null, return 0.
        if(node==nullptr){
            return 0;
        }
        // Calculate the maximum sum of paths starting from the left and right child nodes.

        // Maximum sum of the path starting from the left child
        int leftSum=max(0,maxPathDown(node->left,maxi)); 

        // Maximum sum of the path starting from the right child
        int rightSum=max(0,maxPathDown(node->right,maxi)); 

        // Update 'maxi' with the maximum of the following:
        // 1. Current maximum value.
        // 2. Sum of the path through the current node, left child, and right child.
        maxi=max(maxi,leftSum+rightSum+node->val);

        // Return the maximum sum starting from the current node going downwards.
        // This will be the maximum of:
        // 1. The value of the current node.
        // 2. The sum of the path starting from either left or right child, whichever is greater.
        return (node->val)+max(leftSum,rightSum);
    }
public:
    int maxPathSum(TreeNode* root) {
        int maxi=INT_MIN;
        maxPathDown(root,maxi); 
        return maxi;
    }
};
```



**Important Link**
1. **[Solution Link](https://leetcode.com/problems/binary-tree-maximum-path-sum/solutions/4910129/best-c-solution-optimized-approach-with-explanation-striver-solution)**
2. **[Video Link](https://youtu.be/WszrfSwMz58)**
3. **[For Detailed Solution](https://takeuforward.org/data-structure/maximum-sum-path-in-binary-tree/)** 