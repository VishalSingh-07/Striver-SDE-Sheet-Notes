


#### Leetcode


**[Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array/)**

You are given two integer arrays `nums1` and `nums2`, sorted in **non-decreasing order**, and two integers `m` and `n`, representing the number of elements in `nums1` and `nums2` respectively.

**Merge** `nums1` and `nums2` into a single array sorted in **non-decreasing order**.

The final sorted array should not be returned by the function, but instead be _stored inside the array_ `nums1`. To accommodate this, `nums1` has a length of `m + n`, where the first `m` elements denote the elements that should be merged, and the last `n` elements are set to `0` and should be ignored. `nums2` has a length of `n`.

**Example 1:**

```
Input: nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3

Output: [1,2,2,3,5,6]

Explanation: The arrays we are merging are [1,2,3] and [2,5,6].

The result of the merge is [1,2,2,3,5,6] with the underlined elements coming from nums1.
```


**Example 2:**

```
Input: nums1 = [1], m = 1, nums2 = [], n = 0

Output: [1]

Explanation: The arrays we are merging are [1] and [].

The result of the merge is [1].
```

**Example 3:**

```
Input: nums1 = [0], m = 0, nums2 = [1], n = 1

Output: [1]

Explanation: The arrays we are merging are [] and [1].

The result of the merge is [1].

Note that because m = 0, there are no elements in nums1. The 0 is only there to ensure the merge result can fit in nums1.
```

**Constraints:**

- `nums1.length == m + n`
- `nums2.length == n`
- `0 <= m, n <= 200`
- `1 <= m + n <= 200`
- `-109 <= nums1[i], nums2[j] <= 109`

**Follow up:** Can you come up with an algorithm that runs in `O(m + n)` time?


#### Brute Force Approach

#### Complexity

- Time complexity: O(klogk)
    
- Space complexity: O(k)
    

where k = m + n

#### Code

```cpp
// Brute Force Approach 
// Copy elements of second array into first and sort the merged array 
// Time complexity --> O(klogk) and space :-- O(m+n)
// where k = m + n;

class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {

        vector<int> merge;

        for(int i=0;i<m;i++)
        {
            merge.push_back(nums1[i]);
        }
        for(int i=0;i<n;i++)
        {
            merge.push_back(nums2[i]);
        }

        sort(merge.begin(),merge.end());

        nums1.clear();

        for(auto it: merge)
        {
            nums1.push_back(it);
        }
    }
};
```

#### Better Approach

#### Complexity

- Time complexity:O(m + n)
    
- Space complexity: O(m + n)
    

#### Code

```cpp
// Better Approach
// Time complexity -> O(n+m) and Space -> O(n+m)
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {

        vector<int> nums3(n+m);
        int left=0;
        int right=0;
        int index=0;

        while(left<m && right<n)
        {
            if(nums1[left]<=nums2[right])
            {
                nums3[index]=nums1[left];
                left++;
                index++;
            }
            else
            {
                nums3[index]=nums2[right];
                right++;
                index++;
            }
        }
        while(left<m)
        {
            nums3[index++]=nums1[left++];
        }
        while(right<n)
        {
            nums3[index++]=nums2[right++];
        }
        for(int i=0;i<n+m;i++)
        {
            nums1[i]=nums3[i];
        }
    }
};
```

#### Optimized Approach

#### Complexity

- Time complexity: O(m+n)
    
- Space complexity: O(1)
    

#### Code

```cpp
// Optimized Approach [Two Pointer Approach] 
// Time complexity -->  O(m+n) and space: -- O(1)
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        int p1=m-1; // for first array (pointer)
        int p2=n-1; // for second array (pointer)
        int i=m+n-1; // Point to the last element of the array 1

        while(p2>=0)
        {
            if(p1>=0 && nums1[p1]>nums2[p2])
            {
                nums1[i]=nums1[p1];
                i--;
                p1--;
            }
            else
            {
                nums1[i]=nums2[p2];
                i--;
                p2--;
            }
        }
        
    }
};
```

