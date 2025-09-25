## Binary Search

##### When to use binary search?
A find operation where we can always eliminate half of our search space based on some condition


```python
# binary search on a sorted array

def binary_search(arr, target):
    left, right = 0, len(arr) - 1
    while left <= right:
        mid = left + (right - left) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return -1

# time complexity: O(logn)
# space complexity: O(1)
```


```python
# lower bound - first element that is greater than or equal to the target

def lower_bound(arr, target):
    start, end= 0, len(arr)-1
    ans= len(arr) # incase the target greater than the largest element
    while start<=end:
        mid= start + (end-start)//2
        if arr[mid]>=target:
            ans= mid
            end= mid-1
        else:
            start= mid+1
    return ans
```


```python
# upper bound - first element that is greater than target

def upper_bound(arr, target):
    start, end= 0, len(arr)-1
    ans= len(arr) # incase the target greater than the largest element
    while start<=end:
        mid= start + (end-start)//2
        if arr[mid]<=target:
            start= mid+1
        else:
            ans= mid
            end= mid-1
    return ans
```


```python
# floor of 'x' - the largest element in the array <= 'x'.

def floor(arr, num):
    start, end= 0, len(arr)-1
    ans= -1
    while start<=end:
        mid= start + (end-start)//2
        if arr[mid]==num:
            return mid
        elif arr[mid]<num:
            ans= mid
            start= mid+1
        else:
            end= mid-1
    return ans
```


```python
# ceil of 'x' - the smallest element in the array >='x'.

def ceil(arr, num):
    start, end= 0, len(arr)-1
    ans= -1
    while start<=end:
        mid= start + (end-start)//2
        if arr[mid]==num:
            return mid
        elif arr[mid]<num:
            start= mid+1
        else:
            ans= mid
            end= mid-1
    return ans
```


```python
# first occurence of a number

def firstOccurence(nums, target):
        start, end= 0, len(nums)-1
        first= -1
        while start<=end:
            mid= start + (end-start)//2
            if nums[mid]==target:
                first= mid
                end= mid-1
            elif nums[mid]<target:
                start= mid+1
            else:
                end=mid-1
        return first
```


```python
# last occurence of a number

def lastOccurence(nums, target):
    start, end= 0, len(nums)-1
    last= -1
    while start<=end:
        mid= start + (end-start)//2
        if nums[mid]==target:
            last= mid
            start= start+1
        elif nums[mid]<target:
            start= mid+1
        else:
            end=mid-1
    return last
```


```python
# 1. Search in Rotated Sorted Array

def search(nums, target):
    start, end= 0, len(nums)-1
    while start<=end:
        mid= start + (end-start)//2
        if nums[mid]==target:
            return mid    
        if nums[start]<=nums[mid]:
            if nums[start]<=target and target<nums[mid]:
                end= mid-1
            else:
                start= mid+1
        else:
            if nums[end]>=target and target>nums[mid]:
                start= mid+1
            else:
                end= mid-1
    return -1

# concept : at any given index i => either arr[0] -> arr[i] == sorted or arr[i] -> arr[n-1] == sorted
```


```python
# 2. Search in Rotated Sorted Array with Duplicates

def search(nums, target):
    start, end= 0, len(nums)-1
    while start<=end:
        mid= start+(end-start)//2
        if nums[mid]==target:
            return True
        
        # shrink the search space when start=mid=end
        if nums[start]==nums[mid] and nums[end]==nums[mid]:
            start+=1
            end-=1
            continue

        if nums[start]<=nums[mid]:
            if nums[start]<=target and target<nums[mid]:
                end= mid-1
            else:
                start= mid+1
        else:
            if nums[end]>=target and target>nums[mid]:
                start= mid+1
            else:
                end= mid-1
    return False

# Time complexity: O(logn) but in worst case O(n) as we are shrinking the search space by 1
# Space complexity: O(1)
```


