```python
# --- Simple Binary Search ---
def binary_search_iterative(arr, target):
    """
    Perform binary search on a sorted array to check if target exists.
    Time: O(logN), Space: O(1)

    Example:
    binary_search_iterative([1, 2, 3, 4, 5], 3) -> True
    binary_search_iterative([1, 2, 3, 4, 5], 6) -> False
    """
    left, right = 0, len(arr) - 1
    while left <= right:
        mid = left + (right - left) // 2
        if arr[mid] == target:
            return True
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return False

# --- Order-Agnostic Binary Search ---
def order_agnostic_binary_search(arr, key):
    """
    Binary search on a sorted array which may be in ascending or descending order.
    Time: O(logN), Space: O(1)

    Examples:
    order_agnostic_binary_search([4, 6, 10], 10) -> 2
    order_agnostic_binary_search([10, 6, 4], 10) -> 0
    """
    start, end = 0, len(arr) - 1
    is_ascending = arr[start] < arr[end]

    while start <= end:
        mid = start + (end - start) // 2
        if arr[mid] == key:
            return mid
        if is_ascending:
            if key < arr[mid]:
                end = mid - 1
            else:
                start = mid + 1
        else:
            if key > arr[mid]:
                end = mid - 1
            else:
                start = mid + 1
    return -1

# --- Ceiling of a Number ---
def search_ceiling_of_a_number(arr, key):
    """
    Finds the index of the smallest element >= key in a sorted array.
    Time: O(logN), Space: O(1)

    Examples:
    search_ceiling_of_a_number([4, 6, 10], 6) -> 1
    search_ceiling_of_a_number([1, 3, 8, 10, 15], 12) -> 4
    search_ceiling_of_a_number([4, 6, 10], 17) -> -1
    """
    if key > arr[-1]:
        return -1
    start, end = 0, len(arr) - 1
    while start <= end:
        mid = start + (end - start) // 2
        if key == arr[mid]:
            return mid
        elif key < arr[mid]:
            end = mid - 1
        else:
            start = mid + 1
    return start

# --- Floor of a Number ---
def search_floor_of_a_number(arr, key):
    """
    Finds the index of the largest element <= key in a sorted array.
    Time: O(logN), Space: O(1)

    Examples:
    search_floor_of_a_number([4, 6, 10], 6) -> 1
    search_floor_of_a_number([1, 3, 8, 10, 15], 12) -> 3
    search_floor_of_a_number([4, 6, 10], -1) -> -1
    """
    if key < arr[0]:
        return -1
    start, end = 0, len(arr) - 1
    while start <= end:
        mid = start + (end - start) // 2
        if key == arr[mid]:
            return mid
        elif key < arr[mid]:
            end = mid - 1
        else:
            start = mid + 1
    return end

# --- Next Letter (Circular) ---
def search_next_letter(letters, key):
    """
    Find the smallest letter > key in a circular sorted list of characters.
    Time: O(logN), Space: O(1)

    Examples:
    search_next_letter(['a', 'c', 'f', 'h'], 'f') -> 'h'
    search_next_letter(['a', 'c', 'f', 'h'], 'm') -> 'a'
    """
    n = len(letters)
    if key < letters[0] or key >= letters[-1]:
        return letters[0]
    start, end = 0, n - 1
    while start <= end:
        mid = start + (end - start) // 2
        if key < letters[mid]:
            end = mid - 1
        else:
            start = mid + 1
    return letters[start % n]

# --- Number Range ---
def find_range(arr, key):
    """
    Find the first and last index of a key in a sorted array.
    Time: O(logN), Space: O(1)

    Examples:
    find_range([4, 6, 6, 6, 9], 6) -> [1, 3]
    find_range([1, 3, 8, 10, 15], 12) -> [-1, -1]
    """
    return [search_index(arr, key, False), search_index(arr, key, True)]

def search_index(arr, key, find_max):
    index = -1
    start, end = 0, len(arr) - 1
    while start <= end:
        mid = start + (end - start) // 2
        if key < arr[mid]:
            end = mid - 1
        elif key > arr[mid]:
            start = mid + 1
        else:
            index = mid
            if find_max:
                start = mid + 1
            else:
                end = mid - 1
    return index

# --- Infinite Array Search ---
class ArrayReader:
    """Simulates a reader for an infinite array."""
    def __init__(self, arr):
        self.arr = arr

    def get(self, index):
        if index >= len(self.arr):
            return float('inf')
        return self.arr[index]

def search_in_infinite_array(reader, key):
    """
    Search for a key in an infinite sorted array using a simulated reader.
    Time: O(logN), Space: O(1)

    Example:
    reader = ArrayReader([1, 3, 8, 10, 15])
    search_in_infinite_array(reader, 10) -> 3
    """
    start, end = 0, 1
    while reader.get(end) < key:
        new_start = end + 1
        end += (end - start + 1) * 2
        start = new_start
    return binary_search_infinite(reader, key, start, end)

def binary_search_infinite(reader, key, start, end):
    while start <= end:
        mid = start + (end - start) // 2
        if reader.get(mid) == key:
            return mid
        elif reader.get(mid) < key:
            start = mid + 1
        else:
            end = mid - 1
    return -1

```
