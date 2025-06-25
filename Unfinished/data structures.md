
**Search notes**:
- `bisect_left(sorted_list, num, beginning, end)`: returns index `i` where `num` would be inserted into the sorted list (built-in binary search implementation). *In the case of equality, the leftmost position is returned*
	- `bisect` does the same thing but returns the *rightmost* possible position in the case of equality
- Two-pointer technique: used for problems where you are trying to find pairs of elements in a sorted list (e.g. how many pairs of elements sum to `n`). 
	- left pointer = 0, right pointer = len(lst) - 1
	- while left < right: check condition


**Heap & Priority Queue**
- `import heapq`
- `heapq.heappop(lst: List)`
- `heapq.heappush(lst: List)`

Sample usage for max heap:
```
import heapq
listForTree = [1,2,3,4,5,6,7,8,9,10,11,12,13,14,15]    
heapq.heapify(listForTree)             # for a min heap
heapq._heapify_max(listForTree)        # for a maxheap!!
```


**Set**
Basic syntax: 
- `new_set = {"item", "item1", "item2"}`
- `new_set = set()` or `new_set = set(lst: List)`

Methods:
- `new_set.add(item)`
- `new_set.remove(item)`

