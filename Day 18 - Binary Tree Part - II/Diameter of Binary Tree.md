
**[Diameter of Binary Tree](https://leetcode.com/problems/diameter-of-binary-tree/description/)**

Given the `root` of a binary tree, return _the length of the **diameter** of the tree_.

The **diameter** of a binary tree is the **length** of the longest path between any two nodes in a tree. This path may or may not pass through the `root`.

The **length** of a path between two nodes is represented by the number of edges between them.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/03/06/diamtree.jpg)

```
Input: root = [1,2,3,4,5]
Output: 3
Explanation: 3 is the length of the path [4,2,1,3] or [5,2,1,3].
```

**Example 2:**

```
Input: root = [1,2]
Output: 1
```

**Constraints:**

- The number of nodes in the tree is in the range `[1, 104]`.
- `-100 <= Node.val <= 100`


***
### Brute Force Approach

### Complexity

- Time complexity: O(n^2)
    
- Space complexity: O(h)
    

where h: height of binary tree and n: number of nodes in binary Tree

#### Algorithm: 

- Traverse the tree recursively.
- At every node, calculate height of left and right subtrees
- Calculate the diameter for every node using the above formula.
- Calculate the maximum of all diameters. This can be done simply using a variable passed by reference in the recursive calls or a global static variable.

#### Dry-run :