```python
# 3. Find Minimum in Rotated Sorted Array

def findMin(nums):
    start, end= 0, len(nums)-1
    while start<end:
        mid= start + (end-start)//2
        if nums[mid]>nums[end]:
            start= mid+1
        else:
            end= mid
    return nums[start]

# concept: min will always lie in the unsorted portion of the array
```


```python
# 4. Find Kth Rotation

def findKthRotation(nums):
    start, end= 0, len(nums)-1
    while start<end:
        mid= start+(end-start)//2
        if nums[mid]>nums[end]:
            start= mid+1
        else:
            end= mid
    return start
```


```python
# 5. Find the single element in a sorted array

def singleNonDuplicate(nums):
    size= len(nums)
    if size==1 or nums[0]!=nums[1]:
        return nums[0]

    if nums[size-1]!=nums[size-2]:
        return nums[size-1]

    start, end= 0, size-1
    while start<=end:
        mid= start + (end-start)//2

        if nums[mid]!=nums[mid-1] and nums[mid]!=nums[mid+1]:
            return nums[mid]

        # we are on the left of the ans
        if (mid%2==0 and nums[mid]==nums[mid+1]) or (mid%2==1 and nums[mid]==nums[mid-1]):
            start= mid+1
        
        # we are definitely on the right
        else: 
            end= mid-1

    return -1 
```


```python
# 6. Find the peak element in an array

def findPeakElement(nums):
    if len(nums)==1:
        return 0
    
    if nums[0]>nums[1]:
        return 0
    
    if nums[-1]>nums[-2]:
        return len(nums)-1
    
    start, end= 0, len(nums)-1
    while start<=end:
        mid= start + (end-start)//2

        # check if mid is the peak element
        if nums[mid]>nums[mid+1] and nums[mid]>nums[mid-1]:
            return mid
        
        # check if mid is on the left of the peak element
        elif nums[mid]<nums[mid+1]:
            start= mid+1
        else:
            end= mid-1

    return -1
```


```python
# 7. Find the square root of a number

def findSquareRoot(num):
    start, end= 0, num
    ans= -1
    while start<=end:
        mid= start + (end-start)//2
        if mid*mid==num:
            return mid
        elif mid*mid<num:
            ans= mid
            start= mid+1
        else:
            end= mid-1
    return ans
```


```python
# 8. Find nth root of a number

def findNthRoot(n, m):
    start, end= 1, m
    while start<=end:
        mid= start + (end-start)//2
        if mid**n==m:
            return mid
        elif mid**n<m:
            start= mid+1
        else:
            end= mid-1
    return -1
```


```python
# 9. koko eating bananas

import math
def getTimeToEat(piles, k):
    time= 0
    for bananas in piles:
        time+= math.ceil(bananas/k)
    return time

def minEatingSpeed(piles, h):
    start, end= 1, max(piles)
    while start<=end:
        mid= start + (end-start)//2

        if getTimeToEat(piles, mid)>h:
            start= mid+1
        else:
            end= mid-1
    return start
```


```python
# 10. find Kth missing positive integer

def findKthMissing(arr, k):
    size= len(arr)
    missingTillLast= arr[size-1]-(size)
    if k<arr[0]:
        return k
    if k>missingTillLast:
        return arr[size-1]+(k-missingTillLast)

    start, end= 0, size-1
    while start<=end:
        mid= start+(end-start)//2
        missingTillMid= arr[mid]-(mid+1)
        if missingTillMid<k:
            start= mid+1
        else:
            end= mid-1
    return arr[end]+(k-(arr[end]-(end+1)))
```


```python
# 11. Agressive cows

def canPlaceCows(stalls, dist, k):
        count, last= 1, 0
        for i in range(1, len(stalls)):
            if stalls[i]-stalls[last]>=dist:
                last= i
                count+=1
        return count>=k
                
def aggressiveCows(stalls, k):
    stalls.sort()
    start, end= 1, stalls[len(stalls)-1]-stalls[0]
    while start<=end:
        mid= start + (end-start)//2
        if canPlaceCows(stalls, mid, k):
            start= mid+1
        else:
            end= mid-1
    return end
```


