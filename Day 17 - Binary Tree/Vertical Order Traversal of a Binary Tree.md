
**[Vertical Order Traversal of a Binary Tree](https://leetcode.com/problems/vertical-order-traversal-of-a-binary-tree/description/)**

Given the `root` of a binary tree, calculate the **vertical order traversal** of the binary tree.

For each node at position `(row, col)`, its left and right children will be at positions `(row + 1, col - 1)` and `(row + 1, col + 1)` respectively. The root of the tree is at `(0, 0)`.

The **vertical order traversal** of a binary tree is a list of top-to-bottom orderings for each column index starting from the leftmost column and ending on the rightmost column. There may be multiple nodes in the same row and same column. In such a case, sort these nodes by their values.

Return _the **vertical order traversal** of the binary tree_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/01/29/vtree1.jpg)

```
Input: root = [3,9,20,null,null,15,7]
Output: [[9],[3,15],[20],[7]]
Explanation:
Column -1: Only node 9 is in this column.
Column 0: Nodes 3 and 15 are in this column in that order from top to bottom.
Column 1: Only node 20 is in this column.
Column 2: Only node 7 is in this column.
```

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/01/29/vtree2.jpg)

```
Input: root = [1,2,3,4,5,6,7]
Output: [[4],[2],[1,5,6],[3],[7]]
Explanation:
Column -2: Only node 4 is in this column.
Column -1: Only node 2 is in this column.
Column 0: Nodes 1, 5, and 6 are in this column.
          1 is at the top, so it comes first.
          5 and 6 are at the same position (2, 0), so we order them by their value, 5 before 6.
Column 1: Only node 3 is in this column.
Column 2: Only node 7 is in this column.`
```

**Example 3:**

![](https://assets.leetcode.com/uploads/2021/01/29/vtree3.jpg)

```
Input: root = [1,2,3,4,6,5,7]
Output: [[4],[2],[1,5,6],[3],[7]]
Explanation:
This case is the exact same as example 2, but with nodes 5 and 6 swapped.
Note that the solution remains the same since 5 and 6 are in the same location and should be ordered by their values.
```

**Constraints:**

- The number of nodes in the tree is in the range `[1, 1000]`.
- `0 <= Node.val <= 1000`

#### Optimized Approach

### Complexity

- Time complexity: O(nlogn)
    
- Space complexity: O(n)
    

where n: number of nodes in a binary tree

#### Steps: 

We will perform a tree traversal and assign a vertical and level to every node. Based on this vertical and node, we store the node in our special data structure. For easy understanding, we break it into these steps:

**Step-1: Assigning vertical and level to every node**

We can perform any tree traversal for this step. Here we are taking the example of level order traversal. In the initial step when we push the node to our queue, we will push two more variables to it, one for the vertical and one for the level (both initialized as zero). Now whenever we push the left child of the node, we decrease vertical by 1 and increase level by 1, whereas whenever we push the right child of the node, we increase both vertical and level by one.

![image.png](https://assets.leetcode.com/users/images/485e9486-abc6-4c22-a7c2-f36663d0f25e_1710438862.5338988.png)

Verticals and levels will be marked as follows:

![image.png](https://assets.leetcode.com/users/images/72e7f4dd-d617-44da-89e1-8446616553cd_1710438876.3097606.png)

**Step-2: Storing Verticals and levels to our data structure**

When we are assigning the verticals and levels, it is very important to store them in a suitable data structure. After assigning we have:

![image.png](https://assets.leetcode.com/users/images/86d06802-3ea5-47f4-9bf2-8eca6467df66_1710438892.4422107.png)

In the vertical order traversal, we need to print the nodes of the left vertical first, therefore in our example, nodes of -2 vertical will be the first to  be printed. Therefore, we need a data structure that can store nodes according to their vertical value and give us the nodes of least values first. Hence we will use a **map** as it satisfies both criterias.

![image.png](https://assets.leetcode.com/users/images/61f5ac8e-7844-4008-8808-02b2ca5cd291_1710438907.8589835.png)

Now, we will explore X. In a single vertical we want to get the nodes by their levels. In our example, vertical 0 has nodes of three different levels, we will print level 0 first (node 1), then level 2 (node 9 and 10) and at last level 4 (node 6). Therefore as in the case of our verticals, we will again use **map** to store nodes level-wise inside the vertical. So, our data structure will become:

image.png  
![image.png](https://assets.leetcode.com/users/images/59318bbe-7eda-4929-ad5d-994c37e516f8_1710438922.791877.png)

Now, we will explore Y. There can be a case that two or more nodes overlap at the same vertical and level, as with case of node 9 and node 10 at vertical 0 and level 2. In such a case we will print nodes with lesser value first. Therefore for every level, we need a data-structure which can store node values in a sorted order. Moreover, as duplicate values are allowed in our tree, our data structure needs to handle this well. This is acheived by using [**multiset**](https://www.cplusplus.com/reference/set/multiset/) **in C++**. Multiset is similar to a set which keeps elements in sorted order but also allows duplicates. **In Java**, we can use **priority queues** as it gives us the minimum value at the top.

Therefore, our final data structure will be:

![image.png](https://assets.leetcode.com/users/images/9c72a601-1fbf-4568-9eb7-fff131337e32_1710439361.151118.png)

**Note:** This is not the only choice for the data structure. You are free to choose any other data structure as well but the requirements remain the same. Instead of a multiset/priority queue, simple lists can also be used but then we will need to sort them in our last step.

**Step 3: Printing vertical order traversal from our data structure**

In the last step, we iterate over our verticals by using the data structure of step 2. In every iteration, we take a list(to store all nodes of that vertical) and again iterate over the levels. We then push the nodes of the level (stored in the multiset/priority queue) and push it to our vertical list. Once we iterate over all verticals we get our vertical order traversal.

![image.png](https://assets.leetcode.com/users/images/0c4dea07-198a-488f-88c7-23f56cd97934_1710438714.7737315.png)


![image.png](https://assets.leetcode.com/users/images/5f6f663d-5e76-4032-83e9-97a3c5ad42d0_1710438702.9843607.png)

```cpp
Remember :

