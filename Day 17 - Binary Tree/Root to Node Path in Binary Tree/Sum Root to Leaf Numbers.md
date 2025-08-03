
**[Sum Root to Leaf Numbers](https://leetcode.com/problems/sum-root-to-leaf-numbers/)**

You are given the `root` of a binary tree containing digits from `0` to `9` only.

Each root-to-leaf path in the tree represents a number.

- For example, the root-to-leaf path `1 -> 2 -> 3` represents the number `123`.

Return _the total sum of all root-to-leaf numbers_. Test cases are generated so that the answer will fit in a **32-bit** integer.

A **leaf** node is a node with no children.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/num1tree.jpg)

**Input:** 
```
root = [1,2,3]
```

**Output:** 
```
25
```

**Explanation:**
```
The root-to-leaf path 1->2 represents the number 12.
The root-to-leaf path 1->3 represents the number 13.
Therefore, sum = 12 + 13 = 25.
```

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/02/19/num2tree.jpg)

**Input:** 
```
root = [4,9,0,5,1]
```

**Output:** 
```
1026
```

**Explanation:**
```
The root-to-leaf path  4->9->5  represents the number 495.
The root-to-leaf path  4->9->1  represents the number 491.
The root-to-leaf path  4->0  represents the number 40.
Therefore, sum = 495 + 491 + 40 = `1026`.
```

**Constraints:**

- The number of nodes in the tree is in the range `[1, 1000]`.
- `0 <= Node.val <= 9`
- The depth of the tree will not exceed `10`.


***
### Optimized Approach

### Complexity

- Time complexity: O(n)
    
- Space complexity: O(h)
    

where n: number of nodes in a binary tree and h: the height of the binary tree

#### Algorithm

1. Initialize a variable `totalSum` to store the sum of all numbers formed by root-to-leaf paths.
2. Define a recursive function `findAllPaths` that takes three parameters:
    - `root`: pointer to the current node being traversed.
    - `path`: reference to a string representing the current path from the root to the current node.
    - `totalSum`: reference to the total sum.
3. In the `findAllPaths` function:  
    a. If the current node `root` is nullptr, return.  
    b. Append the string representation of the value of the current node `root->val` to the `path`.  
    c. If the current node is a leaf node (i.e., it has no left or right children), convert the `path` to an integer and add it to the `totalSum`.  
    d. Recursively call `findAllPaths` for the left child of the current node.  
    e. Recursively call `findAllPaths` for the right child of the current node.  
    f. Backtrack by removing the last character from the `path`.
4. Call the `findAllPaths` function with the root node, an empty string `path`, and `totalSum` initialized to 0.
5. Return the `totalSum`.

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
// Time complexity -> O(n) and Space -> O(h)
// Where n: number of nodes in binary Tree
class Solution {
    void findAllPaths(TreeNode *root, string &path,int &totalSum){
        if(root==nullptr){
            return;
        }
        path+=to_string(root->val);
        if(root->left==nullptr && root->right==nullptr){
            totalSum+=stoi(path);
        }
        findAllPaths(root->left,path,totalSum);
        findAllPaths(root->right,path,totalSum);
        path.pop_back();
    }
public:
    int sumNumbers(TreeNode* root) {
        int totalSum=0;
        string path="";
        findAllPaths(root,path,totalSum);
        return totalSum;
    }
};
```

### OR

#### Algorithm

1. Initialize a variable `res` to store the total sum of all root-to-leaf paths.
2. Define a recursive function `totalSum` that takes three parameters:
    - `root`: pointer to the current node being traversed.
    - `currSum`: integer representing the current sum formed by the root-to-current node path.
    - `res`: reference to the total sum.
3. In the `totalSum` function:  
    a. If the current node `root` is a leaf node (i.e., it has no left or right children), calculate the sum formed by the root-to-leaf path by multiplying the `currSum` by 10 and adding the value of the current node `root->val`. Then, add this sum to the `res`.  
    b. If the current node has a left child, recursively call `totalSum` for the left child, passing the updated `currSum`.  
    c. If the current node has a right child, recursively call `totalSum` for the right child, passing the updated `currSum`.
4. Call the `totalSum` function with the root node, an initial `currSum` of 0, and the reference to `res`.
5. Return the value of `res`, which contains the total sum of all root-to-leaf paths.

```cpp
class Solution {
    void totalSum(TreeNode *root, int currSum,int &res){
        if(root->left==nullptr && root->right==nullptr){
            currSum=currSum*10+root->val;
            res+=currSum;
            return;
        }
        currSum=currSum*10+root->val;
        if(root->left!=nullptr){
            totalSum(root->left,currSum,res);
        }
        if(root->right!=nullptr){
            totalSum(root->right,currSum,res);
        }
    }
public:
    int sumNumbers(TreeNode* root) {
        int res=0;
        totalSum(root,0,res);
        return res;
    }
};
```

***

**Important Link**
1. **[Solution Link](https://leetcode.com/problems/sum-root-to-leaf-numbers/solutions/4958455/optimized-approach-with-explanation-best-c-solution-beats-100-00-of-users-with-c)**


