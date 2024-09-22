# Algorithm

## Binary Search

```python
def binary_search(target, arr):
    low = 0
    hi = len(arr) - 1
    while low <= hi:
        mid = (low + hi) // 2
        if arr[mid] == target:
            return True
        elif arr[mid] < target:
            low = mid+1
        else:
            hi = mid-1
    return False
```

## Bubble Sort

- slowest
- easiest to code
- useful for quick script when array is small
- O(n^2)

```python
def bubble_sort(nums):
    swapping = True
    end = len(nums)
    while swapping:
        swapping = False
        for i in range (1, end):
            if nums[i-1] > nums[i]:
                temp = nums[i]
                nums[i] = nums[i-1]
                nums[i-1] = temp
                swapping = True
        end -= 1
    return nums
    pass
```

### Divide and Conquer

- Divide: divide the large problem into smaller problems, and recursively solve the smaller problems
- Conquer: Combine the results of the smaller problems to solve the large problem

## Merge Sort

- recursive -> resource overheat
- stable
- a bit faster than bubble sort
- divide and conquer
- require extra memory
- O(n log(n))

```python
def merge_sort(nums):
    if len(nums) < 2:
        return nums
    mid = len(nums) // 2
    sorted_left_side = merge_sort(nums[:mid])
    sorted_right_side = merge_sort(nums[mid:])

    return merge(sorted_left_side, sorted_right_side)
    pass


def merge(first, second):
    final = []
    i = 0
    j = 0

    while i < len(first) and j < len(second):
        if first[i] < second[j]:
            final.append(first[i])
            i += 1
        else:
            final.append(second[j])
            j += 1


    final.extend(first[i:])
    final.extend(second[j:])
    return final
    pass
```

## Insertion Sort

- good with small array
- O(n^2) best case is O(n) when array is sorted (wtf?)
- faster than bubble sort
- fast for partially sorted array

```python
def insertion_sort(nums):
    for i in range(0, len(nums)):
        j = i
        while j > 0 and nums[j-1] > nums[j]:
            temp = nums[j]
            nums[j] = nums[j-1]
            nums[j-1] = temp
            j -= 1
    return nums
    pass
```

## Quick Sort

- O(n log(n)) averagely, O(n^2) at worst caused by already sorted list
- very fast in average case but not stable
- ensure O(n log(n)) by randomize the array
- or the median approach is used to ensure that worst-case complexity is impossible

```python
def quick_sort(nums, low, high):
    if low < high:
        i = partition(nums, low, high)
        quick_sort(nums, low, i-1)
        quick_sort(nums, i+1, high)
    pass


def partition(nums, low, high):
    pivot = nums[high]
    i = low
    for j in range(low, high):
        if nums[j] < pivot:
            tmp = nums[j]
            nums[j] = nums[i]
            nums[i] = tmp
            i += 1
    tmp = nums[i]
    nums[i] = nums[high]
    nums[high] = tmp
    return i
    pass
```

## Selection Sort

- slightly better than bubble sort

```python
def selection_sort(nums):
    for i in range(0, len(nums)):
        smallest = i
        for j in range(smallest + 1, len(nums)):
            if nums[j] < nums[smallest]:
                smallest = j
        tmp = nums[i]
        nums[i] = nums[smallest]
        nums[smallest] = tmp
    return nums
    pass
```

## Polynomial Time Fibonacci

```python
def fib(n):
    if n == 0:
        return 0
    grand_parent = 0
    parent = 1
    current = 1
    for i in range(0, n-1):
        current = parent + grand_parent
        temp = parent
        parent = current
        grand_parent = temp
    return current
```

## Power Set

```python
def power_set(input_set):
    if len(input_set) == 0:
        return [[]]

    sets = power_set(input_set[1:])
    final = []
    for set in sets:
       final.append([input_set[0]] + set)
       final.append(set)

    return final
    pass
```

## Prime Factorial

```python
def prime_factors(n):
    prime_factors = []
    while n % 2 == 0:
        n /= 2
        prime_factors.append(2)
    for i in range(3, int(math.sqrt(n)) + 1, 2):
        while n % i == 0:
            n /= i
            prime_factors.append(i)
    if n > 2:
        prime_factors.append(int(n))
    return prime_factors
```

## Parenthesis

```python
def is_balanced(input_str):
    stack = Stack() // this could be just an array
    for i in input_str:
        if i == "(":
            stack.push(i) // append
        elif i == ")" and stack.peek() == "(":
            stack.pop() // pop
        else:
            return False
    if len(stack.items) != 0:
        return False
    else:
        return True

    pass
```

## end
