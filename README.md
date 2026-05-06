# daa
practical 1 Write a program to sort the elements of an array using Insertion Sort and count the number of comparisons.
✅ 1. Insertion Sort
```
def insertion_sort(arr):
    comp = 0
    for i in range(1, len(arr)):
        key = arr[i]
        j = i - 1
        while j >= 0:
            comp += 1
            if arr[j] > key:
                arr[j+1] = arr[j]
                j -= 1
            else:
                break
        arr[j+1] = key
    return arr, comp

arr = list(map(int, input("Enter elements: ").split()))
sorted_arr, comp = insertion_sort(arr)
print("Sorted:", sorted_arr)
print("Comparisons:", comp)
```
practical 2
✅ 2. Merge Sort
Write a program to sort an array using Merge Sort and count comparisons.
 
```
def merge_sort(arr):
    if len(arr) <= 1:
        return arr, 0

    mid = len(arr)//2
    left, c1 = merge_sort(arr[:mid])
    right, c2 = merge_sort(arr[mid:])

    i = j = comp = 0
    merged = []

    while i < len(left) and j < len(right):
        comp += 1
        if left[i] < right[j]:
            merged.append(left[i]); i += 1
        else:
            merged.append(right[j]); j += 1

    merged += left[i:]
    merged += right[j:]

    return merged, comp + c1 + c2

arr = list(map(int, input("Enter elements: ").split()))
sorted_arr, comp = merge_sort(arr)
print("Sorted:", sorted_arr)
print("Comparisons:", comp)
```


✅ 3. Heap Sort

Question:
Write a program to sort an array using Heap Sort and count comparisons.
```
def heapify(arr, n, i, comp):
    largest = i
    l = 2*i + 1
    r = 2*i + 2

    if l < n:
        comp[0] += 1
        if arr[l] > arr[largest]:
            largest = l

    if r < n:
        comp[0] += 1
        if arr[r] > arr[largest]:
            largest = r

    if largest != i:
        arr[i], arr[largest] = arr[largest], arr[i]
        heapify(arr, n, largest, comp)

def heap_sort(arr):
    n = len(arr)
    comp = [0]

    for i in range(n//2 - 1, -1, -1):
        heapify(arr, n, i, comp)

    for i in range(n-1, 0, -1):
        arr[i], arr[0] = arr[0], arr[i]
        heapify(arr, i, 0, comp)

    return arr, comp[0]

arr = list(map(int, input("Enter elements: ").split()))
sorted_arr, comp = heap_sort(arr)
print("Sorted:", sorted_arr)
print("Comparisons:", comp)
```

✅ 4. Strassen’s Matrix Multiplication

Question:
Write a program to multiply two matrices using Strassen’s algorithm.
```
def add(A, B):
    return [[A[i][j] + B[i][j] for j in range(len(A))] for i in range(len(A))]

def sub(A, B):
    return [[A[i][j] - B[i][j] for j in range(len(A))] for i in range(len(A))]

def strassen(A, B):
    n = len(A)
    if n == 1:
        return [[A[0][0] * B[0][0]]]

    mid = n // 2
    A11 = [row[:mid] for row in A[:mid]]
    A12 = [row[mid:] for row in A[:mid]]
    A21 = [row[:mid] for row in A[mid:]]
    A22 = [row[mid:] for row in A[mid:]]

    B11 = [row[:mid] for row in B[:mid]]
    B12 = [row[mid:] for row in B[:mid]]
    B21 = [row[:mid] for row in B[mid:]]
    B22 = [row[mid:] for row in B[mid:]]

    M1 = strassen(add(A11, A22), add(B11, B22))
    M2 = strassen(add(A21, A22), B11)
    M3 = strassen(A11, sub(B12, B22))
    M4 = strassen(A22, sub(B21, B11))
    M5 = strassen(add(A11, A12), B22)
    M6 = strassen(sub(A21, A11), add(B11, B12))
    M7 = strassen(sub(A12, A22), add(B21, B22))

    C11 = add(sub(add(M1, M4), M5), M7)
    C12 = add(M3, M5)
    C21 = add(M2, M4)
    C22 = add(sub(add(M1, M3), M2), M6)

    result = []
    for i in range(mid):
        result.append(C11[i] + C12[i])
    for i in range(mid):
        result.append(C21[i] + C22[i])

    return result
n = int(input("Enter size (power of 2): "))

print("Enter Matrix A:")
A = [list(map(int, input().split())) for _ in range(n)]

print("Enter Matrix B:")
B = [list(map(int, input().split())) for _ in range(n)]

result = strassen(A, B)

print("Result Matrix:")
for row in result:
    print(row)
```

✅ 5. Radix Sort

Question:
Write a program to sort elements using Radix Sort.
```
def counting_sort(arr, exp):
    n = len(arr)
    output = [0]*n
    count = [0]*10

    for i in arr:
        count[(i//exp) % 10] += 1

    for i in range(1, 10):
        count[i] += count[i-1]

    for i in range(n-1, -1, -1):
        index = (arr[i]//exp) % 10
        output[count[index]-1] = arr[i]
        count[index] -= 1

    for i in range(n):
        arr[i] = output[i]

def radix_sort(arr):
    m = max(arr)
    exp = 1
    while m//exp > 0:
        counting_sort(arr, exp)
        exp *= 10

arr = list(map(int, input("Enter elements: ").split()))
radix_sort(arr)
print("Sorted:", arr)
```

✅ 6. Bucket Sort

