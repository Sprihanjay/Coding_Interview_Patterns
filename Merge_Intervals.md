# Merge Intervals 

The **Merge Intervals** pattern deals with overlapping intervals and finding optimal ways to merge, insert, or process them efficiently.

---

## ✅ Common Strategy

1. **Sort the intervals** by start time.
2. **Iterate through each interval**, and:
   - If it **overlaps** with the previous, merge them.
   - If not, just append to the result.

---

## 🔁 Merge Intervals

```python
def merge_intervals(intervals):
    if not intervals:
        return []

    # Sort by start time
    intervals.sort(key=lambda x: x[0])
    merged = [intervals[0]]

    for i in range(1, len(intervals)):
        start, end = intervals[i]
        last_end = merged[-1][1]

        if start <= last_end:
            # Overlapping — merge
            merged[-1][1] = max(last_end, end)
        else:
            # Non-overlapping — add new
            merged.append([start, end])

    return merged
```

---

## 🔁 Insert Interval

```python
def insert_interval(intervals, new_interval):
    result = []
    i = 0

    # Add all intervals before new_interval
    while i < len(intervals) and intervals[i][1] < new_interval[0]:
        result.append(intervals[i])
        i += 1

    # Merge all overlapping intervals
    while i < len(intervals) and intervals[i][0] <= new_interval[1]:
        new_interval[0] = min(new_interval[0], intervals[i][0])
        new_interval[1] = max(new_interval[1], intervals[i][1])
        i += 1
    result.append(new_interval)

    # Add the rest
    while i < len(intervals):
        result.append(intervals[i])
        i += 1

    return result
```

---

## 🔁 Intervals Intersection

```python
def interval_intersection(A, B):
    result = []
    i, j = 0, 0

    while i < len(A) and j < len(B):
        start = max(A[i][0], B[j][0])
        end = min(A[i][1], B[j][1])

        if start <= end:
            result.append([start, end])

        if A[i][1] < B[j][1]:
            i += 1
        else:
            j += 1

    return result
```

---

## 🔁 Conflicting Appointments

```python
def can_attend_all_appointments(intervals):
    intervals.sort(key=lambda x: x[0])
    for i in range(1, len(intervals)):
        if intervals[i][0] < intervals[i - 1][1]:
            return False
    return True
```



