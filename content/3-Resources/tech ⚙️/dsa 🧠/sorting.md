## Sorting Algorithms

### Merge Sort


```python
def merge(arr, start, mid, end):
    left= start
    right= mid+1

    temp = []

    while left<=mid and right<=end:
        if arr[left]<=arr[right]:
            temp.append(arr[left])
            left+=1
        else:
            temp.append(arr[right])
            right+=1

    while left<=mid:
        temp.append(arr[left])
        left+=1
    
    while right<=end:
        temp.append(arr[right])
        right+=1

    for i in range(start,end+1):
        arr[i]= temp[i-start]

def mergesort(arr, start, end):
    if start>=end:
        return
    
    mid=(start + end)//2

    mergesort(arr,start,mid)
    mergesort(arr,mid+1,end)
    merge(arr,start,mid,end)


arr = [2, 1, 3, 8, 4, 6]
mergesort(arr,0,5)
print(arr)

# Time Complexity = O(NlogN) , Space Complexity = O(N)

```

    [1, 2, 3, 4, 6, 8]


### Quick Sort


```python
def getpartition(arr, start, end):
    pivot = arr[start]
    i = start + 1
    j = end

    while True:
        while i <= j and arr[i] <= pivot:
            i += 1
        while i <= j and arr[j] > pivot:
            j -= 1

        if i <= j:
            arr[i], arr[j] = arr[j], arr[i]
        else:
            break

    arr[start], arr[j] = arr[j], arr[start]
    return j


def quicksort(arr, start, end):
    if start < end:
        partition = getpartition(arr, start, end)
        quicksort(arr, start, partition - 1)
        quicksort(arr, partition + 1, end)


arr = [2, 1, 3, 8, 4, 6]
quicksort(arr, 0, len(arr) - 1)
print(arr)
```

    [1, 2, 3, 4, 6, 8]

