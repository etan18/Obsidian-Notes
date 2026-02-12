
**Search notes**:
- `bisect_left(sorted_list, num, beginning, end)`: returns index `i` where `num` would be inserted into the sorted list (built-in binary search implementation). *In the case of equality, the leftmost position is returned*
	- `bisect` does the same thing but returns the *rightmost* possible position in the case of equality
- Two-pointer technique: used for problems where you are trying to find pairs of elements in a sorted list (e.g. how many pairs of elements sum to `n`). 
	- left pointer = 0, right pointer = len(lst) - 1
	- while left < right: check condition

- **lst.sort()** (in place), **sorted(lst)** (copy)
	- N log N time complexity
	- key = sort function, reverse = True if descending (ascending default)

`import bisect`
Given a sorted list:
Bisect O(log n)
- `bisect_left(sorted_list, new_item, key=Optional_fn) --> leftmost insertion index`
- `bisect_right(sorted_list, new_item) --> rightmost insertion index`
Insort = Insert O(n) + Search O(log n) = O(n)
- `insort(sorted_list, new_item, key=Optional_search_fn) --> None` , inserts new_item into sorted_list in place
	- Does insort_right, insort_left also exists

	

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

`from collections import ...`
- **deque** (double ended queue)
	- append, pop, appendleft, popleft
	- `rotate(n)`: rotates n elements right (or left if negative)
	- `deque(maxlen=Optional_int)`: once maxlen reached, evict from other side

`import heapq`
- **heapq** (heap queue)
	- heapq.heapify(lst): list to min-heap (or heapify_max(lst))
	- heapq.heappush(heap, item)
	- heapq.heappop(heap): if heap is empty, [`IndexError`](https://docs.python.org/3/library/exceptions.html#IndexError "IndexError") is raised. To access the smallest item without popping it, use `heap[0]`.

General purpose functions (not heapq, but use heap for efficiency)
	- heapq.merge(lst, lst2, ..., key=None, reverse=False) --> iterable: merge n sorted lists 
		- If reverse=True, lsts must also be sorted in descending order
	- nlargest(n, iterable, key=None): or nsmallest

**Set**
Basic syntax: 
- `new_set = {"item", "item1", "item2"}`
- `new_set = set()` or `new_set = set(lst: List)`

Methods:
- `new_set.add(item)`
- `new_set.remove(item)`

### union find
The **disjoint set** data structure, also known as the union find data structure, stores a set of elements as a series of non-overlapping sets (each element belongs to exactly one set). There are two operations that can be performed on this structure:
- **Union**: join two disjoint sets
- **Find**: determine which set a given element belongs to

Each disjoint set is represented as a tree with **path compression** applied in the find operation. Each set is assigned a **root node** which is the parent to all other elements in the set.
![[path.png]]
**Implementation**
```
# each element begins in its own set as its own parent
parent = [i for i in elements]

def find(node):               # O(log N)
	if parent[node] != node:
		parent[node] = find(parent[node])
	
	return parent[node]

def union(node1, node2):
	root1 = find(node1)
	root2 = find(node2)
	
	parent[root2] = root1     # path is uncompressed

```

One common optimization is **union-by-rank** which stores the rank (depth of tree) and chooses to attach the shallower tree to the deeper tree, rather than vice versa, to keep the trees as shallow as possible.

Another consideration is that the above implementation requires the node labels to be $0 \dots N-1$. A label-agnostic approach may store the nodes in a hashmap. 


##### linked lists

Floyd's cycle detection algorithm ("tortoise and the hare")
- O(1) space complexity
