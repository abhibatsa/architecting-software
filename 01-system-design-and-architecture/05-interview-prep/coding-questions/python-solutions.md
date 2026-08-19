# Python Solutions

All 15 problems, solved and explained. See [`README.md`](./README.md) for
difficulty and pattern index.

---

## 1. Two Sum (Easy)

**Problem:** Given an array of integers and a target, return indices of
the two numbers that add up to the target. Assume exactly one solution.

```python
def two_sum(nums, target):
    seen = {}  # value -> index
    for i, num in enumerate(nums):
        complement = target - num
        if complement in seen:
            return [seen[complement], i]
        seen[num] = i
    return []  # no solution found
```

**Explanation:** The naive approach checks every pair — O(n²). Instead,
walk the array once, and for each number check if its *complement*
(target - num) was already seen. A hash map gives O(1) average lookup, so
the whole thing runs in O(n) time, O(n) space.

**SDET angle:** test duplicate values (`[3,3]`, target `6`), no valid pair,
and negative numbers.

---

## 2. Valid Parentheses (Easy)

**Problem:** Given a string of `()[]{}`` characters, determine if the
brackets are validly matched and nested.

```python
def is_valid(s):
    stack = []
    pairs = {')': '(', ']': '[', '}': '{'}
    for char in s:
        if char in pairs:
            if not stack or stack.pop() != pairs[char]:
                return False
        else:
            stack.append(char)
    return not stack  # stack must be empty at the end
```

**Explanation:** Every opening bracket gets pushed. Every closing bracket
must match the most recently opened one — that's exactly what a stack
gives you (LIFO). If a closing bracket doesn't match the top of the stack,
or the stack's empty when we hit a closer, it's invalid. At the end, an
empty stack means everything was matched.

**SDET angle:** test empty string (valid), unmatched closer with empty
stack, and non-bracket characters if the input isn't guaranteed clean.

---

## 3. Reverse a Linked List (Easy)

**Problem:** Reverse a singly linked list in place.

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

def reverse_list(head):
    prev = None
    curr = head
    while curr:
        next_node = curr.next   # save before overwriting
        curr.next = prev        # reverse the pointer
        prev = curr             # advance prev
        curr = next_node        # advance curr
    return prev  # prev is the new head
```

**Explanation:** Three pointers do the work: `prev` (what's been reversed
so far), `curr` (the node being processed), and a temporary `next_node` to
avoid losing the rest of the list once we overwrite `curr.next`. Runs in
O(n) time, O(1) space — no new list allocated.

**SDET angle:** test empty list (`head=None`), single-node list, and
verify the original list's tail correctly becomes `None`-terminated at the
new tail.

---

## 4. Binary Search (Easy)

**Problem:** Given a sorted array, find the index of a target value, or -1.

```python
def binary_search(nums, target):
    left, right = 0, len(nums) - 1
    while left <= right:
        mid = left + (right - left) // 2  # avoids overflow in other languages
        if nums[mid] == target:
            return mid
        elif nums[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return -1
```

**Explanation:** Halve the search space every iteration by comparing the
midpoint to the target — O(log n) instead of O(n). The
`left + (right - left) // 2` form (instead of `(left + right) // 2`) is a
habit worth keeping even in Python, where integer overflow isn't a real
concern — it's the version that ports cleanly to Java/C++ where it matters.

**SDET angle:** test empty array, target not present, target at index 0
and at the last index (classic off-by-one traps).

---

## 5. First Unique Character in a String (Easy)

**Problem:** Given a string, return the index of the first character that
doesn't repeat. Return -1 if none exists.

```python
from collections import Counter

def first_uniq_char(s):
    counts = Counter(s)
    for i, char in enumerate(s):
        if counts[char] == 1:
            return i
    return -1
```

**Explanation:** Count every character's frequency first (one pass), then
walk the string again looking for the first character whose count is 1.
Two O(n) passes, O(1) extra space if you treat the alphabet as fixed-size
(26 lowercase letters) — otherwise O(k) for k distinct characters.

**SDET angle:** test empty string, all-repeating string (returns -1), and
Unicode input if the interviewer doesn't restrict to ASCII.

---

## 6. Merge Intervals (Medium)

**Problem:** Given a list of intervals, merge all overlapping ones.

```python
def merge(intervals):
    if not intervals:
        return []
    intervals.sort(key=lambda x: x[0])
    merged = [intervals[0]]
    for current in intervals[1:]:
        last = merged[-1]
        if current[0] <= last[1]:  # overlaps
            last[1] = max(last[1], current[1])
        else:
            merged.append(current)
    return merged
```

**Explanation:** Sort by start time first — once sorted, overlapping
intervals are always adjacent, so a single linear sweep merges them.
Compare each interval's start to the *last merged interval's* end: if it
overlaps, extend the end; otherwise, start a new merged interval. O(n log n)
from the sort dominates; the sweep itself is O(n).

