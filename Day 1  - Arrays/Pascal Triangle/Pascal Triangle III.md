

**Variation 1:** Given row number r and column number c. Print the element at position (r, c) in Pascal’s triangle.


In this case, we are given the row number r and the column number c, and we need to find out the element at position (r,c). 

##### Naïve Approach

In this case, we are given the row number r and the column number c, and we need to find out the element at position (r,c). 

**_One of the Naive approaches_** is to generate the entire Pascal triangle and then find the element at position (r,c). We will discuss in variation 3 how to generate Pascal’s triangle.

We have an easier formula to find out the element i.e. r-1Cc-1. Let’s try to analyze the formula to find the value of the combination assuming r-1 as n and c-1 as r:

nCr = n! / (r! * (n-r)!)

**Calculating the value of nCr:**

**Naive Approach:** 

We can separately calculate n!, r!, (n-r)! and using their values we can calculate nCr. This is an extremely naive way to calculate. The time complexity will be O(n)+O(r)+O(n-r).



##### Optimal Approach

Algorithm / Intuition

```
We can optimize this calculation by the following observation. 
Assume, given r = 7, c = 4. 
Now, n = r-1 = 7-1 = 6 and r = c-1 = 4-1 = 3
Let’s calculate 6C3 = 6! / (3! *(6-3)!) = (6*5*4*3*2*1) / ((3*2*1)*(3*2*1))
This will boil down to (6*5*4) / (3*2*1)
So, nCr = (n*(n-1)*(n-2)*.....*(n-r+1)) / (r*(r-1)*(r-2)*....1)
```


Now, we will use this optimized formula to calculate the value of nCr. But while implementing this into code we will take the denominator in the forward direction like

```
(n / 1)*((n-1) / 2)*.....*((n-r+1) / r).
```


The code will be like the following:
![](https://takeuforward.org/wp-content/uploads/2023/04/Screenshot-2023-04-30-210349.png)


#### **Approach:**

The steps are as follows:

1. First, we will consider r-1 as n and c-1 as r.
2. After that, we will simply calculate the value of the combination using a loop. 
3. The loop will run from 0 to r. And in each iteration, we will multiply (n-i) with the result and divide the result by (i+1).
4. Finally, the calculated value of the combination will be our answer.


#### Code

```cpp

#include <bits/stdc++.h>
using namespace std;

int nCr(int n, int r) {
    long long res = 1;

    // calculating nCr:
    for (int i = 0; i < r; i++) {
        res = res * (n - i);
        res = res / (i + 1);
    }
    return res;
}

int pascalTriangle(int r, int c) {
    int element = nCr(r - 1, c - 1);
    return element;
}

int main()
{
    int r = 5; // row number
    int c = 3; // col number
    int element = pascalTriangle(r, c);
    cout << "The element at position (r,c) is: "
            << element << "n";
    return 0;
}
        
```

**Output:** The element at position (r, c) is: 6


Complexity Analysis

**Time Complexity:** O(c), where c = given column number.  
**Reason:** We are running a loop for r times, where r is c-1.

**Space Complexity:** O(1) as we are not using any extra space.



**[Video Link](https://youtu.be/bR7mQgwQ_o8)**


