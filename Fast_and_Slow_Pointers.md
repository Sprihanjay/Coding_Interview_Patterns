# Fast and Slow Pointers Template

Use this pattern when you need to detect cycles, remove duplicates, or work on problems involving relative motion through an array or linked list.

## 1. Cycle Detection (Floyd's Tortoise and Hare)

```python
def has_cycle(head):
    slow = fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow == fast:
            return True
    return False
```

## 2. Length of the Cycle

```python
def cycle_length(head):
    slow = fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow == fast:
            length = 1
            current = slow.next
            while current != slow:
                current = current.next
                length += 1
            return length
    return 0
```

## 3. Start of Cycle in Linked List

```python
def detect_cycle_start(head):
    slow = fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow == fast:
            # find start
            slow = head
            while slow != fast:
                slow = slow.next
                fast = fast.next
            return slow
    return None
```

## 4. Remove Duplicates In-place from Sorted Array

```python
def remove_duplicates(arr):
    if not arr:
        return 0
    slow = 0
    for fast in range(1, len(arr)):
        if arr[fast] != arr[slow]:
            slow += 1
            arr[slow] = arr[fast]
    return slow + 1  # new length
```
