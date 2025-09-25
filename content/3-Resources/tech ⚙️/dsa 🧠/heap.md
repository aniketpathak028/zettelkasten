## Heap


```python
# kth Largest element in the array - easy

# approach-1: sorting, Time Complexity: O(n log n), Space Complexity: O(1)
# approach-2: using a min-heap, Time Complexity: O(n log k), Space Complexity: O(k)
import heapq
def findKthLargest(nums, k):
    heap= []
    for i in range(len(nums)):
        heapq.heappush(heap, nums[i])
    while len(heap)>k:
        heapq.heappop(heap)
    return heapq.heappop(heap)

# Time Complexity: O(n log k)
# Space Complexity: O(k)
```


```python
# kth Smallest element in the array - easy

def kthSmallest(arr,k):
    heap= []
    for i in range(len(arr)):
        heapq.heappush(heap, -arr[i])
    while len(heap)>k:
        heapq.heappop(heap)
    return -heapq.heappop(heap)

# Time Complexity: O(n log k)
# Space Complexity: O(k)
```


```python
# top k frequent elements in an array - easy

from collections import defaultdict
import heapq
def topKFrequent(nums, k):
    n= len(nums)
    heap= []
    mpp= defaultdict(int)
    for i in range(n):
        mpp[nums[i]]+=1
    for num, freq in mpp.items():
        heapq.heappush(heap,(freq, num))
    while len(heap)>k:
        heapq.heappop(heap)
    ans= []
    while len(heap):
        ans.append(heapq.heappop(heap)[1])
    return ans

# Time Complexity: O(n log k)
# Space Complexity: O(n)
```


```python
# merge k sorted linked lists 

class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

from typing import List, Optional
import heapq
def mergeKLists(lists: List[Optional[ListNode]]) -> Optional[ListNode]:
    heap= []
    k= len(lists)
    for i in range(k):
        node= lists[i]
        if node:
            heapq.heappush(heap, (node.val, id(node), node))
    dummyNode = ListNode()
    temp= dummyNode
    while len(heap):
        _, _, second= heapq.heappop(heap)
        temp.next= second
        temp= temp.next
        if second.next:
            heapq.heappush(heap, (second.next.val, id(second.next), second.next))
    return dummyNode.next

# Time Complexity: O(n log k)
# Space Complexity: O(k)
# where n is the total number of nodes in all linked lists and k is the number of linked lists
```


```python
# task scheduler

from collections import Counter, deque
import heapq
def leastInterval(tasks, n):
    counter= Counter(tasks)
    maxHeap= [-cnt for cnt in counter.values()]
    heapq.heapify(maxHeap)
    q= deque()
    time= 0
    while maxHeap or q:
        time+=1
        if maxHeap:
            cnt= heapq.heappop(maxHeap) + 1
            if cnt:
                q.append((cnt, time+n))
        if q and q[0][1]==time:
            heapq.heappush(maxHeap, q.popleft()[0])
    return time

# Time Complexity: O(n log n)
# Space Complexity: O(n)
```


```python
# kth largest element in a stream

import heapq
class KthLargest:
    def __init__(self, k: int, nums: List[int]):
        self.k = k
        self.minHeap = []
        for num in nums:
            heapq.heappush(self.minHeap, num)
            if len(self.minHeap) > k:
                heapq.heappop(self.minHeap)

    def add(self, val: int) -> int:
        heapq.heappush(self.minHeap, val)
        if len(self.minHeap) > self.k:
            heapq.heappop(self.minHeap)
        return self.minHeap[0]
```


```python
# k sorted array

# If this array is truly K-sorted, then my K+1 heap method should produce perfect sorted order. 

def kSortedArray(arr, n, k):
    heap= []
    sortedArr= []
    if k>=n:
        return "Yes"
    for i in range(n):
        heapq.heappush(heap, arr[i])
        if i >= k:
            sortedArr.append(heapq.heappop(heap))
    while len(heap):
        sortedArr.append(heapq.heappop(heap))
    for i in range(1,n):
        if sortedArr[i]<sortedArr[i-1]:
            return "No"
    return "Yes"

# Time Complexity: O(n log k)
```


```python
# k closest elements

import heapq
def findClosestElements(arr, k, x):
    heap= []
    for i in range(len(arr)):
        heapq.heappush(heap, (-abs(arr[i]-x), -arr[i]))
        if len(heap)>k:
            heapq.heappop(heap)
    ans= []
    while heap:
        ans.append(-heapq.heappop(heap)[1])
    return sorted(ans)
```
