
**[Construct Binary Tree from Inorder and Postorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/)**

Given two integer arrays `inorder` and `postorder` where `inorder` is the inorder traversal of a binary tree and `postorder` is the postorder traversal of the same tree, construct and return _the binary tree_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/tree.jpg)

```
Input: inorder = [9,3,15,20,7], postorder = [9,15,7,20,3]
Output: [3,9,20,null,null,15,7]
```

**Example 2:**

```
Input: inorder = [-1], postorder = [-1]
Output: [-1]
```


**Constraints:**
- `1 <= inorder.length <= 3000`
- `postorder.length == inorder.length`
- `-3000 <= inorder[i], postorder[i] <= 3000`
- `inorder` and `postorder` consist of **unique** values.
- Each value of `postorder` also appears in `inorder`.
- `inorder` is **guaranteed** to be the inorder traversal of the tree.
- `postorder` is **guaranteed** to be the postorder traversal of the tree.


***
### Optimized Approach

### Complexity

- Time complexity: O(n)
    
- Space complexity: O(n)
    
where:
- n: number of nodes in a binary tree
- is: inorderStart
- ie: inorderEnd
- ps: postorderStart
- pe: postorderEnd

#### Explanation:

Inorder traversal is a special traversal that helps us to identify a node and its left and right subtree. Postorder traversal always gives us the root node as its last element. Using these properties we can construct the unique binary tree.

Given this example:

![image.png](https://assets.leetcode.com/users/images/47eba2bb-4124-4da0-9ce6-550db7b996db_1714844685.6052.png)

Here 10 (last element of postorder) is the root element. So we can find its index in the inorder traversal(say elem). The left subtree of the root will be present to the left side of inorder whereas the right subtree of root will be present on the right side of elem in the inorder traversal:

We can define a recursive function that creates one node at a time. First, we create the root node, and then we can take the help of recursion to create its left and right subtrees. In order to make recursion work, we need to provide the correct inorder and postorder traversal of the subtree for every recursive call.

![image.png](https://assets.leetcode.com/users/images/8e4c2378-c85a-4dcb-8cb7-41188dd35524_1714844701.871553.png)

To make more efficient function calls we can use variables (inStart, inEnd) and (postStart and postEnd) in order to point to the start and end of the inorder and postorder traversal respectively, and avoid copying of arrays.

Next, we need to figure out how we are going to search the root index in the inorder traversal. For this, we have two options: Linear Search and Hashmaps. We will choose the second one because it will return us the index in constant time. Before making the first recursive call, we will simply add all the (value, index) pairs to a map and pass it to our recursive function.

If n is the size of the Inorder traversal/Postorder traversal. Then our first function call will be :

![image.png](https://assets.leetcode.com/users/images/44aa00e3-8a0a-4ecc-8d40-75ad51dd531f_1714844715.6650999.png)

Now the main task left is to pass the correct postStart, postEnd, inStart, inEnd to the respective recursive calls for the left and right subtree. We can calculate the number of elements in the left subtree from the root index, say nElems (elem - InStart, where elem is the index of root in inorder traversal). As inorder is [left, root, right] and postorder is [left, right, root] the number of elements (nElems) will easily tell us the preorder and inorder traversal of the subtrees according to the following table:

![image.png](https://assets.leetcode.com/users/images/dbb7e40e-b26c-4c26-a0cd-63bab00a3d65_1714844724.7676766.png)

The base case will be when inStart> inEnd or postStart > postEnd, in that case, we can simply return NULL.

#### Algorithm:

- Create a map to store the inorder indexes.
- Call the function constructTree with all 7 parameters as shown above.
- In the recursive function, first check the base case, if (postStart,>postEnd || inStart> inEnd) then return NULL.
- Construct a node (say root) with the root value( last element of postorder). 
- Find the index of the root, say elem from the hashmap.
- Find the number of elements ( say nElem) in the left subtree  = elem - inStart
-  Call recursively for the left subtree with correct values (shown in the above table) and store the answer received in root->left.
- Call recursively for the right subtree with correct values (shown in the above table) and store the answer received in root->right.
- Return root

![WhatsApp Image 2024-05-04 at 23.17.22_d9b5fb0f.jpg](https://assets.leetcode.com/users/images/347a8816-dbbd-4f25-83a4-84d04fbe56b1_1714844872.2793221.jpeg)

![WhatsApp Image 2024-05-04 at 23.17.23_03b5a181.jpg](https://assets.leetcode.com/users/images/a22d99c3-09c7-4e8e-b2cd-61dddf202ecf_1714844860.783831.jpeg)

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
- is: inorderStart
- ie: inorderEnd
- ps: postorderStart
- pe: postorderEnd
*/
class Solution {
    TreeNode* constructBinaryTree(vector<int> &inorder, int is, int ie, vector<int> &postorder, int ps, int pe, map<int,int> &mpp){
        if(ps>pe || is>ie){
            return nullptr;
        }
        TreeNode* root=new TreeNode(postorder[pe]);
        int inRoot=mpp[postorder[pe]];
        int numsLeft=inRoot-is;

        root->left=constructBinaryTree(inorder,is,inRoot-1,postorder,ps,ps+numsLeft-1,mpp);
        root->right=constructBinaryTree(inorder,inRoot+1,ie,postorder,ps+numsLeft,pe-1,mpp);

        return root;
    }
public:
    TreeNode* buildTree(vector<int>& inorder, vector<int>& postorder) {
        if(inorder.size()!=postorder.size()){
            return nullptr;
        }
        map<int,int> mpp;
        for(int i=0;i<inorder.size();i++){
            mpp[inorder[i]]=i;
        }
        
        return constructBinaryTree(inorder,0,inorder.size()-1,postorder,0,postorder.size()-1,mpp);
    }
};
```


**Important Link**
1. **[Video Link](https://youtu.be/LgLRTaEMRVc?si=sLowSLnvSjB2WAm2)**
2. **[Solution Link](https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/solutions/5112274/optimized-approach-with-detailed-explanation-best-c-solution-striver-solution)**
3. **[For Detailed Solution](https://takeuforward.org/data-structure/construct-binary-tree-from-inorder-and-postorder-traversal/)**

