
**[Find Missing And Repeating](https://practice.geeksforgeeks.org/problems/find-missing-and-repeating2512/1)**

**Medium**

Given an unsorted array **Arr** of size **N** of positive integers. **One number 'A'** from set {1, 2,....,N} is missing and **one number 'B'** occurs twice in array. Find these two numbers.

**Example 1:**

**Input:**
```
N = 2
Arr[] = {2, 2}
Output: 2 1
Explanation: Repeating number is 2 and 
smallest positive missing number is 1.
```

**Example 2:**

**Input:**
```
N = 3
Arr[] = {1, 3, 3}
Output: 3 2
Explanation: Repeating number is 3 and 
smallest positive missing number is 2.
```

**Your Task:**  
You don't need to read input or print anything. Your task is to complete the function **findTwoElement()** which takes the array of integers **arr** and **n** as parameters and returns an array of integers of size 2 denoting the answer ( The first index contains **B** and second index contains **A.)**

**Expected Time Complexity:** O(N)  
**Expected Auxiliary Space:** O(1)

**Constraints:**  
2 ≤ N ≤ 105  
1 ≤ Arr[i] ≤ N


#### Brute Force Approach

#### Complexity

- Time complexity: O(n^2)
    
- Space complexity: O(1)


The steps are as follows:

1. We will run a loop(say i) from 1 to N.
2. For each integer, i, we will count its occurrence in the given array using linear search.
3. We will store those two elements that have the occurrence of 2 and 0.
4. Finally, we will return the elements.


#### Code

```cpp
// Brute Force Approach
// Time complexity -> O(n^2) and Space -> O(1)
class Solution{
public:
    vector<int> findTwoElement(vector<int> arr, int n) {
        // code here
        int repeating=-1,missing=-1;
        for(int i=1;i<=n;i++)
        {
            int count=0;
            for(int j=0;j<n;j++)
            {
                if(arr[j]==i)
                {
                    count++;
                }
            }
            if(count==2)
            {
                repeating=i;
            }
            if(count==0)
            {
                missing=i;
            }
            if(repeating!=-1 && missing!=-1)
            {
                break;
            }
        }
        return {repeating,missing};
    }
};
```


Above code ❌ give time limit Exceeded due to time complexity O(n^2)

![[WhatsApp Image 2023-07-11 at 17.03.43.jpg]]



#### Better Approach

#### Complexity

- Time complexity: O(2n)
    
- Space complexity: O(n)

The steps are as follows:

1. The range of the number is 1 to N. So, we need a hash array of size N+1 (_as we want to store the frequency of N as well_).
2. We will iterate all the elements of the given array and update the hash array accordingly i.e. hash[a[i]] = hash[a[i]]+1.
3. Now, we will iterate on the hash array and return the two elements with frequencies 2 and 0.

#### Code

```cpp
// Better Approach
// Time complexity -> O(2n) and Space -> O(n)
class Solution{
public:
    vector<int> findTwoElement(vector<int> arr, int n) {
        // code here
        int hash[n+1]={0};
        for(int i=0;i<n;i++)
        {
            hash[arr[i]]++;
        }
        int repeating=-1,missing=-1;
        for(int i=1;i<=n;i++)
        {
            if(hash[i]==2)
            {
                repeating=i;
            }
            if(hash[i]==0)
            {
                missing=i;
            }
            if(repeating!=-1 && missing!=-1)
            {
                break;
            }
        }
        return {repeating,missing};
    }
};
```


![[WhatsApp Image 2023-07-11 at 17.03.42.jpg]]



#### Optimized Approach

#### Complexity

- Time complexity:  O(n)
    
- Space complexity: O(1)

**Intuition:**

The idea is to convert the given problem into mathematical equations. Since we have two variables i.e. missing and repeating, we will try to form two linear equations. And then we will find the values of two variables using those equations.

Assume the repeating number to be X and the missing number to be Y.

In the array, the numbers are between 1 to N, and in that range, one number is missing and one number is occurring twice.

**Step 1: Form equation 1:**

Now, we know the summation of the first N numbers is:

Sn = (N*(N+1))/2

Let’s say, **S = the summation of all the elements in the given array**.

Therefore, S - Sn = X - Y…………………equation 1

**Step 2: Form equation 2:**

Now, we know the summation of squares of the first N numbers is:

S2n = (N*(N+1)*(2N+1))/6

Let’s say, **S2 = the summation of squares of all the elements in the given array**.

Therefore, S2-S2n = X2 - Y2...................equation 2

From equation 2 we can conclude,

X+Y = (S2 - S2n) / (X-Y)  ………… equation 3

From equation 1 and equation 3, we can easily find the value of X and Y. And this is what we want.

**Note:** _Here, we are summing all the numbers and squares of all the numbers, so we should use a bigger data type(Like in C++, long long instead of int)._



Assume the repeating number to be X and the missing number to be Y.

The steps are as follows:

1. First, find out the values of S and Sn and then calculate S – Sn (Using the above formulas).
2. Then, find out the values of S2 and S2n and then calculate S2 – S2n.
3. After performing steps 1 and 2, we will be having the values of X + Y and X – Y. Now, by substitution of values, we can easily find the values of X and Y.

#### Code

```cpp
// Optimized Approach
// Time complexity -> O(n) and Space -> O(1)
class Solution{
public:
    vector<int> findTwoElement(vector<int> arr, int n) {
        // code here
        
        // S - SN 
        // S2 - S2N
        long long len=arr.size();
        long long SN=(len * (len + 1))/2;
        long long S2N=(len * (len + 1) * (2 * len + 1)) / 6;
        
        long long S=0,S2=0;
        for(int i=0;i<len;i++)
        {
            S+=(long long)arr[i];
            S2+=(long long)arr[i] * (long long)arr[i];
        }
        
        long long val1=S-SN; // S-Sn = X-Y
        
        long long val2=S2-S2N; // S2-S2n = X^2-Y^2
        val2=val2/val1; // x + y
        
        long long x=(val1+val2)/2; // repeating number
        
        long long y=x-val1; // missing number
        
        return {(int)x,(int)y};
    }
};
```



![[WhatsApp Image 2023-07-11 at 17.03.42 1.jpg]]

![[WhatsApp Image 2023-07-11 at 17.03.43 1.jpg]]


**Important Link**
1. **[Video Link](https://youtu.be/2D0D8HE6uak)**

