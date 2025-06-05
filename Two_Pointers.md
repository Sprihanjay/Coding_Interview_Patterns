'''
TWO POINTERS
------------------------------
Solves sorted array pair sums, removing duplicates, triplets/quads, or string problems with backspaces.
'''

def two_pointers_template(arr):
    # If applicable, sort the array (only if order doesn't matter and it's not already sorted)
    # arr.sort()

    left = 0
    right = len(arr) - 1

    while left < right:
        # Example operation: calculate the sum of values at both pointers
        current_sum = arr[left] + arr[right]

        if current_sum == target:
            # Found a valid pair (or satisfy some condition)
            return [left, right]  # or store result, or increment counters

        elif current_sum < target:
            # Move left pointer to increase the sum
            left += 1
        else:
            # Move right pointer to decrease the sum
            right -= 1

    # Return result depending on problem (boolean, list, count, etc.)
    return []  # or -1, False, or result variable

'''
🔁 Variants:
-----------
- For **removal or in-place update**:
  - use `slow` and `fast` pointer pattern

- For **strings or backspace compare**:
  - start from end of both strings and move backward

- For **triplet or quad problems**:
  - outer loop fixes first element(s), inner uses two pointers

- For **subarray/window problems**:
  - expand with `right`, shrink with `left` when condition breaks
'''

def slow_fast_pointer_template(arr):
    # Example: remove duplicates
    slow = 0
    for fast in range(1, len(arr)):
        if arr[fast] != arr[slow]:
            slow += 1
            arr[slow] = arr[fast]
    return slow + 1  # New length


def sliding_window_template(arr, condition):
    left = 0
    result = 0
    window_state = 0  # e.g. product, sum, char count, etc.

    for right in range(len(arr)):
        # expand window: update state
        # while condition not met: shrink from left
        while left <= right and not condition:
            # shrink window: undo arr[left]
            left += 1

        # use window (e.g. count, store, etc.)
        result += right - left + 1

    return result
