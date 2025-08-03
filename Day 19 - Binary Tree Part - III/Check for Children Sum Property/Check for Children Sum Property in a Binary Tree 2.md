

**[Check for Children Sum Property in a Binary Tree](https://www.geeksforgeeks.org/problems/children-sum-parent/1)**

Given a binary tree having **n** nodes. Check whether all of its nodes have the value equal to the sum of their child nodes. Return 1 if all the nodes in the tree satisfy the given properties, else it return 0.

For every node, data value must be equal to the sum of data values in left and right children. Consider data value as 0 for NULL child.  Also, leaves are considered to follow the property.

**Example 1:**

**Input:  
```
Binary tree
        35
      /    \
     20     15  
    /  \   /  \  
   15  5  10    5
```
   
**Output:** 

```
1
```

**Explanation:** 

```
Here, every node is sum of its left and right child.
```


**Example 2:**

**Input:  
```
Binary tree
       1
     /   \
    4     3
   /  
  5    
```

**Output:** 
```
0
```

**Explanation:** 
```
Here, 1 is the root node and 4, 3 are its child nodes. 4 + 3 = 7 which is not equal to the value of root node. Hence, this tree does not satisfy the given condition.
```

**Your Task:**  
You don't need to read input or print anything. Your task is to complete the function **isSumProperty()** that takes the root Node of the binary tree as input and returns 1 if all the nodes in the tree satisfy the following properties, else it returns 0.

**Expected Time Complexiy:** O(n).  
**Expected Auxiliary Space:** O(Height of the Tree).

**Constraints:**  
1 <= n <= 105  
1 <= Data on nodes <= 10<sup>5</sup>

***


### Optimized Approach

### Complexity:
-  Time complexity: O(n)
    
-  Space complexity: O(h)

where n: number of nodes in binary tree and h: Height of the binary tree

#### Dry Run

![image](../../Screenshots/Check%20for%20Children%20Sum%20Property%20in%20a%20Binary%20Tree%208.jpg)

![image](../../Screenshots/Check%20for%20Children%20Sum%20Property%20in%20a%20Binary%20Tree%209.jpg)

![image](../../Screenshots/Check%20for%20Children%20Sum%20Property%20in%20a%20Binary%20Tree%2010.jpg)

![image](../../Screenshots/Check%20for%20Children%20Sum%20Property%20in%20a%20Binary%20Tree%2011.jpg)

![image](../../Screenshots/Check%20for%20Children%20Sum%20Property%20in%20a%20Binary%20Tree%2012.jpg)

![image](../../Screenshots/Check%20for%20Children%20Sum%20Property%20in%20a%20Binary%20Tree%2013.jpg)

![image](../../Screenshots/Check%20for%20Children%20Sum%20Property%20in%20a%20Binary%20Tree%2014.jpg)

![image](../../Screenshots/Check%20for%20Children%20Sum%20Property%20in%20a%20Binary%20Tree%2015.jpg)

![image](../../Screenshots/Check%20for%20Children%20Sum%20Property%20in%20a%20Binary%20Tree%2016.jpg)

![image](../../Screenshots/Check%20for%20Children%20Sum%20Property%20in%20a%20Binary%20Tree%2017.jpg)

![image](../../Screenshots/Check%20for%20Children%20Sum%20Property%20in%20a%20Binary%20Tree%2018.jpg)

![image](../../Screenshots/Check%20for%20Children%20Sum%20Property%20in%20a%20Binary%20Tree%2019.jpg)

![image](../../Screenshots/Check%20for%20Children%20Sum%20Property%20in%20a%20Binary%20Tree%2020.jpg)

![image](../../Screenshots/Check%20for%20Children%20Sum%20Property%20in%20a%20Binary%20Tree%2021.jpg)



### Code
```cpp
// Optimized Approach
// Time complexity -> O(n) and Space -> O(h)
// where n: number of nodes in a binary tree and h: height of the binary tree
class Solution{
    public:
    //Function to check whether all nodes of a tree have the value 
    //equal to the sum of their child nodes.
    int isSumProperty(Node *root)
    {
        // Add your code here
        if(root==nullptr || (root->left==nullptr && root->right==nullptr)){
            return 1;
        }
        int sum=0;
        if(root->left!=nullptr){
            sum+=root->left->data;
        }
        if(root->right!=nullptr){
            sum+=root->right->data;
        }
        return (root->data==sum && isSumProperty(root->left) && isSumProperty(root->right));
    }
};
```