1. For left child -> {vertical-1,level+1}
2. For right child -> {vertical+1,level+1}

where vertical: columns and level: rows


    This int is for storing verticals
     ^
     |
map<int,map<int,multiset<int>>> mpp:

    
        This int is for level 
         ^
         |
    map<int,multiset<int>>
                |
                This multiset is used for multinode on same level as well as same vertical
```

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
// Time complexity -> O(nlogn) and Space -> O(n)
// where n: number of nodes in a binary tree
class Solution {
public:
    vector<vector<int>> verticalTraversal(TreeNode* root) {
        vector<vector<int>> ans;
        if(root==nullptr){
            return ans;
        }
        map<int,map<int,multiset<int>>> mpp;
        queue<pair<TreeNode*,pair<int,int>>> q;
        q.push({root,{0,0}}); // q.push({root,{verticals,levels}})
        while(!q.empty()){
            auto it=q.front();
            q.pop();
            TreeNode* node=it.first;
            int vertical=it.second.first,level=it.second.second;
            mpp[vertical][level].insert(node->val);
            if(node->left!=nullptr){
                q.push({node->left,{vertical-1,level+1}});
            }
            if(node->right!=nullptr){
                q.push({node->right,{vertical+1,level+1}});
            }
        }

        // where p.first=int and p.second=map<int,multiset<int>>
        for(auto p: mpp){
            vector<int> col;
            for(auto q: p.second){
                // q.first -> int and q.second -> multiset<int>
                col.insert(col.end(),q.second.begin(),q.second.end());
            }
            ans.push_back(col);
        }
        return ans; 
    }
};
```


**Important Link**
1. **[Solution Link](https://leetcode.com/problems/vertical-order-traversal-of-a-binary-tree/solutions/4876004/beats-100-00-of-users-with-c-easy-c-solution-optimized-approach-with-explanation)**
2. **[Video Link](https://youtu.be/q_a6lpbKJdw)**
3. **[For Detailed Solution](https://takeuforward.org/data-structure/vertical-order-traversal-of-binary-tree/)**