**SDET angle:** test fully nested intervals (`[1,10]` and `[2,3]`),
touching-but-not-overlapping intervals (`[1,2]`, `[2,3]` — should merge),
and a single interval.

---

## 7. Group Anagrams (Medium)

**Problem:** Group a list of strings into anagram sets.

```python
from collections import defaultdict

def group_anagrams(strs):
    groups = defaultdict(list)
    for s in strs:
        key = ''.join(sorted(s))  # canonical form
        groups[key].append(s)
    return list(groups.values())
```

**Explanation:** Two strings are anagrams if and only if their sorted
characters are identical — so the sorted string becomes a canonical key.
Group everything by that key. Sorting each string is O(k log k) for length
k, across n strings: O(n · k log k) overall.

**SDET angle:** test empty strings (they're all anagrams of each other),
case sensitivity (`"Eat"` vs `"eat"` — are they anagrams here or not,
depends on spec), and single-character strings.

---

## 8. Longest Substring Without Repeating Characters (Medium)

**Problem:** Given a string, find the length of the longest substring
without repeating characters.

```python
def length_of_longest_substring(s):
    seen = {}  # char -> most recent index
    left = 0
    longest = 0
    for right, char in enumerate(s):
        if char in seen and seen[char] >= left:
            left = seen[char] + 1  # shrink window past the repeat
        seen[char] = right
        longest = max(longest, right - left + 1)
    return longest
```

**Explanation:** Sliding window: expand `right` one character at a time.
If that character was already seen *inside the current window*, shrink
`left` to just past its last occurrence — this is the part people get
wrong: only shrink if the previous occurrence is still inside the window
(`seen[char] >= left`), not just "if seen anywhere in the string." One
pass, O(n) time, O(min(n, alphabet size)) space.

**SDET angle:** test empty string, all-same-character string (`"aaaa"` →
answer is 1), and a string with no repeats at all.

---

## 9. Linked List Cycle Detection (Medium)

**Problem:** Determine if a linked list has a cycle, without extra space.

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

**Explanation:** Floyd's cycle detection ("tortoise and hare"). Two
pointers move through the list at different speeds — if there's a cycle,
the faster pointer eventually laps the slower one and they meet; if there's
no cycle, `fast` hits the end (`None`) first. O(n) time, O(1) space — no
extra hash set needed to track visited nodes.

**SDET angle:** test an empty list, a single self-referencing node
(cycle of length 1), and a list with no cycle at all.

---

## 10. LRU Cache (Medium — design)

**Problem:** Design a cache with `get(key)` and `put(key, value)`, both
O(1), that evicts the least-recently-used item when capacity is exceeded.

```python
from collections import OrderedDict

class LRUCache:
    def __init__(self, capacity):
        self.capacity = capacity
        self.cache = OrderedDict()

    def get(self, key):
        if key not in self.cache:
            return -1
        self.cache.move_to_end(key)  # mark as recently used
        return self.cache[key]

    def put(self, key, value):
        if key in self.cache:
            self.cache.move_to_end(key)
        self.cache[key] = value
        if len(self.cache) > self.capacity:
            self.cache.popitem(last=False)  # evict least recently used
```

**Explanation:** Python's `OrderedDict` already tracks insertion order and
supports O(1) move-to-end and pop-from-front — exactly what LRU needs, so
it's a legitimate production-quality solution, not just an interview
shortcut. (Worth knowing the "from scratch" version too — a hash map +
doubly linked list — since some interviewers explicitly disallow
`OrderedDict` to test whether you understand *why* it works.)

**SDET angle:** the real test surface here is state mutation over a
sequence of calls — test capacity-1 cache, evicting immediately after a
`get` (does the get correctly refresh recency?), and overwriting an
existing key's value.

---

## 11. Median of Two Sorted Arrays (Hard)

**Problem:** Given two sorted arrays, find the median of the combined
array in O(log(min(m,n))) time.

```python
def find_median_sorted_arrays(nums1, nums2):
    if len(nums1) > len(nums2):
        nums1, nums2 = nums2, nums1  # ensure nums1 is the shorter array
    m, n = len(nums1), len(nums2)
    left, right = 0, m
    half = (m + n + 1) // 2

    while left <= right:
        i = (left + right) // 2       # partition point in nums1
        j = half - i                  # partition point in nums2

        nums1_left = nums1[i - 1] if i > 0 else float('-inf')
        nums1_right = nums1[i] if i < m else float('inf')
        nums2_left = nums2[j - 1] if j > 0 else float('-inf')
        nums2_right = nums2[j] if j < n else float('inf')

        if nums1_left <= nums2_right and nums2_left <= nums1_right:
            if (m + n) % 2 == 1:
                return max(nums1_left, nums2_left)
            return (max(nums1_left, nums2_left) + min(nums1_right, nums2_right)) / 2
        elif nums1_left > nums2_right:
            right = i - 1
        else:
            left = i + 1
```

**Explanation:** The brute-force merge-and-find-middle is O(m+n) — this
problem specifically wants better. The trick: binary search for a
*partition point* in the shorter array such that everything to the left of
the combined partition is ≤ everything to the right. Once that partition
is correct, the median is directly derivable from the four boundary
values, without ever merging the arrays.

**SDET angle:** test one empty array, arrays of very different lengths,
and both even and odd total-length combined arrays (the median formula
differs).

---

## 12. Word Ladder (Hard)

**Problem:** Given a start word, end word, and a word list, find the
length of the shortest transformation sequence changing one letter at a
time, where every intermediate word is in the list.

```python
from collections import deque

def ladder_length(begin_word, end_word, word_list):
    word_set = set(word_list)
    if end_word not in word_set:
        return 0

    queue = deque([(begin_word, 1)])
    while queue:
        word, steps = queue.popleft()
        if word == end_word:
            return steps
        for i in range(len(word)):
            for c in 'abcdefghijklmnopqrstuvwxyz':
                next_word = word[:i] + c + word[i + 1:]
                if next_word in word_set:
                    word_set.remove(next_word)  # mark visited
                    queue.append((next_word, steps + 1))
    return 0
```

**Explanation:** Model this as a graph where each word is a node, and an
edge exists between two words that differ by exactly one letter. The
shortest transformation sequence is then just shortest-path — BFS, since
BFS naturally finds shortest paths in an unweighted graph. Generating all
possible one-letter-changed words per step (26 × word length) and checking
set membership is the practical way to build edges without precomputing
the whole graph.

**SDET angle:** test no path exists (returns 0), begin word equals end
word, and end word not in the word list.

---

## 13. Serialize and Deserialize Binary Tree (Hard)

**Problem:** Design an algorithm to serialize a binary tree to a string
and deserialize it back to the original tree structure.

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

def serialize(root):
    def dfs(node):
        if not node:
            vals.append('#')
            return
        vals.append(str(node.val))
        dfs(node.left)
        dfs(node.right)
    vals = []
    dfs(root)
    return ','.join(vals)

def deserialize(data):
    vals = iter(data.split(','))
    def dfs():
        val = next(vals)
        if val == '#':
            return None
        node = TreeNode(int(val))
        node.left = dfs()
        node.right = dfs()
        return node
    return dfs()
```

**Explanation:** Pre-order DFS (node, then left, then right), marking
missing children with a sentinel (`'#'`). This ordering matters — pre-order
is what makes deserialization straightforward, because the first value in
any subtree's serialization is always that subtree's root. Deserializing
just replays the same traversal order, consuming values one at a time.

**SDET angle:** test an empty tree (`root=None`), a single-node tree, and
round-trip correctness — serialize then deserialize then serialize again,
confirm the string matches.

---

## 14. Trapping Rain Water (Hard)

**Problem:** Given an array representing elevation heights, compute how
much water it can trap after raining.

```python
def trap(height):
    if not height:
        return 0
    left, right = 0, len(height) - 1
    left_max, right_max = height[left], height[right]
    water = 0
    while left < right:
        if left_max <= right_max:
            left += 1
            left_max = max(left_max, height[left])
            water += left_max - height[left]
        else:
            right -= 1
            right_max = max(right_max, height[right])
            water += right_max - height[right]
    return water
```

**Explanation:** Water trapped at any index is
`min(max_height_to_the_left, max_height_to_the_right) - height[index]`.
Instead of precomputing left-max and right-max arrays (O(n) space), two
pointers moving inward track the running max from each side — whichever
side has the smaller max is the side that's safe to resolve, because the
water level there is bounded by that smaller max regardless of what's
further past the taller side. O(n) time, O(1) space.

**SDET angle:** test a flat array (0 water), a strictly increasing or
decreasing array (0 water), and a single-element array.

---

## 15. Merge K Sorted Lists (Hard)

**Problem:** Merge k sorted linked lists into one sorted linked list.

```python
import heapq

class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

def merge_k_lists(lists):
    heap = []
    for i, node in enumerate(lists):
        if node:
            heapq.heappush(heap, (node.val, i, node))

    dummy = ListNode()
    curr = dummy
    while heap:
        val, i, node = heapq.heappop(heap)
        curr.next = node
        curr = curr.next
        if node.next:
            heapq.heappush(heap, (node.val, i, node.next))  # note: reuse i, next node's val
    return dummy.next
```

**Explanation:** A min-heap holds one node per list at a time (the current
"front runner" from each list). Repeatedly pop the smallest, append it to
the result, and push that list's next node. The list index `i` is included
in the heap tuple purely to break ties when two nodes have equal values —
Python can't compare `ListNode` objects directly. Runs in O(N log k) where
N is total nodes across all lists and k is the number of lists — better
than the O(N log N) of dumping everything into one array and sorting.

**SDET angle:** test an empty input list (`lists=[]`), lists containing
some empty linked lists mixed with non-empty ones, and duplicate values
across different lists (tests the tie-breaking).

---

*Java versions: [`java-solutions.md`](./java-solutions.md)*