```python
# 12. Book Allocation

def allocatePages(books, p, m):
    count, sumPages= 1, 0
    for book in books:
        if sumPages+book>p:
            count+= 1
            sumPages= book
        else:
            sumPages+= book
    
    return count<=m
        
def findPages(arr, m):
    n= len(arr)
    if m>n:
         return -1
    start, end= max(arr), sum(arr)
    while start<=end:
        mid= start + (end-start)//2
        if allocatePages(arr, mid, m):
            end= mid-1
        else:
            start= mid+1
    return start
```


```python
# 13. Minimize maximum distance between gas stations

import heapq
def minimiseMaxDistance(arr, k):
    pq = []
    how_many = [0] * (len(arr) - 1)

    for i in range(len(arr) - 1):
        diff = arr[i + 1] - arr[i]
        heapq.heappush(pq, (-diff, i))

    for _ in range(k):
        dist, index = heapq.heappop(pq)
        actual_diff = arr[index + 1] - arr[index]

        new_diff = actual_diff / (how_many[index] + 2)
        heapq.heappush(pq, (-new_diff, index))
        how_many[index] += 1

    return -pq[0][0]
```


```python
# 14. Median of 2 sorted arrays
# brute force O(m+n)

def findMedianSortedArrays(nums1, nums2):      
    n1, n2= len(nums1), len(nums2)
    ptr1, ptr2= 0, 0
    n= n1 + n2
    idx2= n//2
    idx1= idx2-1
    idxEle1, idxEle2= -1, -1 
    cnt= 0 

    while ptr1<n1 and ptr2<n2:
        if nums1[ptr1]<nums2[ptr2]:
            if cnt==idx1:
                idxEle1= nums1[ptr1]
            if cnt==idx2:
                idxEle2= nums1[ptr1]
            cnt+=1
            ptr1+=1
        else:
            if cnt==idx1:
                idxEle1= nums2[ptr2]
            if cnt==idx2:
                idxEle2= nums2[ptr2]
            cnt+=1
            ptr2+=1
    
    while ptr1<n1:
        if cnt==idx1:
            idxEle1= nums1[ptr1]
        if cnt==idx2:
            idxEle2= nums1[ptr1]
        cnt+=1
        ptr1+=1

    while ptr2<n2:
        if cnt==idx1:
            idxEle1= nums2[ptr2]
        if cnt==idx2:
            idxEle2= nums2[ptr2]
        cnt+=1
        ptr2+=1

    return idxEle2 if n%2 else (idxEle1+idxEle2)/2
```


```python
# optimal solution
import sys
def findMedianSortedArrays(nums1, nums2):
    n1, n2 = len(nums1), len(nums2)
    n = n1 + n2

    if n == 1:
        return nums1[0] if n1 == 1 else nums2[0]

    # total number of elements in the left of median
    leftCount = n // 2

    # taking the array with less elements as arr1
    arr1 = nums1 if n1 <= n2 else nums2
    arr2 = nums2 if n1 <= n2 else nums1

    start, end = max(0, leftCount-len(arr2)), min(leftCount, len(arr1))
    while start <= end:
        mid = start + (end - start) // 2

        # mid = elements from arr1
        elementsFromArr1= mid 
        elementsFromArr2 = leftCount - mid

        l1 = arr1[elementsFromArr1 - 1] if elementsFromArr1 > 0 else -sys.maxsize - 1
        l2 = arr2[elementsFromArr2 - 1] if elementsFromArr2 > 0 else -sys.maxsize - 1
        r1 = arr1[elementsFromArr1] if len(arr1) - elementsFromArr1 > 0  else sys.maxsize
        r2 = arr2[elementsFromArr2] if len(arr2) - elementsFromArr2 > 0  else sys.maxsize

        if max(l1, l2) <= min(r1, r2):
            # if odd then return the median
            if n % 2:
                return min(r1, r2)
            else:
            # if even then calculate the median
                return (max(l1, l2) + min(r1, r2)) / 2
        elif l1 > r2:
            end = mid - 1
        else:
            start = mid + 1
```