Question:
Write a program to sort elements using Bucket Sort.
```
def bucket_sort(arr):
    n = len(arr)
    buckets = [[] for _ in range(n)]

    for x in arr:
        index = int(x * n)
        buckets[index].append(x)

    for b in buckets:
        b.sort()

    result = []
    for b in buckets:
        result.extend(b)

    return result

arr = list(map(float, input("Enter elements (0-1): ").split()))
print("Sorted:", bucket_sort(arr))
```

✅ 7. BFS

Question:
Display data stored in a graph using Breadth-First Search.
```
from collections import deque

def bfs(graph, start):
    visited = set()
    queue = deque([start])

    while queue:
        node = queue.popleft()
        if node not in visited:
            print(node, end=" ")
            visited.add(node)
            queue.extend(graph[node])

graph = {'A':['B','C'], 'B':['D'], 'C':['E'], 'D':[], 'E':[]}
bfs(graph, 'A')
```
✅ 8. DFS

Question:
Display data stored in a graph using Depth-First Search.
```
def dfs(graph, node, visited=set()):
    if node not in visited:
        print(node, end=" ")
        visited.add(node)
        for n in graph[node]:
            dfs(graph, n, visited)

graph = {'A':['B','C'], 'B':['D'], 'C':['E'], 'D':[], 'E':[]}
dfs(graph, 'A')
```

✅ 9. Prim’s Algorithm

Question:
Write a program to find Minimum Spanning Tree using Prim’s algorithm.
```
import heapq

def prim(graph, start):
    visited = set([start])
    edges = [(cost, start, to) for to, cost in graph[start]]
    heapq.heapify(edges)

    mst = []

    while edges:
        cost, frm, to = heapq.heappop(edges)
        if to not in visited:
            visited.add(to)
            mst.append((frm, to, cost))
            for next_to, next_cost in graph[to]:
                heapq.heappush(edges, (next_cost, to, next_to))

    return mst
graph = {
    'A': [('B', 2), ('C', 3)],
    'B': [('A', 2), ('C', 1), ('D', 4)],
    'C': [('A', 3), ('B', 1), ('D', 5)],
    'D': [('B', 4), ('C', 5)]
}

start = 'A'
cost = prim(graph, start)

print("Minimum Cost of MST:", cost)

```
✅ 10. Dijkstra’s Algorithm

Question:
Find shortest path from a source node using Dijkstra’s algorithm.

```
import heapq

def dijkstra(graph, start):
    dist = {v: float('inf') for v in graph}
    dist[start] = 0
    pq = [(0, start)]

    while pq:
        d, node = heapq.heappop(pq)
        for neighbor, weight in graph[node]:
            if dist[neighbor] > d + weight:
                dist[neighbor] = d + weight
                heapq.heappush(pq, (dist[neighbor], neighbor))

    return dist
graph = {
    'A': [('B', 1), ('C', 4)],
    'B': [('A', 1), ('C', 2), ('D', 5)],
    'C': [('A', 4), ('B', 2), ('D', 1)],
    'D': [('B', 5), ('C', 1)]
}

start = 'A'

distances = dijkstra(graph, start)

print("Shortest distances:")
for node in distances:
    print(node, ":", distances[node])
```

✅ 11. Weighted Interval Scheduling (Greedy)

Question:
Write a program to solve weighted interval scheduling (basic greedy version).
```
def interval_scheduling(intervals):
    intervals.sort(key=lambda x: x[1])
    result = [intervals[0]]

    for i in intervals[1:]:
        if i[0] >= result[-1][1]:
            result.append(i)

    return result

intervals = [(1,3), (2,5), (4,6), (6,7)]
print(interval_scheduling(intervals))
```

✅ 12. 0/1 Knapsack

Question:
Write a program to solve the 0/1 Knapsack problem.
```
def knapsack(W, wt, val, n):
    dp = [[0]*(W+1) for _ in range(n+1)]

    for i in range(1, n+1):
        for w in range(W+1):
            if wt[i-1] <= w:
                dp[i][w] = max(val[i-1] + dp[i-1][w-wt[i-1]], dp[i-1][w])
            else:
                dp[i][w] = dp[i-1][w]

    return dp[n][W]

val = [60, 100, 120]
wt = [10, 20, 30]
W = 50
print("Max value:", knapsack(W, wt, val, len(val)))
```


 ques 13 Write a program to sort the elements of an array using Quick Sort (The program should report the number of comparisons).
```
def quick_sort(arr):
    comparisons = 0

    def partition(low, high):
        nonlocal comparisons
        pivot = arr[high]
        i = low - 1

        for j in range(low, high):
            comparisons += 1
            if arr[j] < pivot:
                i += 1
                arr[i], arr[j] = arr[j], arr[i]

        arr[i + 1], arr[high] = arr[high], arr[i + 1]
        return i + 1

    def quicksort(low, high):
        if low < high:
            pi = partition(low, high)

            quicksort(low, pi - 1)
            quicksort(pi + 1, high)

    quicksort(0, len(arr) - 1)
    return arr, comparisons


# Input from user
arr = list(map(int, input("Enter elements: ").split()))

sorted_arr, comp = quick_sort(arr)

print("Sorted array:", sorted_arr)
print("Number of comparisons:", comp)
```
ques 14Write a program to sort the elements of an array using Count Sort.

```
def count_sort(arr):
    # Find maximum element
    max_element = max(arr)

    # Create count array
    count = [0] * (max_element + 1)

    # Store frequency of each element
    for num in arr:
        count[num] += 1

    # Build sorted array
    sorted_arr = []

    for i in range(len(count)):
        while count[i] > 0:
            sorted_arr.append(i)
            count[i] -= 1

    return sorted_arr


# Input from user
arr = list(map(int, input("Enter elements: ").split()))

# Perform Count Sort
sorted_arr = count_sort(arr)

# Display result
print("Sorted array:", sorted_arr)

```
