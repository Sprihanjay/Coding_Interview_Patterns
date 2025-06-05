# Cyclic Sort 

The **Cyclic Sort** pattern works best for problems involving **numbers in a known range**, usually `1 to N` or `0 to N-1`. The idea is to place each number at its correct index in a single pass using swapping.

---

## 🔁 Cyclic Sort (Core)

```python
def cyclic_sort(nums):
    i = 0
    while i < len(nums):
        correct_idx = nums[i] - 1
        if nums[i] != nums[correct_idx]:
            nums[i], nums[correct_idx] = nums[correct_idx], nums[i]
        else:
            i += 1
    return nums
```

---

## ✅ Find the Missing Number (Leetcode)

- **Key Idea**: One number from `0 to n` is missing.
- **Why Easy**: One-pass placement using index match.
```python
def missing_number(nums):
    i = 0
    while i < len(nums):
        if nums[i] < len(nums) and nums[i] != nums[nums[i]]:
            nums[nums[i]], nums[i] = nums[i], nums[nums[i]]
        else:
            i += 1

    for i in range(len(nums)):
        if nums[i] != i:
            return i
    return len(nums)
```

---

## ✅ Find all Missing Numbers (Leetcode)

- **Key Idea**: Some numbers `1 to N` are missing, and some may appear twice.
- **Why Easy**: Just skip duplicates while placing.
```python
def find_disappeared_numbers(nums):
    i = 0
    while i < len(nums):
        correct = nums[i] - 1
        if nums[i] != nums[correct]:
            nums[i], nums[correct] = nums[correct], nums[i]
        else:
            i += 1

    return [i + 1 for i in range(len(nums)) if nums[i] != i + 1]
```

---

## ✅ Find the Duplicate Number (Leetcode)

- **Key Idea**: One number appears twice, no missing.
- **Why Easy**: Swap until duplicate detected.
```python
def find_duplicate(nums):
    i = 0
    while i < len(nums):
        if nums[i] != nums[nums[i] - 1]:
            nums[i], nums[nums[i] - 1] = nums[nums[i] - 1], nums[i]
        else:
            if i != nums[i] - 1:
                return nums[i]
            i += 1
    return -1
```

---

## ✅ Find all Duplicate Numbers (Leetcode)

- **Key Idea**: Multiple duplicates, no missing.
- **Why Easy**: Detect misplacements.
```python
def find_duplicates(nums):
    i = 0
    while i < len(nums):
        correct = nums[i] - 1
        if nums[i] != nums[correct]:
            nums[i], nums[correct] = nums[correct], nums[i]
        else:
            i += 1
    return [nums[i] for i in range(len(nums)) if nums[i] != i + 1]
```

---

## ✅ Find the Corrupt Pair (TheCodingSimplified)

- **Key Idea**: One number duplicated, one missing.
- **Why Easy**: Simple swap mismatch yields result.
```python
def find_corrupt_numbers(nums):
    i = 0
    while i < len(nums):
        correct = nums[i] - 1
        if nums[i] != nums[correct]:
            nums[i], nums[correct] = nums[correct], nums[i]
        else:
            i += 1

    for i in range(len(nums)):
        if nums[i] != i + 1:
            return [nums[i], i + 1]
```

---

## 🔁 Find the Smallest Missing Positive Number (Leetcode)

- **Key Idea**: Unsorted array, ignore negatives/large numbers.
- **Why Medium**: Need to filter valid range while placing.
```python
def first_missing_positive(nums):
    i = 0
    while i < len(nums):
        correct = nums[i] - 1
        if 1 <= nums[i] <= len(nums) and nums[i] != nums[correct]:
            nums[i], nums[correct] = nums[correct], nums[i]
        else:
            i += 1

    for i in range(len(nums)):
        if nums[i] != i + 1:
            return i + 1
    return len(nums) + 1
```

---

## 🔁 Find the First K Missing Positive Numbers (TheCodingSimplified)

- **Key Idea**: Find first `k` missing positive numbers, consider extras after full traversal.
- **Why Hard**: Must go beyond length `n` using extra space to track missing numbers.
```python
def find_first_k_missing_positive(nums, k):
    i = 0
    n = len(nums)
    while i < n:
        correct = nums[i] - 1
        if 1 <= nums[i] <= n and nums[i] != nums[correct]:
            nums[i], nums[correct] = nums[correct], nums[i]
        else:
            i += 1

    missing = []
    extra_set = set(nums)

    for i in range(n):
        if nums[i] != i + 1 and len(missing) < k:
            missing.append(i + 1)

    i = 1
    while len(missing) < k:
        candidate = i + n
        if candidate not in extra_set:
            missing.append(candidate)
        i += 1

    return missing
```


