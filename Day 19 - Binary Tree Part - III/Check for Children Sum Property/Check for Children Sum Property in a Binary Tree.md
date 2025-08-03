

**Problem Statement:** 

Given a Binary Tree, convert the value of its nodes to follow the Children Sum Property. The Children Sum Property in a binary tree states that for every node, the sum of its children's values (if they exist) should be equal to the node's value. If a child is missing, it is considered as having a value of 0.

**Note:**
1. The node values can be increased by any positive integer any number of times, but decrementing any node value is not allowed.
2. A value for a NULL node can be assumed as 0.
3. We cannot change the structure of the given binary tree.

***

**[Check for Children Sum Property in a Binary Tree](https://www.naukri.com/code360/problems/childrensumproperty_790723)**
## Problem statement

Given a binary tree of nodes 'N', you need to modify the value of its nodes, such that the tree holds the Children sum property.

A binary tree is said to follow the children sum property if, for every node of that tree, the value of that node is equal to the sum of the value(s) of all of its children nodes( left child and the right child).

**Note :**
1.  You can only increment the value of the nodes, in other words, the modified value must be at least equal to the original value of that node.
 2. You can not change the structure of the original binary tree.
 3. A binary tree is a tree in which each node has at most two children.      
 4. You can assume the value can be 0 for a NULL node and there can also be an empty tree.


**Constraints :**

```
1 <= T <= 10^2
0 <= N <= 10^2
1 <= node.Value <= 10^6

Time Limit : 1 sec
```

**Sample Input 1 :**

```
1
2 35 10 2 3 5 2 -1 -1 -1 -1 -1 -1 -1 -1 
```

![image](../../Screenshots/Check%20for%20Children%20Sum%20Property%20in%20a%20Binary%20Tree%201.png)

**Sample Output 1 :**

```
Valid ( One of the possible answers is : 45 35 10 32 3 8 2 -1 -1 -1 -1 -1, thus if the user modifies the given tree like this, the output printed will be valid).
```

**Explanation For Sample Input 1 :**

```
The tree can be represented as follows :
```

![altimage](https://files.codingninjas.in/screenshot-from-2020-10-09-12-55-59-5133.png)

```
The value at the root node is 2 which is less than the sum of its children’s values (35 + 10). So we simply increase the value at the root node to 45. The node with value  = 35 has children with values 2 and 3 so their sum i.s 2 + 3 = 5 < 35. As we can't decrement any value, so instead we have to increase the sum of children and thus we update 35's children (2 and 3) as 30 and 5 so that 30 + 5 = 35 and the same is done for the children of the node with value = 10.
```

**The final tree looks like this :**

![altimage](https://files.codingninjas.in/screenshot-from-2020-10-09-12-56-05-5132.png)

```
Note that there can be many other valid solutions.
```

**Sample Input 2 :**

```
1
10 5 5 -1 -1 -1 -1
```

**Sample Output 2 :**

```
Valid
```

****

### Optimized Approach

### Complexity:
-  Time complexity: O(n)
    
-  Space complexity: O(h)

where n: number of nodes in binary tree and h: Height of the binary tree


#### Intuition:

The constraint is that we cannot decrease the value of any node, only increase it. Also, the structure of the binary tree cannot be changed. If we follow a bottom-up approach and try to adjust parent values based on children, we may reach a situation where the sum of children exceeds the parent's value, requiring us to decrease the parent's value, which is not allowed.

![image](../../Screenshots/Check%20for%20Children%20Sum%20Property%20in%20a%20Binary%20Tree%202.png)

With just a bottom-up approach, we cannot guarantee that the Children Sum Property will be satisfied at each level. It might work for some cases but not for all. There's no clear strategy to ensure that the property holds true for the entire tree. A key insight here is that there's no restriction on how much we can increase the value of each node. Hence, we have the flexibility to adjust the values as needed to ensure that the Children Sum Property holds true at every node in the tree.

![image](../../Screenshots/Check%20for%20Children%20Sum%20Property%20in%20a%20Binary%20Tree%203.png)

This means that if the sum of the values of a node's children is less than the node's value, we can simply increase the values of the children (and potentially the grandchildren and so on) until the property is satisfied. Using recursive calls, we traverse the binary tree, addressing each node and its children iteratively. At each step, we calculate the sum of the children's values and compare it with the parent node's value.

#### Algorithm:

**Step 1: Base Case**Start by checking if we've reached the end of a branch in the tree. If the current node is null, simply return.

**Step 2: Calculate Children Sum:** For each non-null node, calculate the sum of the values of its left and right children, if they exist. Add up the values of the left and right children (if they are not null) and store this sum in a variable called child.

**Step 3: Comparison and Value Update:** Compare the sum of the children (child) with the current node's value.

![image](../../Screenshots/Check%20for%20Children%20Sum%20Property%20in%20a%20Binary%20Tree%204.png)

If the sum of children is greater than or equal to the current node's value, we update the value of the parent to the sum of the children.

![image](../../Screenshots/Check%20for%20Children%20Sum%20Property%20in%20a%20Binary%20Tree%205.png)

If the sum of children is smaller than the current node's value, we need to make an adjustment to ensure the property holds. However, remember that we cannot decrease the value of any node. So, instead, we update one of the children's values to match the current node's value.

**Step 4: Recursive Calls:** For each node in the current level: After handling the current node, we recursively call the function on the left and right children of the current node.

**Step 5: Update Current Node's Value:** Once both children have been processed, we recalculate the total sum of the values of the left and right children and update the current node’s value to match the total sum of its children.

![image](../../Screenshots/Check%20for%20Children%20Sum%20Property%20in%20a%20Binary%20Tree%206.jpg)


![image](../../Screenshots/Check%20for%20Children%20Sum%20Property%20in%20a%20Binary%20Tree%207.jpg)

### Code 
```cpp
// Optimized Approach
// Time complexity -> O(n) and Space -> O(h)
// where n: number of nodes in binary tree and h: Height of the binary tree
void changeTree(BinaryTreeNode < int > * root) {
    // Write your code here.
    //  Base case: If the current node is NULL, return and do nothing.
    if(root==nullptr){
        return;
    }
    // Calculate the sum of the values of
    // the left and right children, if they exist.
    int child=0;
    if(root->left!=nullptr){
        child+=root->left->data;
    }
    if(root->right!=nullptr){
        child+=root->right->data;
    }
    // Compare the sum of children with
    // the current node's value and update
    if(child>=root->data){
        root->data=child;
    }else{
        // If the sum is smaller, update the
        // child with the current node's value.
        if(root->left!=nullptr){
            root->left->data=root->data;
        }
        else if(root->right!=nullptr){
            root->right->data=root->data;
        }
    }
    
    // Recursively call the function
    // on the left and right children.
    changeTree(root->left);
    changeTree(root->right);
    // Calculate the total sum of the
    // values of the left and right
    // children, if they exist.
    int tot=0;
    if(root->left!=nullptr){
        tot+=root->left->data;
    }
    if(root->right!=nullptr){
        tot+=root->right->data;
    }
    // If either left or right child
    // exists, update the current node's
     // value with the total sum.
    if(root->left!=nullptr || root->right!=nullptr){
        root->data=tot;
    }
}
```


##### Important Links
1. **[Video Link](https://youtu.be/fnmisPM6cVo)**



