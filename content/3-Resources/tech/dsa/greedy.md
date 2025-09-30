## Greedy


```python
# assign cookies

def findContentChildren(g, s):
    s.sort()
    g.sort()
    n, m= len(g),len(s)
    l, r= 0,0
    while l<n and r<m:
        if s[r]>=g[l]:
            r+= 1
            l+= 1
        else:
            r+=1
    return l

g= [1, 2]
s= [1, 2, 3]
print(findContentChildren(g,s))
```

    2



```python
# fractional knapsack

def fractionalknapsack(val, wt, capacity):
    ans= 0
    cap= capacity
    n= len(val)
    tpl= []
    for i in range(n):
        tpl.append((val[i],wt[i]))
    tpl.sort(key=lambda x: x[1]/x[0])
    for i in range(len(tpl)):
        value,weight= tpl[i][0], tpl[i][1]
        if cap>=weight:
            cap-= weight
            ans+= value
        else:
            ans+= cap*(value/weight)
            break
    return ans
```


```python
# minimum number of coins needed

def minPartition(N):
    currency= [1, 2, 5, 10, 20, 50, 100, 200, 500, 2000]
    ans= []
    for i in range(len(currency)-1,-1,-1):
        while N>0 and currency[i]<=N:
            ans.append(currency[i])
            N-=currency[i]
    return ans
```


```python
# valid paranthesis

# approach-1: use recursion, for each * we can either treat it as ( or ) or empty, if at any point cnt==-1 return False 
# T.C O(3^n) S.C O(n)

def check(s, i, cnt):
    if i==len(s):
        return cnt==0

    if cnt<0:
        return False

    if s[i]=="(":
        return check(s, i+1, cnt+1)
    elif s[i]==")":
        return check(s, i+1, cnt-1)
    else:
        return check(s, i+1, cnt+1) or check(s, i+1, cnt-1) or check(s, i+1, cnt)

def isValid(s):
    return check(s, 0, 0)
```


```python
# approach-2: use min and max counters, for each ( we increase both min and max, for each ) we decrease both
# for each * we decrease min by 1 and increase max by 1, if at any point max<0 return False, at the end check if min==0

# Note: this is a trick for recursion based greedy problems, where there are multiple possibilities, we can use this min and max approach to keep the extremes and return the answer based on the extreme values

# T.C O(n) S.C O(1)

def isValid(s):
    min, max= 0, 0
    for i in range(s):
        if s[i]=='(':
            min+= 1
            max+= 1
        elif s[i]==')':
            min-= 1
            max-= 1
        else:
            min-= 1
            max+= 1
        if max<0:
            return False
        min= max(0, min)
    return min==0
```


```python
# n meetings in one room

def maxMeetings(start, end):
    n= len(start)
    meetings= []
    for i in range(n):
        meetings.append((start[i], end[i]))
    meetings.sort(key=lambda x: x[1])
    ans= []
    last_end= -1
    for i in range(n):
        if meetings[i][0]>last_end:
            ans.append(i+1)
            last_end= meetings[i][1]
    return ans
```


```python
# jump game

# approach-1: use recursion, for each index we can jump to any index from i+1 to i+nums[i], if we reach the end return True
# T.C O(2^n) S.C O(n)

# approach-2: use dp  T.C O(n^2) S.C O(n)

# approach-3: use greedy, for each index we can jump to any index from i+1 to i+nums[i], if we reach the end return True
# we can keep track of the farthest index we can reach, if at any point we reach an index that is greater than the farthest index we can reach, return False
# T.C O(n) S.C O(1)
def canJump(nums):
    maxIndex= 0
    for i in range(len(nums)):
        if i>maxIndex:
            return False
        maxIndex= max(maxIndex, i+nums[i])
    return True
```


```python
# jump game II

# dp approach
# Time Complexity: O(n^2)
# Space Complexity: O(n)

def solve(i, nums, dp):
    if i>=len(nums)-1:
        return 0

    if dp[i]!=-1:
        return dp[i]

    mini= sys.maxsize
    for j in range(1, nums[i]+1):
        mini= min(mini, 1+solve(i+j, nums, dp))
    dp[i]= mini
    return mini

def jump(nums):
    n= len(nums)
    dp= [-1] * n
    return solve(0, nums, dp)
```


