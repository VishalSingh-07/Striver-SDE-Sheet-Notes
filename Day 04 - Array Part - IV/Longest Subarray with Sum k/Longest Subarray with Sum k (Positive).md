

[**Longest Subarray with Sum k**](https://www.codingninjas.com/studio/problems/longest-subarray-with-sum-k_6682399)  **Array contain only positive integer**


**Problem statement**

You are given an array _**'a'**_ of size _**'n'**_ and an integer _**'k'**_.

Find the length of the longest subarray of 'a' whose sum is equal to 'k'.


**Example :**

```
Input: ‘n’ = 7 ‘k’ = 3
‘a’ = [1, 2, 3, 1, 1, 1, 1]

Output: 3

Explanation: Subarrays whose sum = ‘3’ are:

[1, 2], [3], [1, 1, 1] and [1, 1, 1]

Here, the length of the longest subarray is 3, which is our final answer.
```


**Sample Input 1 :**

```
7 3
1 2 3 1 1 1 1
```

**Sample Output 1 :**

```
3
```

  

**Explanation Of Sample Input 1 :**

```
Subarrays whose sum = ‘3’ are:
[1, 2], [3], [1, 1, 1] and [1, 1, 1]
Here, the length of the longest subarray is 3, which is our final answer.
```

  
**Sample Input 2 :**

```
4 2
1 2 1 3
```


**Sample Output 2 :**

```
1
```

  
**Sample Input 3 :**

```
5 2
2 2 4 1 2 
```


**Sample Output 3 :**

```
1
```

  

**Expected time complexity :**

```
The expected time complexity is O(n).
```

  

**Constraints :**

```
1 <= 'n' <= 5 * 10 ^ 6
1 <= 'k' <= 10^18
0 <= 'a[i]' <= 10 ^ 9

Time Limit: 1-second
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
int longestSubarrayWithSumK(vector<int> a, long long k) {
    // Write your code here
    int n=a.size();
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
            if(sum==k)
            {
                maxLen=max(maxLen,j-i+1);
            }
        }
    }
    return maxLen;
}
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
int longestSubarrayWithSumK(vector<int> a, long long k) {
    // Write your code here
    int n=a.size();
    int maxLen=0;
    for(int i=0;i<n;i++)
    {
        long long sum=0;
        for(int j=i;j<n;j++)
        {
            sum+=a[j];
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
int longestSubarrayWithSumK(vector<int> a, long long k) {
    // Write your code here
    int n=a.size();
    map<long long,int> mpp;
    long long prefixsum=0;
    int maxLen=0;
    for(int i=0;i<n;i++)
    {
        prefixsum+=a[i];
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

### Approach 4: Most Optimized Approach [Two Pointer]

### Complexity

- Time complexity: O(n)
    
- Space complexity: O(1)
    

##### **Approach:**

The steps are as follows:

1. First, we will take two pointers: left and right, initially pointing to the index 0.
2. The sum is set to a[0] i.e. the first element initially.
3. Now we will run a while loop until the right pointer crosses the last index i.e. n-1.
4. Inside the loop, we will do the following:
    1. We will use another while loop and it will run until the sum is lesser or equal to k.
        1. Inside this second loop, from the sum, we will subtract the element that is pointed by the left pointer and increase the left pointer by 1.
    2. After this loop gets completed, we will check if the sum is equal to k. If it is, we will compare the length of the current subarray i.e. (right-left+1) with the existing one and consider the maximum one.
    3. Then we will move forward the right pointer by 1. If the right pointer is pointing to a valid index(< n) after the increment, we will add the element i.e. a[right] to the sum.
5. Finally, we will return the maximum length.

![alt text](../../Screenshots/Longest%20Subarray%20with%20Sum%20k%20(Positive)_5.jpg)

```cpp
// Most Optimized Approach
// Time complexity -> O(n) and Space -> O(1)
int longestSubarrayWithSumK(vector<int> a, long long k) {
    // Write your code here
    int n=a.size();
    int left=0,right=0;
    long long sum=a[0];
    int maxLen=0;
    while(right<n)
    {
        while(left<=right && sum>k)
        {
            sum-=a[left];
            left++;
        }
        if(sum==k)
        {
            maxLen=max(maxLen, right-left+1);
        }
        right++;
        if(right<n)
        {
            sum+=a[right];
        }
    }
    return maxLen;
}
```



**Important Link**
1. **[Video Link](https://youtu.be/frf7qxiN2qU)**