![image.png](https://assets.leetcode.com/users/images/c11127d7-2b17-4534-a897-929128e87163_1711020835.7379003.png)

Start traversing the tree.

- Initialize Maximum Diameter variable with Integer.MIN_VALUE.
- Reach on **Node 5** , call Height Function , Left height = 1 , Right height = 4 so Diameter is (1 + 4) = 5. Hence , Maximum Diameter = Max( Integer.MIN_VALUE , 5 ) = 5.
- Reach on **Node 9** , call Height Function , Left height = 0 , Right height = 0 so Diameter is ( 0 + 0) = 0. Hence , Maximum Diameter = Max( 5 , 0 ) = 5.
- Reach on **Node 4** , call Height Function , Left height = 3 , Right height = 3 so Diameter is (3 + 3) = 6. Hence , Maximum Diameter = Max( 5 , 6 ) = 6.
- Reach on **Node 7** , call Height Function , Left height = 2 , Right height = 0 so Diameter is (2 + 0) = 2. Hence , Maximum Diameter = Max( 6,2 ) = 6.
- Reach on **Node 2** , call Height Function , Left height = 1 , Right height = 0 so Diameter is (1 + 0) = 1. Hence , Maximum Diameter = Max( 6 , 1) = 6.
- Reach on **Node 12** , call Height Function , Left height = 0 , Right height = 0 so Diameter is (0 + 0) = 0. Hence , Maximum Diameter = Max( 6 , 0) = 6.
- Reach on **Node 8** , call Height Function , Left height = 2 , Right height = 1 so Diameter is (2 + 1) = 3. Hence , Maximum Diameter = Max( 6 , 3) = 6.
- Reach on **Node 1** , call Height Function , Left height = 1 , Right height = 0 so Diameter is (1 + 0) = 1. Hence , Maximum Diameter = Max( 6 , 1) = 6.
- Reach on **Node 3** , call Height Function , Left height = 0 , Right height = 0 so Diameter is (0 + 0) = 0. Hence , Maximum Diameter = Max( 6 , 0) = 6.
- Reach on **Node 0** , call Height Function , Left height = 0 , Right height = 0 so Diameter is (0 + 0) = 0. Hence , Maximum Diameter = Max( 6 , 0) = 6.

![WhatsApp Image 2024-03-21 at 17.08.35_f62fc58e.jpg](https://assets.leetcode.com/users/images/f3a91f74-b9c7-470c-8320-26f9cd27c181_1711021198.3063793.jpeg)

![WhatsApp Image 2024-03-21 at 17.08.34_e3224cf8.jpg](https://assets.leetcode.com/users/images/18ef8509-1983-41cb-9b18-59ef58ef5c71_1711021206.8037705.jpeg)

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
// Time complexity -> O(n^2) and Space -> O(h)
// where h: height of binary tree and n: number of nodes in binary tree
class Solution {
private:
    int diameter=0;
    int height(TreeNode *root){
        if(root==nullptr){
            return 0;
        }
        return 1+max(height(root->left),height(root->right));
    }
public:
    int diameterOfBinaryTree(TreeNode* root) {
        if(root==nullptr){
            return 0;
        }
        int lh=height(root->left);
        int rh=height(root->right);

        diameter=max(diameter,lh+rh);

        diameterOfBinaryTree(root->left);
        diameterOfBinaryTree(root->right);

        return diameter;
    }
};
```

### Optimized Approach

### Complexity

- Time complexity: O(n)
    
- Space complexity: O(h)
    

where h: height of binary tree and n: number of nodes in binary Tree

#### Approach :

- Start traversing the tree recursively and do work in Post Order.
- In the Post Order of every node , calculate diameter and height of the current node.
- If current diameter is maximum then update the variable used to store the maximum diameter.
- Return height of current node to the previous recursive call.

#### Dry Run :

In Post Order, Start traversing the tree:

![image.png](https://assets.leetcode.com/users/images/6f4475f9-51b4-4a74-b6cf-4baf9f74c67a_1711020922.5221393.png)

- Reach on **Node 6 ,** Left height = 0 as left == null , Right height = 0 as right == null so Diameter is (0 + 0) = 0. Hence , Maximum Diameter = Max( 0 , 0) = 0 and return height = max(0,0)+1 = 1.
- Reach on **Node 0**, Left height = 1 , Right height = 0 as right == null so Diameter is (1 + 0) = 1. Hence , Maximum Diameter = Max( 0 , 1) = 1 and return height = max(1,0)+1 = 2.
- Reach on **Node 9 ,** Left height = 0 as left == null , Right height = 0 as right == null so Diameter is (0 + 0) = 0. Hence , Maximum Diameter = Max( 1 , 0) = 1 and return height = max(0,0)+1 = 1.
- Reach on **Node 4 ,** Left height = 0 as left == null , Right height = 1 , so Diameter is (0 + 1) = 1. Hence , Maximum Diameter = Max( 1 , 1) = 1 and return height = max(0,1)+1 = 2.
- Reach on **Node 14 ,** Left height = 2 , Right height = 2 , so Diameter is (2 + 2) = 4. Hence , Maximum Diameter = Max( 1 , 4) = 4 and return height = max(2,2)+1 = 3.
- Reach on **Node 3 ,** Left height = 3 , Right height = 0 as right == null , so Diameter is (3 + 0) = 3. Hence , Maximum Diameter = Max( 4 , 3) = 4 and return height = max(3,0)+1 = 4.
- Hence , the maximum diameter is 4 .

![WhatsApp Image 2024-03-21 at 17.08.38_62021d6b.jpg](https://assets.leetcode.com/users/images/9d66d0ed-719a-4e39-ab3e-cddda2039603_1711021183.036821.jpeg)

### Code

```cpp
// Optimized Approach
// Time complexity -> O(n) and Space -> O(h)
// where h: height of binary tree and n: number of nodes in binary tree
class Solution {
private:
    int height(TreeNode *root, int &diameter){
        if(root==nullptr){
            return 0;
        }
        int lh=height(root->left, diameter);
        int rh=height(root->right, diameter);
        diameter=max(diameter,lh+rh);
        return 1+max(lh,rh);
    }
public:
    int diameterOfBinaryTree(TreeNode* root) {
        int diameter=0;
        height(root,diameter);
        return diameter;
    }
};
```


**Important Link**
1. **[Solution Link](https://leetcode.com/problems/diameter-of-binary-tree/solutions/4905891/easy-c-solution-2-approach-brute-force-and-optimized-approach-with-explanation)**
2. **[Video Link](https://youtu.be/Rezetez59Nk)**