```python
# jump game II

# Greedy approach
# Time Complexity: O(n)
# Space Complexity: O(1)

def jump(nums):
    n= len(nums)
    l, r= 0,0
    jumps= 0
    while r<n-1:
        farthest= -1
        for i in range(l, r+1):
            farthest= max(farthest, i+nums[i])
        l= r+1
        r= farthest
        jumps+=1
    return jumps
```


```python
# minimum number of platforms

def minimumPlatform(arr,dep):
    cnt= 0
    dep.sort()
    arr.sort()
    n= len(arr)
    i, j= 0, 0
    ans= -1
    while i<n:
        if arr[i]<=dep[j]:
            cnt+=1
            i+=1
        else:
            cnt-=1
            j+=1
        ans= max(ans, cnt)
    return ans
```


```python
# candy problem

# naive approach

# Time Complexity: O(3N)
# Space Complexity: O(2N)

def candy(ratings):
    n= len(ratings)
    left= [1] * n
    right= [1] * n
    for i in range(1, n):
        if ratings[i]>ratings[i-1]:
            left[i]= left[i-1]+1
        else:
            left[i]= 1
    for i in range(n-2, -1, -1):
        if ratings[i]>ratings[i+1]:
            right[i]= right[i+1]+1
        else:
            right[i]= 1
    ans= 0
    for i in range(n):
        ans+= max(left[i], right[i])
    return ans
```


```python
# optimizing space

# Time Complexity: O(2N)
# Space Complexity: O(N)

def candy(ratings):
    n= len(ratings)
    left= [1] * n
    for i in range(1, n):
        if ratings[i]>ratings[i-1]:
            left[i]= left[i-1]+1
        else:
            left[i]= 1
    curr, right= 1, 1
    sum= max(left[n-1], 1)
    for i in range(n-2, -1, -1):
        if ratings[i]>ratings[i+1]:
            curr= right + 1
        else:
            curr= 1
        right= curr
        sum+= max(curr, left[i])
    return sum
```


```python
# optimal approach

# Time Complexity: O(N)
# Space Complexity: O(1)

def candy(ratings):
    i, sum= 1, 1
    n= len(ratings)
    while i<n:
        while i<n and ratings[i]==ratings[i-1]:
            sum+=1
            i+=1
        peak= 1
        while i<n and ratings[i]>ratings[i-1]:
            peak+=1
            sum+=peak
            i+=1
        down= 1
        while i<n and ratings[i]<ratings[i-1]:
            sum+=down
            down+=1
            i+=1
        if down>peak:
            sum+=down-peak
    return sum
```


```python
# insert intervals

# T.C O(n) S.C O(n)

def insert(intervals, newInterval):
    n= len(intervals)
    ans= []
    i= 0
    # left
    while i<n and newInterval[0]>intervals[i][1]:
        ans.append(intervals[i][:])
        i+=1
    # mid
    start, end= newInterval[0], newInterval[1]
    while i<n and newInterval[1]>=intervals[i][0]:
        start= min(start, intervals[i][0])
        end= max(end, intervals[i][1])
        i+=1
    ans.append([start,end])
    # right
    while i<n:
        ans.append(intervals[i][:])
        i+=1
    return ans
```


```python
# merge intervals

def merge(intervals):
    n= len(intervals)
    ans= []
    # sort the intervals in ascending order
    i= 0
    intervals.sort(key=lambda x: x[0])
    while i<n:
        j= i+1
        start, end= intervals[i][0], intervals[i][1]
        while j<n and intervals[j][0]<=end:
            end= max(end, intervals[j][1])
            j+=1
        i= j
        ans.append([start,end])
    return ans
```


```python
# non-overlapping intervals

def findNonOverlapping(intervals):
    n= len(intervals)
    intervals.sort(key=lambda x: x[1])
    count= 1
    lastEndTime= intervals[0][1]
    for i in range(1,n):
        if intervals[i][0]>=lastEndTime:
            count+=1
            lastEndTime= intervals[i][1]
    return n-count
```