![image.png](https://assets.leetcode.com/users/images/f0f0faed-a439-4ce8-9576-d20aed92d3bd_1688652049.4565148.png)

![image.png](https://assets.leetcode.com/users/images/f54748e8-ab6d-470f-b170-81f88aafd026_1688652107.412193.png)

![image.png](https://assets.leetcode.com/users/images/1dbf812a-ff2f-479a-83cf-9385b379cfaf_1688652143.3201115.png)

![image.png](https://assets.leetcode.com/users/images/760b0ec7-0498-47ac-b26b-dde85d7b7baa_1688652171.7061744.png)

![image.png](https://assets.leetcode.com/users/images/a63ce738-f407-4edd-969d-0db4f568e31c_1688652204.7190852.png)

![image.png](https://assets.leetcode.com/users/images/cd7643d3-46f2-4479-b0d4-08fa59ec9559_1688652236.4263797.png)


**Important Link**
1. **[Solution Link](https://leetcode.com/problems/merge-sorted-array/solutions/3727130/3-approach-easy-c-solution-brute-force-better-and-optimized-approach/)**
2.  **[Video Link](https://youtu.be/C4oBXLr3zos)**

---

### **[GFG Question](https://practice.geeksforgeeks.org/problems/merge-two-sorted-arrays-1587115620/1)**

#### Merge two Sorted Arrays Without Extra Space [Important]

Given two sorted arrays **arr1[]** and **arr2[]** of sizes **n** and **m** in non-decreasing order. Merge them in sorted order without using any extra space. Modify arr1 so that it contains the first N elements and modify arr2 so that it contains the last M elements.

**Example 1:**
```
Input: 
n = 4, arr1[] = [1 3 5 7] 
m = 5, arr2[] = [0 2 6 8 9]
Output: 
arr1[] = [0 1 2 3]
arr2[] = [5 6 7 8 9]
Explanation:
After merging the two 
non-decreasing arrays, we get, 
0 1 2 3 5 6 7 8 9.
```

**Example 2:**

```
Input: 
n = 2, arr1[] = [10 12] 
m = 3, arr2[] = [5 18 20]
Output: 
arr1[] = [5 10]
arr2[] = [12 18 20]
Explanation:
After merging two sorted arrays 
we get 5 10 12 18 20.

```

**Your Task:**  
You don't need to read input or print anything. You only need to complete the function **merge()** that takes arr1, arr2, n and m as input parameters and modifies them in-place so that they look like the sorted merged array when concatenated.

**Expected Time Complexity:**  O((n+m) log(n+m))  
**Expected Auxiliary Space:** O(1)

**Constraints:**  
1 <= n, m <= 105  
0 <= arr1i, arr2i <= 107



#### Naive Approach

#### Complexity

- Time complexity: O((n + m)log(n + m))
    
- Space complexity: O(n + m)
    

#### Code

```cpp
// Naive Approach
// Time complexity -> O((n + m)log(n + m)) and Space -> O(n + m)
class Solution{
    public:
        //Function to merge the arrays.
        void merge(long long arr1[], long long arr2[], int n, int m) 
        { 
            // creating vector for inserting both array element
            vector <long long> v;
            
            // Inserting 1st Array element
            for(int i=0;i<n;i++)
            {
                v.push_back(arr1[i]);
            }
            // Inserting 2nd Array element
            for(int i=0;i<m;i++)
            {
                v.push_back(arr2[i]);
            }
            
            // Sorting the whole vector array
            sort(v.begin(),v.end());
            
            // Inserting element in 1st Array with size "n" from vector v
            for(int i=0;i<n;i++)
            {
                arr1[i]=v[i];
            }
            // Inserting element in 2nd Array with size "n" from vector v
            for(int i=0;i<m;i++)
            {
                arr2[i]=v[n+i];
            }
            
            
        } 
};
```

#### Brute Force Approach

#### Complexity

- Time complexity: O(n + m)
    
- Space complexity: O(n + m)


Assume the size of the given arrays are n and m.

The steps are as follows:

1. We will first declare a third array, arr3[] of size n+m, and two pointers i.e. **_left and right_**, one pointing to the first index of arr1[] and the other pointing to the first index of arr2[].
2. The two pointers will move like the following:
    1. **If arr1[left] < arr2[right]:** We will insert the element arr1[left] into the array and increase the left pointer by 1.
    2. **If arr2[right] < arr1[left]:** We will insert the element arr2[right] into the array and increase the right pointer by 1.
    3. **If arr1[left] == arr2[right]:** Insert any of the elements and increase that particular pointer by 1.
    4. **If one of the pointers reaches the end,** then we will only move the other pointer and insert the rest of the elements of that particular array into the third array i.e. arr3[].
3. If we move the pointer like the above, we will get the third array in the sorted order.
4. Now, from sorted array arr3[], we will copy first n(_size of arr1[]_) elements to arr1[], and the next m(_size of arr2[]_) elements to arr2[].

#### Code

```cpp
// Brute Force Approach
// Time complexity -> O(n+m) and Space -> O(n+m) 
class Solution{
    public:
        //Function to merge the arrays.
        void merge(long long arr1[], long long arr2[], int n, int m) 
        { 
            // code here 
            long long arr3[n+m];
            int left=0;
            int right=0;
            int index=0;
            while(left<n && right<m)
            {
                if(arr1[left]<=arr2[right])
                {
                    arr3[index]=arr1[left];
                    left++;
                    index++;
                }
                else
                {
                    arr3[index]=arr2[right];
                    right++;
                    index++; 
                }
            }
            while(left<n)
            {
                arr3[index++]=arr1[left++];
            }
            while(right<m)
            {
                arr3[index++]=arr2[right++];
            }
            
            for(int i=0;i<n+m;i++)
            {
                if(i<n)
                {
                    arr1[i]=arr3[i];
                }
                else
                {
                    arr2[i-n]=arr3[i];
                }
            }
        } 
        
};
```

![WhatsApp Image 2023-07-06 at 17.23.42.jpg](https://assets.leetcode.com/users/images/872f11d6-7f11-44e5-a893-73cc8711f35d_1688644462.6431084.jpeg)

#### Optimized Approach [Two pointer]

#### Complexity

- Time complexity: O(min(n, m))+O(nlogn)+O(mlogm)
    
- Space complexity: O(1)


The sizes of the given arrays are n(_size of arr1[]_) and m(_size of arr2[]_).

The steps are as follows:

1. We will declare two pointers i.e. **left** and **right.** The left pointer will point to the last index of the arr1[](_i.e. Basically the maximum element of the array_). The right pointer will point to the first index of the arr2[](_i.e. Basically the minimum element of the array_).
2. Now, the left pointer will move toward index 0 and the right pointer will move towards the index m-1. While moving the two pointers we will face 2 different cases like the following:
    1. **If arr1[left] > arr2[right]:** In this case, we will swap the elements and move the pointers to the next positions.
    2. **If arr1[left] <= arr2[right]:** In this case, we will stop moving the pointers as arr1[] and arr2[] are containing correct elements.
3. Thus, after step 2, arr1[] will contain all smaller elements and arr2[] will contain all bigger elements. Finally, we will sort the two arrays.

#### Code

```cpp
// Optimized Approach 1 [Two Pointer]
// Time complexity -> O(min(n,m))+O(nlogn)+O(mlogm) and Space -> O(1) 
class Solution{
    public:
        //Function to merge the arrays.
        void merge(long long arr1[], long long arr2[], int n, int m) 
        { 
            // code here 
            int left=n-1;
            int right=0;
            while(left>=0 && right<m)
            {
                if(arr1[left]>arr2[right])
                {
                    swap(arr1[left],arr2[right]);
                    left--;
                    right++;
                }
                else
                {
                    break;
                }
            }
            sort(arr1,arr1+n);
            sort(arr2,arr2+m);
            
            
        } 
        
};
```

![WhatsApp Image 2023-07-06 at 17.23.40.jpg](https://assets.leetcode.com/users/images/3390c0f7-4550-4811-bdbc-65b2af8a36fb_1688644491.118808.jpeg)

#### Optimized Approach [Gap Method]

#### Complexity

- Time complexity: O(log2(n+m)*O(n+m))
    
- Space complexity: O(1)


The steps are as follows:

1. First, assume the two arrays as a single array and calculate the gap value i.e. ceil((size of arr1[] + size of arr2[]) / 2).
2. We will perform the following operations for each gap until the value of the gap becomes 0:
    1. Place two pointers in their correct position like the left pointer at index 0 and the right pointer at index (left + gap).
    2. Again we will run a loop until the right pointer reaches the end i.e. (n + m). Inside the loop, there will be 3 different cases:
        1. **If the left pointer is inside arr1[] and the right pointer is in arr2[]:** We will compare arr1[left] and arr2[right-n] and swap them if arr1[left] > arr2[right-n].
        2. **If both the pointers are in arr2[]:** We will compare arr1[left-n] and arr2[right-n] and swap them if arr1[left-n] > arr2[right-n].
        3. **If both the pointers are in arr1[]:** We will compare arr1[left] and arr2[right] and swap them if arr1[left] > arr2[right].
    3. After the right pointer reaches the end, we will decrease the value of the gap and it will become ceil(current gap / 2). 
3. Finally, after performing all the operations, we will get the merged sorted array.



#### Code

```cpp
// Optimized Approach 2
// Time complexity -> O(log2(n+m)*O(n+m)) and Space -> O(1) 
class Solution{
    private:
        void swapIfGreater(long long arr1[], long long arr2[], int index1, int index2)
        {
            if(arr1[index1]>arr2[index2])
            {
                swap(arr1[index1],arr2[index2]);
            }
        }
    public:
        //Function to merge the arrays.
        void merge(long long arr1[], long long arr2[], int n, int m) 
        { 
            // code here
            int len=n+m;
            int gap=(len/2)+(len%2);
            while(gap>0)
            {
                int left=0;
                int right=left+gap;
                while(right<len)
                {
                    // arr1 and arr2 element
                    if(left<n && right>=n)
                    {
                        swapIfGreater(arr1, arr2,left,right-n);
                    }
                    // arr2 and arr2 element
                    else if(left>=n)
                    {
                       swapIfGreater(arr2, arr2,left-n,right-n); 
                    }
                    // arr1 and arr1 element
                    else
                    {
                       swapIfGreater(arr1, arr1,left,right); 
                    }
                    left++;
                    right++;
                }
                if(gap==1)
                {
                    break;
                }
                gap=(gap/2)+(gap%2);
            }
            
        } 
        
};
```

![WhatsApp Image 2023-07-06 at 17.23.41.jpg](https://assets.leetcode.com/users/images/ae1c2137-c14e-4aac-a99e-890a8b6a69ac_1688644517.8748624.jpeg)

![WhatsApp Image 2023-07-06 at 17.23.41.jpg](https://assets.leetcode.com/users/images/baf08890-6db5-4f2a-8a49-3766ad08e3b3_1688644557.6922426.jpeg)

![WhatsApp Image 2023-07-06 at 17.23.43.jpg](https://assets.leetcode.com/users/images/94a072f5-82ec-4fb0-8d9a-ab72ae9e81fb_1688644583.2465158.jpeg)

![WhatsApp Image 2023-07-06 at 17.23.42.jpg](https://assets.leetcode.com/users/images/26c6c98b-7b4e-45a4-8e94-e05036c9ca34_1688644595.370868.jpeg)


**Important Link**
1. **[Solution Link](https://leetcode.com/problems/merge-sorted-array/solutions/3727130/3-approach-easy-c-solution-brute-force-better-and-optimized-approach/)**
2.  **[Video Link](https://youtu.be/n7uwj04E0I4)**