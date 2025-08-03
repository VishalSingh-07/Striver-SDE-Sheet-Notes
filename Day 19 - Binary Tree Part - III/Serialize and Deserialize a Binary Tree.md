
**[Serialize and Deserialize Binary Tree](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/)**

Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.

Design an algorithm to serialize and deserialize a binary tree. There is no restriction on how your serialization/deserialization algorithm should work. You just need to ensure that a binary tree can be serialized to a string and this string can be deserialized to the original tree structure.

**Clarification:** The input/output format is the same as [how LeetCode serializes a binary tree](https://support.leetcode.com/hc/en-us/articles/360011883654-What-does-1-null-2-3-mean-in-binary-tree-representation-). You do not necessarily need to follow this format, so please be creative and come up with different approaches yourself.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/09/15/serdeser.jpg)

```
Input: root = [1,2,3,null,null,4,5]
Output: [1,2,3,null,null,4,5]
```

**Example 2:**

```
Input: root = []
Output: []
```

**Constraints:**

- The number of nodes in the tree is in the range `[0, 104]`.
- `-1000 <= Node.val <= 1000`

***
### Examples

**Example 1:**

```sql
Input: 
Binary Tree: 1 2 3 -1 -1 4 5

Output: 
After Serialisation: 1,2,3,#,#,4,5,#,#,#,#, 
After Deserialization: (Original Tree Back)

Explanation: 
Any algorithm that compresses this binary tree to a 
string which can be transmitted and from which the 
binary tree can be reconstructed later can be used.
Here we have used a serialisation algorithm based 
on level order traversal where comma separates 
the nodes and # denotes null nodes.
```

![image.png](https://assets.leetcode.com/users/images/6504efa8-4657-41c3-9ed1-cbceb6691f64_1714648402.4909596.png)

![image.png](https://assets.leetcode.com/users/images/6838940d-6127-415a-bdc0-f810f4349725_1714648547.844048.png)

**Example 2:**

```sql
Input: 
Binary Tree: 1 2 3 -1 4 5 -1

Output: 
After Serialisation: 1,2,3,#,4,5,#, 
After Deserialization: (Original Tree Back)

Explanation: 
Any algorithm that compresses this binary tree to 
a string which can be transmitted and from which 
the binary tree can be reconstructed 
later can be used.
Here we have used a serialisation algorithm based 
on level order traversal where comma separates 
the nodes and # denotes null nodes. 
```

![image.png](https://assets.leetcode.com/users/images/87ca36b2-8f46-4228-a46c-85de3b587357_1714648643.485472.png)

![image.png](https://assets.leetcode.com/users/images/418329c3-2b40-478d-93ee-280765338878_1714648648.9291496.png)

---

### Optimized Approach

### Complexity

- Time complexity: O(n)
    
    - **serialize function:** O(n), where n is the number of nodes in the tree. This is because the function performs a level-order traversal of the tree, visiting each node once.
    - **deserialize function:** O(n), where n is the number of nodes in the tree. Similar to the serialize function, it processes each node once while reconstructing the tree.
- Space complexity: O(n)
    
    - **serialize function:** O(n), where n is the maximum number of nodes at any level in the tree. In the worst case, the queue can hold all nodes at the last level of the tree.
    - **deserialize function:** O(n), where n is the maximum number of nodes at any level in the tree. The queue is used to store nodes during the reconstruction process, and in the worst case, it may hold all nodes at the last level.

#### Algorithm

##### Serialization:

**Step 1:**  Check if the tree is empty: If the root is null, return an empty string.

**Step 2:** Initialize an empty string: This string will store the serialized binary tree.

**Step 3:** Use a queue for level-order traversal: Initialize a queue and enqueue the root.

![image.png](https://assets.leetcode.com/users/images/655d5ac7-9e43-4fed-ac90-f03960a1c704_1714648213.5512915.png)

**Step 4:** Within the level-order traversal loop:

1. Dequeue a node from the queue.
2. If the node is null, append "#" to the string.
3. If the node is not null, append its data value along with a ‘,’ (comma) to the string. This comma acts as a delimiter that separates the different node values in the string. Enqueue its left and right children.

![image.png](https://assets.leetcode.com/users/images/733bfa6f-af80-4fb5-857b-b8ba2724c95c_1714648227.0597773.png)

**Step 5:** Return the final string containing the serialised representation of the tree.

##### Deserialization:

**Step 1:** Check if the serialised data is empty: If it is, return null.

**Step 2:** Tokenize the serialised data: Use a stringstream to tokenize the input string using the comma as a delimiter.

**Step 3:** Read the root value: Read the first token and create the root node with this value.

**Step 4:** Use a queue for level-order traversal: Initialise a queue and enqueue the root.

![image.png](https://assets.leetcode.com/users/images/ad3cbc4f-a9e6-42ba-ada8-c151023ff6f0_1714648241.1959622.png)

**Step 5:** Within the level-order traversal loop:

1. Dequeue a node from the queue.
2. Read the value for the left child from the stringstream.
3. If it is "#", set the left child to null. If it's not "#", create a new node with the value and set it as the left child.
4. Read the next value in the stringstream for the right child.
5. If it is "#", set the right child to null. If it's not "#", create a new node with the value and set it as the right child.
6. Enqueue the left and right children into the queue for further traversal.

![image.png](https://assets.leetcode.com/users/images/dc0d9d85-382c-462b-9b9d-cdc4e309865a_1714648253.3188632.png)

**Step 6:** Return the reconstructed root: The final result is the root of the reconstructed tree.

![WhatsApp Image 2024-05-02 at 16.37.36_ac687ced.jpg](https://assets.leetcode.com/users/images/df260420-b89f-4766-8351-e1fec666c065_1714648127.016635.jpeg)

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

// Optimized Approach
// Time Complexity: O(n) and Space Complexity: O(n)

 
class Codec {
public:

    // Encodes a tree to a single string.
    string serialize(TreeNode* root) {
        // Check if the tree is empty
        if(root==nullptr){
            return "";
        }
        // Initialize an empty string to store the serialized data
        string s="";
        // Use a queue for level-order traversal
        queue<TreeNode*> q;
        // Start with the root node
        q.push(root);

        // Perform level-order traversal
        while(!q.empty()){
            // Get the front node in the queue
            TreeNode*  currNode=q.front();
            q.pop();
            // Check if the current node is null and append "#" to the string
            if(currNode==nullptr){
                s.append("#,");
            }else{
                // Append the value of the current node to the string
                s.append(to_string(currNode->val) + ",");
            }
            if(currNode!=nullptr){
                // Push the left and right children to the queue for further traversal
                q.push(currNode->left);
                q.push(currNode->right);
            }
        }
        return s;
        
    }

    // Decodes your encoded data to tree.
    TreeNode* deserialize(string data) {
        // Check if the serialized data is empty
        if(data.size()==0){
            return nullptr;
        }

        // Use a stringstream to tokenize the serialized data
        stringstream s(data);
        string str;

        // Read the root value from the serialized data
        getline(s, str, ',');
        TreeNode *root=new TreeNode(stoi(str));
        // Use a queue for level-order traversal
        queue<TreeNode*> q;
        // Start with the root node
        q.push(root);

        // Perform level-order traversal to reconstruct the tree
        while(!q.empty()){
            // Get the front node in the queue
            TreeNode *currNode=q.front();
            q.pop();

            // Read the value of the left child from the serialized data
            getline(s, str, ',');
            if(str == "#"){
                currNode->left=nullptr;
            }
            else{
                TreeNode *leftNode=new TreeNode(stoi(str));
                currNode->left=leftNode;
                q.push(leftNode);
            }

            // Read the value of the right child from the serialized data
            getline(s, str, ',');
            if(str=="#"){
                currNode->right=nullptr;
            }
            else{
                TreeNode *rightNode=new TreeNode(stoi(str));
                currNode->right=rightNode;
                q.push(rightNode);
            }
        }
        // Return the reconstructed root of the tree
        return root;
    }
};

// Your Codec object will be instantiated and called as such:
// Codec ser, deser;
// TreeNode* ans = deser.deserialize(ser.serialize(root));
```


**Important Link**
1. **[Video Link ](https://youtu.be/-YbXySKJsX8)**
2. **[Solution Link](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/solutions/5101078/optimized-approach-with-explanation-best-c-solution-striver-solutio)**
3. **[For Detailed Solution](https://takeuforward.org/data-structure/serialize-and-deserialize-a-binary-tree/)**
