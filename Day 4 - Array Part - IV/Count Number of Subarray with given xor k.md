[**Count Number of Subarray with given xor k**](https://www.codingninjas.com/studio/problems/subarrays-with-xor-k_6826258)


**Problem statement**

Given an array _**‘A’**_ consisting of _**‘N’**_ integers and an integer _**‘B’**_, find the number of subarrays of array ‘A’ whose bitwise XOR( ⊕ ) of all elements is equal to ‘B’.  

A subarray of an array is obtained by removing some(zero or more) elements from the front and back of the array.


**Example:**

```
Input: ‘N’ = 4 ‘B’ = 2
‘A’ = [1, 2, 3, 2]

Output: 3

Explanation: Subarrays have bitwise xor equal to ‘2’ are: [1, 2, 3, 2], [2], [2].
```



**Sample Input 1:**

```
4 2
1 2 3 2
```

**Sample Output 1 :**

```
3
```

**Explanation Of Sample Input 1:**

```
Input: ‘N’ = 4 ‘B’ = 2
‘A’ = [1, 2, 3, 2]

Output: 3

Explanation: Subarrays have bitwise xor equal to ‘2’ are: [1, 2, 3, 2], [2], [2].
```

**Sample Input 2:**

```
4 3
1 2 3 3
```

**Sample Output 2:**

```
4
```

**Sample Input 3:**

```
5 6
1 3 3 3 5 
```

**Sample Output 3:**

```
2
```

**Constraints:**

```
1 <= N <= 10^3
1 <= A[i], B <= 10^9

Time Limit: 1-sec
```


### Approach 1: Brute Force Approach

### Complexity

- Time complexity: O(n^3)
    
- Space complexity: O(1)
    

##### **Approach:**

The steps are as follows:

1. **Generate Subarrays:** 
    1. First, we will run a loop(say i) that will select every possible starting index of the subarray. The possible starting indices can vary from index 0 to index n-1(n = size of the array).
    2. Inside the loop, we will run another loop(say j) that will signify the ending index of the subarray. For every subarray starting from the index i, the possible ending index can vary from index i to n-1(n = size of the array).  
        
2. **Calculate XOR of the subarray:** After that for each subarray starting from index i and ending at index j **(i.e. arr[i….j]),** we will run another loop to calculate the XOR of all the elements(of that particular subarray).  
    
3. **Check the XOR and modify the count:** If the XOR is equal to k, we will increase the count by 1.


### Code

```cpp
// Brute Force Approach
// Time complexity -> O(n^3) and Space -> O(1)
int subarraysWithSumK(vector < int > a, int b) {
    // Write your code here
    int  count=0;
    int n=a.size();
    for(int i=0;i<n;i++)
    {
        
        for(int j=i;j<n;j++)
        {
            int xorsum=0;
            for(int k=i;k<=j;k++)
            {
                xorsum^=a[k];
            }
            if(xorsum==b)
            {
                count++;
            }
        }
    }
    return count;
}

// Above code give time limit exceeded due to high time complexity O(n^3)

```



### Approach 2: Better Approach

### Complexity

- Time complexity: O(n^2)
    
- Space complexity: O(1)


##### **Approach:**

The steps are as follows:

1. **Generate Subarrays:** 
    1. First, we will run a loop(say i) that will select every possible starting index of the subarray. The possible starting indices can vary from index 0 to index n-1(n = array size).
    2. Inside the loop, we will run another loop(say j) that will signify the ending index as well as the current element of the subarray. For every subarray starting from the index i, the possible ending index can vary from index i to n-1(n = size of the array).
2. **Calculate XOR of the subarray:** Inside loop j, we will XOR the current element to the XOR of the previous subarray i.e. **xorr = XOR(a[i….j-1]) ^ arr[j]**. 
3. **Check the XOR and modify the count:** After calculating the XOR, we will check if the sum is equal to the given k. If it is, we will increase the value of the count.

### Code

```cpp
// Better Approach
// Time complexity -> O(n^2) and Space -> O(1)
int subarraysWithSumK(vector < int > a, int b) {
    // Write your code here
    int  count=0;
    int n=a.size();
    for(int i=0;i<n;i++)
    {
        int xorsum=0;
        for(int j=i;j<n;j++)
        {
            xorsum^=a[j];
            if(xorsum==b)
            {
                count++;
            }
        }
    }
    return count;
}
```

### Approach 3: Optimized Approach [Using Hash map]

### Complexity

- Time complexity: O(n)
    
- Space complexity: O(n)
    

##### **Approach:**

The steps are as follows:

1. First, we will declare a map to store the prefix XORs and their counts.
2. Then, we will set the value of 0 as 1 on the map.
3. Then we will run a loop(say i) from index 0 to n-1(n = size of the array).
4. For each index i, we will do the following:
    1. We will XOR the current element i.e. arr[i] to the existing prefix XOR.
    2. Then we will calculate the prefix XOR i.e. xr^k, for which we need the occurrence.
    3. We will add the occurrence of the prefix XOR xr^k i.e. mpp[xr^k] to our answer.
    4. Then we will store the current prefix XOR, xr in the map increasing its occurrence by 1.




![alt text](../Screenshots/Count%20Number%20of%20Subarray%20with%20given%20Xor%20k_1.jpg)

![alt text](../Screenshots/Count%20Number%20of%20Subarray%20with%20given%20Xor%20k_2.jpg)

![alt text](../Screenshots/Count%20Number%20of%20Subarray%20with%20given%20Xor%20k_3.jpg)

### Code

```cpp
// Optimized Approach
// Time complexity -> O(n) and Space -> O(n)
int subarraysWithSumK(vector < int > a, int b) {
    // Write your code here
    int count=0,xorsum=0;
    unordered_map<int,int> mpp;
    mpp[xorsum]++; // {0,1}
    for(int i=0;i<a.size();i++)
    {
        xorsum^=a[i];
        int x=xorsum^b;
        count+=mpp[x];
        mpp[xorsum]++;

    }
    return count;
}

```



**Important Link**
1. **[Video Link](https://youtu.be/eZr-6p0B7ME)**








