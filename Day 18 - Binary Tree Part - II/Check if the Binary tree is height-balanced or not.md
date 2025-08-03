
**[Balanced Binary Tree](https://leetcode.com/problems/balanced-binary-tree/description/)**


Given a binary tree, determine if it is  **height-balanced**

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/06/balance_1.jpg)

```
Input: root = [3,9,20,null,null,15,7]
Output: true
```

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/10/06/balance_2.jpg)

```
Input: root = [1,2,2,3,3,null,null,4,4]
Output: false
```

**Example 3:**

```
Input: root = []
Output: true
```

**Constraints:**

- The number of nodes in the tree is in the range `[0, 5000]`.
- `-104 <= Node.val <= 104`


***
### Brute Force Approach

### Complexity

- Time complexity: O(n2)
    
- Space complexity: O(n)
    

#### Dry Run

![image.png](https://assets.leetcode.com/users/images/61ce9176-51a7-4ee4-b417-6b138d55263e_1710521147.4282882.png)

Start traversing the tree, the example given in above diagram:

- Reach on **Node 4**, call Height Function , Left height = 3 , Right height = 4 so Absolute Difference between two is Abs(3 – 4) = 1.
- Reach on **Node 7**, call Height Function , Left height = 2 , Right height = 1 so Absolute Difference between two is Abs(2 – 1) = 1.
- Reach on **Node 2**, call Height Function , Left height = 1 , Right height = 0 so Absolute Difference between two is Abs(1 – 0) = 1.
- Reach on **Node 0**, call Height Function , Left height = 0 , Right height = 0 so Absolute Difference between two is Abs(0 – 0) = 0.
- Now, on **PostOrder of Node 0,** the left subtree (null) gives true & right subtree (null) gives true , as both are true , return true.
- Now, on **PostOrder of Node 2,** the left subtree (0) gives true & right subtree (null) gives true , as both are true , return true.  
- Reach on **Node 11**, call Height Function , Left height = 0 , Right height = 0 so Absolute Difference between two is Abs(0 – 0) = 0.
- Now , on **PostOrder of Node 11,** the left subtree (null) gives true & right subtree (null) gives true , as both are true , return true.
- Now ,on **PostOrder of Node 7,** the left subtree (2) gives true & right subtree (11) gives true , as both are true , return true.
- Reach on **Node 8**, call Height Function , Left height = 3 , Right height = 1 so Absolute Difference between two is Abs(3 – 1) = 2. Here Condition violates , simply return false, no need to call further
- Now , on **PostOrder of Node 4,** the left subtree (7) gives true & right subtree (8) gives false , so any one of subtree gives false , return false.

![WhatsApp Image 2024-03-15 at 22.11.41_0ef97790.jpg](https://assets.leetcode.com/users/images/221348fd-cac8-43bd-9a7e-8c27b8ce8bae_1710520949.6764627.jpeg)

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
// Time complexity -> O(n^2) and Space -> O(n)
class Solution {
private:
    int height(TreeNode *root){
        if(root==nullptr){
            return 0;
        }
        int leftHeight=height(root->left);
        int rightHeight=height(root->right);
        return 1+max(leftHeight,rightHeight);
    }
public:
    bool isBalanced(TreeNode* root) {
        if(root==nullptr){
            return true;
        }
        int leftHeight=height(root->left);
        int rightHeight=height(root->right);

        if(abs(leftHeight-rightHeight)>1){
            return false;
        }

        bool leftBalanced=isBalanced(root->left);
        bool rightBalanced=isBalanced(root->right);

        return leftBalanced && rightBalanced;
    }
};
```

### Optimized Approach

### Complexity

- Time complexity: O(n)
    
- Space complexity: O(n)
    

#### Algorithm

- Start traversing the tree recursively and do work in Post Order.
- For each call, caculate the height of the root node, and return it to previous calls.  
- Simultaneously, in the Post Order of every node , Check for condition of balance as information of left and right subtree height is available.
- If it is balanced , simply return height of current node and if not then return -1.
- Whenever the subtree result is -1 , simply keep on returning -1.

#### Dry run

![image.png](https://assets.leetcode.com/users/images/e6f2620f-97ae-4a51-909c-c689176cbc5f_1710521267.1773055.png)

- Reach on **Node 0**, Left child = null so 0 Height , Right child = null so 0 Height , Difference is 0-0 = 0 , ( 0 <= 1 ) so return height , i.e. Max(0,0) + 1 = 1. 
- Reach on **Node 2** , Left subtree height = 1 , Right subtree height =  0, Difference is 1-0 = 1 , ( 1 <= 1 ) so return height , i.e. Max(1,0) + 1 = 2.
- Reach on **Node 11** , Left child = null so 0 Height , Right child = null so 0 Height , Difference is 0-0 = 0 , ( 0 <= 1 ) so return height , i.e. Max(0,0) + 1 = 1.
- Reach on **Node 7** , Left subtree height = 2 , Right subtree height =  1, Difference is 2-1 = 1 , ( 1 <= 1 ) so return height , i.e. Max(2,1) + 1 = 3.
- Reach on **Node 5** , Left child = null so 0 Height , Right child = null so 0 Height , Difference is 0-0 = 0 , ( 0 <= 1 ) so return height , i.e. Max(0,0) + 1 = 1.
- Reach on **Node 3** , Left subtree height = 1 , Right subtree height =  0, Difference is 1-0 = 1 , ( 1 <= 1 ) so return height , i.e. Max(1,0) + 1 = 2.
- Reach on **Node 1** , Left subtree height = 2 , Right subtree height =  0, Difference is 2-0 = 2 , ( 2 > 1 ) i.e. Tree is **not Balanced** , so return -1.
- Reach on **Node 8** , Left subtree height = **-1**  , indicates that tree is not balanced, simply return -1;
- Reach on **Node 4** , Left subtree height = 3 , Right subtree height =  **-1**, therefore indicates that tree is not balanced , simply return -1;
- In the Main function , If the final Height of tree is -1 return false as tree is not balanced , else return true.

![WhatsApp Image 2024-03-15 at 22.11.41_610e139b.jpg](https://assets.leetcode.com/users/images/66570ee0-9732-4b5e-8949-c6cbf17e648d_1710520928.3514154.jpeg)

### Code

```cpp
// Optimized Approach
// Time complexity -> O(n) and Space -> O(n)
class Solution {
private:
    int height(TreeNode *root){
        if(root==nullptr){
            return 0;
        }
        int leftHeight=height(root->left);
        int rightHeight=height(root->right);
        if(leftHeight==-1 || rightHeight==-1 || abs(leftHeight-rightHeight)>1){
            return -1;
        }
        return 1+max(leftHeight,rightHeight);
    }
public:
    bool isBalanced(TreeNode* root) {
        return height(root)!=-1?true:false;
    }
};
```

**Important Link**
1. **[Solution Link](https://leetcode.com/problems/balanced-binary-tree/solutions/4880228/best-c-solutio-2-approach-brute-force-and-optimized-approach-with-explanation)**
2. **[Video Link](https://youtu.be/Yt50Jfbd8Po)**