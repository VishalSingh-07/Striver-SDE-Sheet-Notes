
**[Count Inversions](https://practice.geeksforgeeks.org/problems/inversion-of-array-1587115620/1)**

**Medium**

Given an array of integers. Find the Inversion Count in the array. 

_**Inversion Count**:_ For an array, inversion count indicates how far (or close) the array is from being sorted. If array is already sorted then the inversion count is 0. If an array is sorted in the reverse order then the inversion count is the maximum.   
Formally, two elements a[i] and a[j] form an inversion if a[i] > a[j] and i < j.  
 

**Example 1:**

```
Input: N = 5, arr[] = {2, 4, 1, 3, 5}
Output: 3
Explanation: The sequence 2, 4, 1, 3, 5 has three inversions (2, 1), (4, 1), (4, 3).
```

**Example 2:**
```
Input: N = 5
arr[] = {2, 3, 4, 5, 6}
Output: 0
Explanation: As the sequence is already sorted so there is no inversion count.
```

**Example 3:**


```
Input: N = 3, arr[] = {10, 10, 10}
Output: 0
Explanation: As all the elements of array are same, so there is no inversion count.
```


**Your Task:  
You don't need to read input or print anything. Your task is to complete the function **inversionCount()** which takes the array arr[] and the size of the array as inputs and returns the inversion count of the given array.  
  
**Expected Time Complexity:** O(nLogn).  
**Expected Auxiliary Space:** O(n).  
  
**Constraints:**  
1 ≤ N ≤ 5*10^5  
1 ≤ arr[i] ≤ 10^18



#### Brute Force Approach

#### Complexity

- Time complexity: O(n^2)
    
- Space complexity: O(1)


The steps are as follows:

1. First, we will run a loop(say i) from 0 to N-1 to select the first element in the pair.
2. As index j should be greater than index i, inside loop i, we will run another loop i.e. j from i+1 to N-1.
3. Inside this second loop, we will check if a[i] > a[j] i.e. if a[i] and a[j] can be a pair. If they satisfy the condition, we will increase the count by 1.
4. Finally, we will return the count i.e. the number of such pairs.

**Intuition:** The naive approach is pretty straightforward. We will use nested loops to solve this problem. We know index i must be smaller than index j. So, we will fix i at one index at a time through a loop, and with another loop, we will check(_the condition a[i] > a[j]_) the elements from index i+1 to N-1  if they can form a pair with a[i]. This is the first naive approach we can think of.


#### Code

```cpp
// Brute Force Approach

// Time complexity -> O(n^2) and Space -> O(1)

class Solution{

  public:

    // arr[]: Input Array

    // N : Size of the Array arr[]

    // Function to count inversions in the array.

    long long int inversionCount(long long arr[], long long n)

    {

        // Your Code Here

        long long int count=0;

        for(int i=0;i<n;i++)

        {

            for(int j=i+1;j<n;j++)

            {

                if(arr[i]>arr[j])

                {

                    count++;

                }

            }

        }

        return count;

    }

  

};
```


Above code ❌ give time limit Exceeded due to high time complexity O(n^2)

![Image](../Screenshots/WhatsApp%20Image%202023-07-15%20at%2021.44.51.jpg)

#### Optimized Approach

#### Complexity

- Time complexity:  O(nlogn)
    
- Space complexity: O(n)


The steps are basically the same as they are in the case of the [merge sort algorithm](https://takeuforward.org/data-structure/merge-sort-algorithm/). The change will be just a one-line addition inside the **merge()** function. Inside the merge(), we need to add the number of pairs to the count when a[left] > a[right].

The steps of the merge() function were the following:

1. In the merge function, we will use a temp array to store the elements of the two sorted arrays after merging. Here, the range of the left array is low to mid and the range for the right half is mid+1 to high.
2. Now we will take two pointers left and right, where left starts from low and right starts from mid+1.
3. Using a while loop( while(left <= mid && right <= high)), we will select two elements, one from each half, and will consider the smallest one among the two. Then, we will insert the smallest element in the temp array. 
4. After that, the left-out elements in both halves will be copied as it is into the temp array.
5. Now, we will just transfer the elements of the temp array to the range low to high in the original array.

**Modifications in merge() and mergeSort():** 

- _In order to count the number of pairs, we will keep a count variable, cnt, initialized to 0 beforehand inside the merge()._
- _While comparing a[left] and a[right] in the 3rd step of merge(), if a[left] > a[right], we will simply add this line:__cnt += mid-left+1 (mid+1 = size of the left half)_
- Now, we will return this cnt from merge() to mergeSort(). 
- Inside mergeSort(), we will keep another counter variable that will store the final answer. With this cnt, we will add the answer returned from mergeSort() of the left half, mergeSort() of the right half, and merge().
- Finally, we will return this cnt, as our answer from mergeSort().


#### Code

```cpp
// Optimized Approach

// Time complexity -> O(nlogn) and Space -> O(n)

class Solution{

    private:

    long long merge(long long arr[], long long low, long long mid, long long high)

    {

        vector<long long> temp;

        long long left=low;

        long long right=mid+1LL;

        long long count=0;

        while(left<=mid && right<=high)

        {

            if(arr[left]<=arr[right])

            {

                temp.push_back(arr[left]);

                left++;

            }

            else

            {

                temp.push_back(arr[right]);

                count+=(mid-left+1LL);

                right++;

            }

        }

        while(left<=mid)

        {

            temp.push_back(arr[left]);

            left++;

        }

        while(right<=high)

        {

            temp.push_back(arr[right]);

            right++;

        }

        for(long long i=low;i<=high;i++)

        {

            arr[i]=temp[i-low];

        }

        return count;

    }

    long long int mergeSort(long long int arr[], long long int low, long long int high)

    {

        long long int count=0;

        if(low>=high)

        {

            return count;

        }

        long long int mid= low + (high - low) / 2;

        count+=mergeSort(arr,low,mid);

        count+=mergeSort(arr,mid+1,high);

        count+=merge(arr,low,mid,high);

        return count;

    }

    public:

    // arr[]: Input Array

    // N : Size of the Array arr[]

    // Function to count inversions in the array.

    long long int inversionCount(long long arr[], long long n)

    {

        // Your Code Here

        return mergeSort(arr,0,n-1);

    }

  

};
```
![Image](../Screenshots/WhatsApp%20Image%202023-07-15%20at%2021.44.49.jpg)

![Image](../Screenshots/WhatsApp%20Image%202023-07-15%20at%2021.44.52.jpg)

![Image](../Screenshots/WhatsApp%20Image%202023-07-15%20at%2021.44.50.jpg)

![Image](../Screenshots/WhatsApp%20Image%202023-07-15%20at%2021.44.51%201.jpg)



**Important Link**
1. **[Video Link](https://youtu.be/AseUmwVNaoY)**

