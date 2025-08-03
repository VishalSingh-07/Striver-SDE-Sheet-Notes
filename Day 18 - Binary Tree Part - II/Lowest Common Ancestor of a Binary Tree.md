
**[Lowest Common Ancestor of a Binary Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/description/)**

Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.

According to the [definition of LCA on Wikipedia](https://en.wikipedia.org/wiki/Lowest_common_ancestor): “The lowest common ancestor is defined between two nodes `p` and `q` as the lowest node in `T` that has both `p` and `q` as descendants (where we allow **a node to be a descendant of itself**).”

**Example 1:**

![](https://assets.leetcode.com/uploads/2018/12/14/binarytree.png)

```
Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1 
Output: 3 
Explanation: The LCA of nodes 5 and 1 is 3.
```

**Example 2:**

![](https://assets.leetcode.com/uploads/2018/12/14/binarytree.png)

```
Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4 
Output: 5 
Explanation: The LCA of nodes 5 and 4 is 5, since a node can be a descendant of itself according to the LCA definition.
```

**Example 3:**

```
Input: root = [1,2], p = 1, q = 2
Output: 1
```


**Constraints:**

- The number of nodes in the tree is in the range `[2, 105]`.
- `-109 <= Node.val <= 109`
- All `Node.val` are **unique**.
- `p != q`
- `p` and `q` will exist in the tree.


***
## Warning:

Before Solving this Problem, Please solve this **[Path to Given Node](https://www.interviewbit.com/problems/path-to-given-node/)** Question, Which give you clear understanding of the brute force approach

**Lowest Common Ancestor(LCA):** The lowest common ancestor is defined between two nodes x and y as the lowest node in T that has both x and y as descendants (where we allow a node to be a descendant of itself.

### Brute Force Approach

### Complexity

- Time complexity: O(2*n)
    
- Space complexity: O(2*h)
    

where n: number of nodes in a binary tree and h: height of the binary tree

![WhatsApp Image 2024-04-15 at 23.50.40_b54f5171.jpg](https://assets.leetcode.com/users/images/e8b81d4d-2c28-45f8-8288-f9ef89a6ddef_1713206078.8473048.jpeg)

### Code

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */

// Brute Force Appproach
// Time complexity -> O(2*n) and Space -> O(2*h)
// where n: number of nodes in a binary tree and h: height of the binary tree
class Solution {
private:
    // Helper function to find the path from root to a given node
    bool getPath(TreeNode *root, vector<TreeNode*> &path, TreeNode* target) {
        // Base case: if root is null, return false as we've reached the end
        if (root == nullptr) {
            return false;
        }
        
        // Add current node to the path
        path.push_back(root);

        // If the current node is the target, return true to indicate we've found the path
        if (root == target) {
            return true;
        }
        
        // Recursively search in left and right subtrees
        if (getPath(root->left, path, target) || getPath(root->right, path, target)) {
            return true; // Return true if target found in either subtree
        }
        
        // If target is not found in the subtree rooted at current node, backtrack
        path.pop_back();
        return false;
    }

public:
    // Main function to find lowest common ancestor of two nodes
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        // Paths to store the nodes from root to p and q
        vector<TreeNode*> pathToP, pathToQ;
        
        // Find paths from root to p and q
        getPath(root, pathToP, p);
        getPath(root, pathToQ, q);

        // Traverse both paths simultaneously to find the lowest common ancestor
        TreeNode *lca = nullptr;
        int i = 0, j = 0;
        while (i < pathToP.size() && j < pathToQ.size()) {
            if (pathToP[i] == pathToQ[j]) {
                lca = pathToP[i]; // Update lowest common ancestor
            } else {
                break; // Stop traversal if nodes diverge
            }
            i++;
            j++;
        }
        
        return lca;
    }
};
```

### Optimized Approach

### Complexity

- Time complexity: O(n)
    
- Space complexity: O(h)
    

where n: number of nodes in a binary tree and h: height of the binary tree

#### Intuition:
The very first thing we can observe from the question is that we can find the LCA of 2 given nodes from 

        i) Left subtree or in
       ii) Right subtree, if not in both the subtrees then root will be the LCA.

#### Approach:

1. If root is null or if root is x or if root is y then return root
2. Made a recursion call for both

i) Left subtree 
ii) Right subtree

Because we would find LCA in the left or right subtree only.

3. If the left subtree recursive call gives a null value that means we haven’t found LCA in the left subtree, which means we found LCA on the right subtree. So we will return right.

4. If the right subtree recursive call gives null value, that means we haven’t found LCA on the right subtree, which means we found LCA on the left subtree. So we will return left .

5.  If both left & right calls give values (not null)  that means the root is the LCA.

Let’s take an example and will try to understand the approach more clearly:

##### LCA of (x,y) = > (4,5) = ? (from above given example)

- Root is 1 which is not null and x,y is not equal to root, So the 1st statement in approach  will not execute.

- i) Call left subtree, While calling recursively it will find 4 and this call will return 4 to its parent 

_Point to Note: At present, the root is 2 ( Look at below recursion tree for better understanding)_

i) Call the right subtree ( i.e right of 2), While calling recursively it will find 5  and this call will return 5 to its parent.

- Now the left recursive  call returns value (not null) i.e 4 and also the right recursive call returns value (not null) i.e 5 to its root ( at present root is 2) , and this 2 will return itself to its root i.e to 1 (main root).  

_Point to Note: At present, the root is 1 ( Look at below recursion tree for better understanding)_

- Now, the left subtree gives a value i.e 2.

- Right recursive call will give null value .because x,y are not present in the right subtree.

- As we know if the right recursive call gives null then we return the answer which we got from the left call, So we will return 2.

-  Hence LCA of (4,5) is 2.


**For a better understanding of the** **above example (LCA OF 4,5) :**  

![image.png](https://assets.leetcode.com/users/images/8cb34c91-22c8-438d-bc48-f76c6b9218ee_1713205837.417183.png)


#### Algorithm

1. **Base Cases**:
    - If the current node is null, or it matches either `p` or `q`, return the current node.
2. **Recursive Calls**:
    - Recursively search for `p` and `q` in the left and right subtrees.
3. **Result Merging**:
    - If both left and right subtrees return non-null results, the current node is the lowest common ancestor.
    - If one subtree returns null and the other returns a non-null result, return the non-null result.
    - If both subtrees return null, return null.

#### Dry Run

![WhatsApp Image 2024-04-15 at 23.50.40_a752b891.jpg](https://assets.leetcode.com/users/images/5dabc4c2-57c6-4538-acea-b42ba39f619e_1713206053.1535385.jpeg)

![WhatsApp Image 2024-04-15 at 23.50.41_b670f0d9.jpg](https://assets.leetcode.com/users/images/87dc0184-c279-4605-92e3-f08024613ea9_1713206043.5651593.jpeg)

### Code

```kotlin
// Optimized Appproach
// Time complexity -> O(n) and Space -> O(h)
// where n: number of nodes in a binary tree and h: height of the binary tree
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if(root==nullptr || root==p || root==q){
            return root;
        }

        TreeNode* left=lowestCommonAncestor(root->left,p,q);
        TreeNode* right=lowestCommonAncestor(root->right,p,q);

        if(left==nullptr){
            return right;
        }
        else if(right==nullptr){
            return left;
        }
        //both left and right are not null, we found our result
        else{
            return root;
        }
    }
};
```



***

##### Important Link
1. **[Video Link](https://youtu.be/_-QHfMDde90)**
2. **[Solution Link](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/solutions/5028379/2-approach-best-c-solution-brute-force-optimized-approach-with-explanation)**




