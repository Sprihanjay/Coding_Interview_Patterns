# Two Pointers problems that involve scanning from both ends of a sorted array or finding pairs.

## Classic Two-Pointers Pattern

```python
def two_pointers_template(arr, target):
    arr.sort()  # If array is not sorted and sorting is allowed
    left = 0
    right = len(arr) - 1

    while left < right:
        current_sum = arr[left] + arr[right]

        if current_sum == target:
            # Process the pair
            return [left, right]  # or save to results
        elif current_sum < target:
            left += 1
        else:
            right -= 1

    return []
```

## Variations

### 1. Triplet/Quadruplet Sum
```python
arr.sort()
for i in range(len(arr)):
    left = i + 1
    right = len(arr) - 1
    while left < right:
        current_sum = arr[i] + arr[left] + arr[right]
        # apply logic...
```

### 2. Comparing Strings with Backspaces
```python
def backspace_compare(S, T):
    def next_valid_char(index, string):
        skip = 0
        while index >= 0:
            if string[index] == "#":
                skip += 1
            elif skip > 0:
                skip -= 1
            else:
                return index
            index -= 1
        return index

    i, j = len(S) - 1, len(T) - 1
    while i >= 0 or j >= 0:
        i = next_valid_char(i, S)
        j = next_valid_char(j, T)

        if i < 0 and j < 0:
            return True
        if i < 0 or j < 0 or S[i] != T[j]:
            return False
        i -= 1
        j -= 1
    return True
```

### 3. Dutch National Flag (3-way Partitioning)
```python
def dutch_national_flag(arr):
    low, mid, high = 0, 0, len(arr) - 1
    while mid <= high:
        if arr[mid] == 0:
            arr[low], arr[mid] = arr[mid], arr[low]
            low += 1
            mid += 1
        elif arr[mid] == 1:
            mid += 1
        else:
            arr[mid], arr[high] = arr[high], arr[mid]
            high -= 1
```