```python
# 15. Kth element of 2 sorted arrays

import sys
def findKth(nums1, nums2, k):
    n1, n2 = len(nums1), len(nums2)
    n = n1 + n2

    # total number of elements in the left of median
    leftCount = k

    # taking the array with less elements as arr1
    arr1 = nums1 if n1 <= n2 else nums2
    arr2 = nums2 if n1 <= n2 else nums1

    start, end = max(0, leftCount-len(arr2)), min(leftCount, len(arr1))
    while start <= end:
        mid = start + (end - start) // 2

        # mid = elements from arr1
        elementsFromArr1= mid 
        elementsFromArr2 = leftCount - mid

        l1 = arr1[elementsFromArr1 - 1] if elementsFromArr1 > 0 else -sys.maxsize - 1
        l2 = arr2[elementsFromArr2 - 1] if elementsFromArr2 > 0 else -sys.maxsize - 1
        r1 = arr1[elementsFromArr1] if len(arr1) - elementsFromArr1 > 0  else sys.maxsize
        r2 = arr2[elementsFromArr2] if len(arr2) - elementsFromArr2 > 0  else sys.maxsize

        if max(l1, l2) <= min(r1, r2):
            return max(l1, l2)
        elif l1 > r2:
            end = mid - 1
        else:
            start = mid + 1
```


```python
# 16. Find the row with maximum number of 1's

```


```python
# 17. Search in a 2D matrix

def searchInMatrix(matrix, target):
    n, m= len(matrix), len(matrix[0])
    start, end= 0, n*m-1
    while start<=end:
        mid= start + (end-start)//2
        x, y= mid//m, mid%m
        if matrix[x][y]==target:
            return True
        elif matrix[x][y]<target:
            start= mid+1
        else:
            end= mid-1
    return False

# Time Complexity = O(log(n*m))
```


```python
# 18. Search in a row and column wise sorted matrix

def searchInMatrix(matrix, target):
    i, j= 0, len(matrix[0])-1
    while i<=len(matrix)-1 and j>=0:
        if matrix[i][j]==target:
            return True
        elif matrix[i][j]<target:
            i+=1
        else:
            j-=1
    return False
```


```python
# 19. Find peak in a 2D Matrix

def findMaxInColumn(mat, col):
        maxi, index= 0, -1
        for i in range(len(mat)):
            if mat[i][col]>maxi:
                maxi= mat[i][col]
                index= i
        return index

def findPeakGrid(mat):
    m=len(mat[0])
    start, end= 0, m-1
    while start<=end:
        mid= start+(end-start)//2
        maxIndex= findMaxInColumn(mat, mid)
        left= mat[maxIndex][mid-1] if mid>0 else -1
        right= mat[maxIndex][mid+1] if mid<m-1 else -1
        if mat[maxIndex][mid]>left and mat[maxIndex][mid]>right:
            return maxIndex, mid
        elif mat[maxIndex][mid]<left:
            end= mid-1
        else:
            start= mid+1
    return -1,-1
```


```python
# 20. Matrix Median

import bisect

def countLessThan(n, mat):
    ans = 0
    for row in mat:
        ans += bisect.bisect_right(row, n)
    return ans

def median(mat):
    n, m = len(mat), len(mat[0])
    
    # Initialize start and end values from the matrix
    start = min(row[0] for row in mat)
    end = max(row[-1] for row in mat)

    countNeeded = (n * m) // 2

    while start <= end:
        mid = start + (end - start) // 2
        if countLessThan(mid, mat) <= countNeeded:
            start = mid + 1
        else:
            end = mid - 1

    return start

# Time complexity: O(nlogm) where n is the number of rows and m is the number of columns
# Space complexity: O(1)
```
