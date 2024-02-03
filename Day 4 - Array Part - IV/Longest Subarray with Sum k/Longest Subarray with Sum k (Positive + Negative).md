### CodeStudio

[**Longest Subarray with Sum k**](https://www.codingninjas.com/studio/problems/longest-subarray-with-sum-k_5713505)  **Array contain positive and Negative integer**


**Problem statement**


Ninja and his friend are playing a game of subarrays. They have an array ‘NUMS’ of length ‘N’. Ninja’s friend gives him an arbitrary integer ‘K’ and asks him to find the length of the longest subarray in which the sum of elements is equal to ‘K’.

Ninjas asks for your help to win this game. Find the length of the longest subarray in which the sum of elements is equal to ‘K’.

If there is no subarray whose sum is ‘K’ then you should return 0.

**Example:**

```
Input: ‘N’ = 5,  ‘K’ = 4, ‘NUMS’ = [ 1, 2, 1, 0, 1 ]

Output: 4

There are two subarrays with sum = 4, [1, 2, 1] and [2, 1, 0, 1]. Hence the length of the longest subarray with sum = 4 is 4.
```


**Constraints :**

```
1 <= T <= 10
1 <= N <= 10^5
-10^6 <= NUMS[ i ] <= 10^6
-10^6 <= K <= 10^6

Sum of N Over all the Test cases <= 10^5

Time Limit: 1 sec
```

**Sample Input 1 :**

```
2
3 5
2 3 5
3 1
-1 1 1
```

**Sample Output 1 :**

```
2
3
```

**Explanation Of Sample Input 1 :**

```
For the first case:
There are two subarrays with sum = 5, [2, 3] and [5]. Hence the length of the longest subarray is 2.

For the second case:
Longest subarray with sum = 1 is [1, -1, 1].
```

**Sample Input 2 :**

```
2
3 4
1 1 1
3 2
-50 0 52
```

**Sample Output 2 :**

```
0 
3
```

### Approach 1: Brute Force Approach

### Complexity

- Time complexity: O(n^3)
    
- Space complexity: O(1)
    

##### **Approach:**

The steps are as follows:

1. First, we will run a loop(say i) that will select every possible starting index of the subarray. The possible starting indices can vary from index 0 to index n-1(n = size of the array).
2. Inside the loop, we will run another loop(say j) that will signify the ending index of the subarray. For every subarray starting from the index i, the possible ending index can vary from index i to n-1(n = size of the array).
3. After that for each subarray starting from index i and ending at index j **(i.e. arr[i….j]),** we will run another loop to calculate the sum of all the elements(of that particular subarray).
4. If the sum is equal to k, we will consider its length i.e. (j-i+1). Among all such subarrays, we will consider the maximum length by comparing all the lengths.


![alt text](../../Screenshots/Longest%20Subarray%20with%20Sum%20k%20(Positive)_1.jpg)

![alt text](../../Screenshots/Longest%20Subarray%20with%20Sum%20k%20(Positive)_2.jpg)

### Code

```cpp
// Brute Force Approach
// Time complexity -> O(n^3) and Space -> O(1)
int getLongestSubarray(vector<int>& nums, int k){
    // Write your code here
    int n=nums.size();
    int maxLen=0;
    for(int i=0;i<n;i++)
    {
        for(int j=i;j<n;j++)
        {
            long long sum=0;
            for(int k=i;k<=j;k++)
            {
                sum+=nums[k];
            }
            if(sum==k)
            {
                maxLen=max(maxLen,j-i+1);
            }
        }
    }
    return maxLen;
    
}

// Above code give Time Limit Exceeded due to High Complexity O(n^3)
```



### Approach 2: Better Approach

### Complexity

- Time complexity: O(n^2)
    
- Space complexity: O(1)


##### **Approach:**

The steps are as follows:

1. First, we will run a loop(_say i_) that will select every possible starting index of the subarray. The possible starting indices can vary from index 0 to index n-1(n = array size).
2. Inside the loop, we will run another loop(say j) that will signify the ending index as well as the current element of the subarray. For every subarray starting from the index i, the possible ending index can vary from index i to n-1(n = size of the array).
3. Inside loop j, we will add the current element to the sum of the previous subarray i.e. **sum = sum + arr[j]**. 
4. If the sum is equal to k, we will consider its length i.e. (j-i+1). Among all such subarrays with sum k, we will consider the one with the maximum length by comparing all the lengths.

![alt text](../../Screenshots/Longest%20Subarray%20with%20Sum%20k%20(Positive)_3.jpg)

### Code

```cpp
// Better Approach
// Time complexity -> O(n^2) and Space -> O(1)
int getLongestSubarray(vector<int>& nums, int k){
    // Write your code here
    int n=nums.size();
    int maxLen=0;
    for(int i=0;i<n;i++)
    {
        long long sum=0;
        for(int j=i;j<n;j++)
        {
            
            sum+=nums[j];
            if(sum==k)
            {
                maxLen=max(maxLen,j-i+1);
            }
        }
    }
    return maxLen;
    
}

```

### Approach 3: Optimized Approach [Using Hash map]

### Complexity

- Time complexity: O(n)
    
- Space complexity: O(n)
    

##### **Approach:**

The steps are as follows:

1. First, we will declare a map to store the prefix sums and the indices.
2. Then we will run a loop(say i) from index 0 to n-1(n = size of the array).
3. For each index i, we will do the following:
    1. We will add the current element i.e. a[i] to the prefix sum.
    2. If the sum is equal to k, we should consider the length of the current subarray i.e. i+1. We will compare this length with the existing length and consider the maximum one.
    3. We will calculate the prefix sum i.e. x-k, of the remaining subarray.
    4. If that sum of the remaining part i.e. x-k exists in the map, we will calculate the length i.e. i-preSumMap[x-k], and consider the maximum one comparing it with the existing length we have achieved until now.
    5. If the sum, we got after step 3.1, does not exist in the map we will add that with the current index into the map. We are checking the map before insertion because we want the index to be as minimum as possible and so we will consider the earliest index where the sum x-k has occurred.

![alt text](../../Screenshots/Longest%20Subarray%20with%20Sum%20k%20(Positive)_4.jpg)

### Code

```cpp
// Optimized Approach
// Time complexity -> O(n) and Space -> O(n)
int getLongestSubarray(vector<int>& nums, int k){
    // Write your code here
    int n=nums.size();
    unordered_map<long long,int> mpp;
    long long prefixsum=0;
    int maxLen=0;
    for(int i=0;i<n;i++)
    {
        prefixsum+=nums[i];
        if(prefixsum==k)
        {
            maxLen=max(maxLen,i+1);
        }
        long long remainingsum=prefixsum-k;
        if(mpp.find(remainingsum)!=mpp.end())
        {
            maxLen=max(maxLen,i-mpp[remainingsum]);
        }
        if(mpp.find(prefixsum)==mpp.end())
        {
            mpp[prefixsum]=i;   
        }
    }
    return maxLen;
    
}
```

*******

### GFG

[**Longest Subarray with Sum Zero**](https://www.geeksforgeeks.org/problems/largest-subarray-with-0-sum/1)  **Array contain positive and Negative integer**


Given an array having both positive and negative integers. The task is to compute the length of the largest subarray with sum 0.

**Example 1:**

```
Input: 
N = 8 
A[] = {15,-2,2,-8,1,7,10,23}

Output: 5

Explanation: The largest subarray with sum 0 will be -2 2 -8 1 7.
```

**Your Task:**  
You just have to complete the function **maxLen()** which takes two arguments an array **A** and **n,** where n is the size of the array A and returns the length of the largest subarray with 0 sum.

**Expected Time Complexity:** O(N).  
**Expected Auxiliary Space:** O(N).

**Constraints:**  
1 <= N <= 105  
-1000 <= A[i] <= 1000, for each valid i


### Approach 1: Brute Force Approach

### Complexity

- Time complexity: O(n^3)
    
- Space complexity: O(1)
    

##### **Approach:**

The steps are as follows:

1. First, we will run a loop(say i) that will select every possible starting index of the subarray. The possible starting indices can vary from index 0 to index n-1(n = size of the array).
2. Inside the loop, we will run another loop(say j) that will signify the ending index of the subarray. For every subarray starting from the index i, the possible ending index can vary from index i to n-1(n = size of the array).
3. After that for each subarray starting from index i and ending at index j **(i.e. arr[i….j]),** we will run another loop to calculate the sum of all the elements(of that particular subarray).
4. If the sum is equal to k, we will consider its length i.e. (j-i+1). Among all such subarrays, we will consider the maximum length by comparing all the lengths.


![alt text](../../Screenshots/Longest%20Subarray%20with%20Sum%20k%20(Positive)_1.jpg)

![alt text](../../Screenshots/Longest%20Subarray%20with%20Sum%20k%20(Positive)_2.jpg)

### Code

```cpp
// Brute Force Approach
// Time complexity -> O(n^3) and Space -> O(1)
class Solution{
    public:
    int maxLen(vector<int>&a, int n)
    {   
        // Your code here
        int maxLen=0;
        for(int i=0;i<n;i++)
        {
            for(int j=i;j<n;j++)
            {
                long long sum=0;
                for(int k=i;k<=j;k++)
                {
                    sum+=a[k];
                }
                if(sum==0)
                {
                    maxLen=max(maxLen,j-i+1);
                }
            }
        }
        return maxLen;
    }
};

// Above code give Time Limit Exceeded due to High Complexity O(n^3)
```



### Approach 2: Better Approach

### Complexity

- Time complexity: O(n^2)
    
- Space complexity: O(1)


##### **Approach:**

The steps are as follows:

1. First, we will run a loop(_say i_) that will select every possible starting index of the subarray. The possible starting indices can vary from index 0 to index n-1(n = array size).
2. Inside the loop, we will run another loop(say j) that will signify the ending index as well as the current element of the subarray. For every subarray starting from the index i, the possible ending index can vary from index i to n-1(n = size of the array).
3. Inside loop j, we will add the current element to the sum of the previous subarray i.e. **sum = sum + arr[j]**. 
4. If the sum is equal to k, we will consider its length i.e. (j-i+1). Among all such subarrays with sum k, we will consider the one with the maximum length by comparing all the lengths.

![alt text](../../Screenshots/Longest%20Subarray%20with%20Sum%20k%20(Positive)_3.jpg)

### Code

```cpp
// Better Approach
// Time complexity -> O(n^2) and Space -> O(1)
class Solution{
    public:
    int maxLen(vector<int>&a, int n)
    {   
        // Your code here
        int maxLen=0;
        for(int i=0;i<n;i++)
        {
            long long sum=0;
            for(int j=i;j<n;j++)
            {
                
                sum+=a[j];
                if(sum==0)
                {
                    maxLen=max(maxLen,j-i+1);
                }
            }
        }
        return maxLen;
        
    }
};

// Above code give Time Limit Exceeded due to High Complexity O(n^2)
```

### Approach 3: Optimized Approach [Using Hash map]

### Complexity

- Time complexity: O(n)
    
- Space complexity: O(n)
    

##### **Approach:**

The steps are as follows:

1. First, we will declare a map to store the prefix sums and the indices.
2. Then we will run a loop(say i) from index 0 to n-1(n = size of the array).
3. For each index i, we will do the following:
    1. We will add the current element i.e. a[i] to the prefix sum.
    2. If the sum is equal to k, we should consider the length of the current subarray i.e. i+1. We will compare this length with the existing length and consider the maximum one.
    3. We will calculate the prefix sum i.e. x-k, of the remaining subarray.
    4. If that sum of the remaining part i.e. x-k exists in the map, we will calculate the length i.e. i-preSumMap[x-k], and consider the maximum one comparing it with the existing length we have achieved until now.
    5. If the sum, we got after step 3.1, does not exist in the map we will add that with the current index into the map. We are checking the map before insertion because we want the index to be as minimum as possible and so we will consider the earliest index where the sum x-k has occurred.

![alt text](../../Screenshots/Longest%20Subarray%20with%20Sum%20k%20(Positive)_4.jpg)

### Code

```cpp
// Optimized Approach
// Time complexity -> O(n) and Space -> O(n)
class Solution{
    public:
    int maxLen(vector<int>&a, int n)
    {   
        // Your code here
        unordered_map<long long,int> mpp;
        int prefixsum=0;
        int maxLen=0;
        for(int i=0;i<n;i++)
        {
            prefixsum+=a[i];
            if(prefixsum==0)
            {
                maxLen=max(maxLen,i+1);
            }
            if(mpp.find(prefixsum)!=mpp.end())
            {
                maxLen=max(maxLen,i-mpp[prefixsum]);
            }
            if(mpp.find(prefixsum)==mpp.end())
            {
                mpp[prefixsum]=i;   
            }
        }
        return maxLen;
        
    }
};

```



**Important Link**
1. **[Video Link](https://youtu.be/frf7qxiN2qU)**







