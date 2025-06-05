# Sliding Window 

when the problem requires examining contiguous subarrays or substrings to find an optimal result (max/min/length/count).

---

## 🔁 Fixed-Size Sliding Window

### Example: Maximum Sum Subarray of Size K
```python
def max_sum_subarray(arr, k):
    max_sum = 0
    window_sum = 0
    for i in range(len(arr)):
        window_sum += arr[i]  # expand window
        if i >= k - 1:
            max_sum = max(max_sum, window_sum)
            window_sum -= arr[i - k + 1]  # shrink window
    return max_sum
```

---

## 🔁 Variable-Size Sliding Window

### Example: Smallest Subarray with Given Sum
```python
def smallest_subarray_with_given_sum(s, arr):
    window_sum = 0
    min_length = float('inf')
    window_start = 0

    for window_end in range(len(arr)):
        window_sum += arr[window_end]  # expand
        while window_sum >= s:
            min_length = min(min_length, window_end - window_start + 1)
            window_sum -= arr[window_start]  # shrink
            window_start += 1
    return min_length if min_length != float('inf') else 0
```

---

### Example: Longest Substring with K Distinct Characters
```python
def longest_substring_k_distinct(s, k):
    window_start = 0
    max_length = 0
    char_freq = {}

    for window_end in range(len(s)):
        right_char = s[window_end]
        char_freq[right_char] = char_freq.get(right_char, 0) + 1

        while len(char_freq) > k:
            left_char = s[window_start]
            char_freq[left_char] -= 1
            if char_freq[left_char] == 0:
                del char_freq[left_char]
            window_start += 1
        max_length = max(max_length, window_end - window_start + 1)
    return max_length
```

---

### General Template

```python
def sliding_window(arr, condition):
    window_start = 0
    window_state = ...
    result = ...

    for window_end in range(len(arr)):
        # Expand window by including arr[window_end]
        ...

        while not condition:
            # Shrink window from the start
            ...
            window_start += 1

        # Update result based on current window
        ...

    return result
```

---

## 💡 Other Key Problems Using Sliding Window

| Problem | Description |
|--------|-------------|
| **Fruits into Baskets** | Max length of subarray with at most 2 types of fruits. |
| **No-repeat Substring** | Longest substring with all unique characters. |
| **Longest Substring with Same Letters after Replacement** | Max length of substring with at most k replacements to make all chars same. |
| **Longest Subarray with Ones after Replacement** | Replace at most k 0s to get longest subarray of 1s. |
| **Permutation in a String** | Check if string contains permutation of pattern using char frequency + sliding window. |
| **String Anagrams** | Find all anagram start indices in text using frequency maps. |
| **Smallest Window containing Substring** | Find minimum length substring containing all characters of a pattern. |
| **Words Concatenation** | Find starting indices of all concatenated words in text. |

---

Let me know if you want any of the problems coded step-by-step!
