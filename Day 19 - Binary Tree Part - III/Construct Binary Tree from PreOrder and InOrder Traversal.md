
**[Construct Binary Tree from Preorder and Inorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/description/)**

Given two integer arrays `preorder` and `inorder` where `preorder` is the preorder traversal of a binary tree and `inorder` is the inorder traversal of the same tree, construct and return _the binary tree_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/tree.jpg)

```
Input: preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
Output: [3,9,20,null,null,15,7]
```

**Example 2:**

```
Input: preorder = [-1], inorder = [-1]
Output: [-1]
```


**Constraints:**
- `1 <= preorder.length <= 3000`
- `inorder.length == preorder.length`
- `-3000 <= preorder[i], inorder[i] <= 3000`
- `preorder` and `inorder` consist of **unique** values.
- Each value of `inorder` also appears in `preorder`.
- `preorder` is **guaranteed** to be the preorder traversal of the tree.
- `inorder` is **guaranteed** to be the inorder traversal of the tree.


***

###  Optimized Approach

### Complexity

- Time complexity: O(n)
    
- Space complexity: O(n)
    

where:

- n: number of nodes in a binary tree
- inStart: inorderStart
- inEnd: inorderEnd
- preStart: postorderStart
- preEnd: postorderEnd

#### Explanation:

Before we dive into the algorithm, it's essential to grasp the significance of `inorder` and `preorder` traversals. Inorder traversal allows us to identify a node and its left and right subtrees, while preorder traversal ensures we always encounter the root node first. Leveraging these properties, we can uniquely construct a binary tree. The core of our approach lies in a recursive algorithm that creates one node at a time. We locate this root node in the inorder traversal, which splits the array into the left and right subtrees.

![image.png](https://assets.leetcode.com/users/images/2c3d9d9f-56c1-4e02-9170-45dc5cda5ac7_1714910227.1941116.png)

The inorder array keeps getting divided into left and subtrees hence to avoid unnecessary array duplication, we use variables `(inStart, inEnd)` and `(preStart, preEnd)` on the inorder and preorder array respectively. These variables effectively define the boundaries of the current subtree within the original inorder and preorder traversals. Everytime we encounter the root of a subtree via preorder traversal, we locate its position in the inorder array to get the left and right subtrees. So to save complexity on the linear look up, we employ a hashmap to store the index of each element in the inorder traversal. This transforms the search operation into a constant-time lookup.

#### Algorithm:

**Step 1:** Create an empty map to store the indices of elements in the inorder traversal. Iterate through each element in the inorder traversal and store its index in the `map (mpp)` using the element as the key and its index as the value.

![image.png](https://assets.leetcode.com/users/images/d0e0e20e-e920-4bc5-a097-7a9de081ae24_1714910241.9357529.png)

**Step 2:** Create a recursive helper function `buildTree` with the following parameters:

1. Preorder vector
2. Start index of preorder `(preStart)`, initially set to `0`
3. End index of preorder `(preEnd)`, initially set to `preorder.size() - 1`.
4. Inorder vector
5. Start index of inorder `(inStart)`, initially set to `0`.
6. End index of inorder `(inEnd)`, initially set to `inorder.size() - 1`.
7. `Map` for efficient root index lookup in the inorder traversal.

**Step 3: Base Case:** Check if preStart is greater than preEnd or inStart is greater than inEnd. If true, return NULL, indicating an empty subtree/node.

![image.png](https://assets.leetcode.com/users/images/e3532c3a-0304-43b3-82aa-a9686e4aeeb7_1714910259.67219.png)

**Step 4:** The root node for the current subtree is the first element in the preorder traversal (preorder[preStart]). Find the index of this root node in the inorder traversal using the map `(mpp[rootValue])`. This is the rootIndex.

**Step 5:** Hence, the left subtree ranges from inStart to rootIndex. Subtracting these indexes gives us the leftSubtreeSize.

**Step 6:** To Make two recursive calls to buildTree to build the left and right subtrees: For the left subtree:

1. Update `preStart to preStart + 1` (moving to the next element in preorder)
2. Update `preEnd to preStart + leftSubtreeSize` (end of left subtree in preorder)
3. Update `inEnd to rootIndex - 1` (end of left subtree in inorder)

For the right subtree:

1. Update `preStart to preStart + leftSubtreeSize + 1` (moving to the next element after the left subtree)
2. Update `preEnd to the original preEnd` (end of right subtree in preorder)
3. Update `inStart to rootIndex + 1` (start of right subtree in inorder)

**Step 7:** Return the root node constructed for the current subtree. The function returns the root of the entire binary tree constructed from the preorder and inorder traversals.

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

/*
Optimized Approach
Time complexity -> O(n) and Space -> O(n)
where:
- n: number of nodes in a binary tree
- inStart: inorderStart
- inEnd: inorderEnd
- preStart: postorderStart
- preEnd: postorderEnd
*/
class Solution {
    TreeNode* constructBinaryTree(vector<int> &inorder, int inStart,int inEnd,vector<int> &preorder, int preStart, int preEnd, map<int,int> &mpp){
        if(preStart>preEnd || inStart>inEnd){
            return nullptr;
        }
        TreeNode *root=new TreeNode(preorder[preStart]);
        int inRoot=mpp[preorder[preStart]];
        int numsLeft=inRoot-inStart;
        root->left=constructBinaryTree(inorder,inStart,inRoot-1,preorder,preStart+1,preStart+numsLeft,mpp);
        root->right=constructBinaryTree(inorder,inRoot+1,inEnd,preorder,preStart+numsLeft+1,preEnd,mpp);
        return root;
    }
public:
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        if(inorder.size()!=preorder.size()){
            return nullptr;
        }
        map<int,int> mpp;
        for(int i=0;i<inorder.size();i++){
            mpp[inorder[i]]=i;
        }
        return constructBinaryTree(inorder,0,inorder.size()-1, preorder,0,preorder.size()-1,mpp);
    }
};
```



**Important Link**
1. **[Video Link](https://youtu.be/aZNaLrVebKQ)**
2. **[Solution Link](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/solutions/5116112/optimized-approach-with-detailed-explanation-best-c-solution-striver-solution)**
3. **[For Detailed Solution](https://takeuforward.org/data-structure/construct-a-binary-tree-from-inorder-and-preorder-traversal/)**

