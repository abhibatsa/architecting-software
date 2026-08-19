# Java Solutions

All 15 problems, solved and explained. Same patterns as the Python
versions — see [`python-solutions.md`](./python-solutions.md) for the
conceptual explanation of each; this file focuses on Java-specific notes
where the language changes the approach.

---

## 1. Two Sum (Easy)

```java
import java.util.HashMap;
import java.util.Map;

public int[] twoSum(int[] nums, int target) {
    Map<Integer, Integer> seen = new HashMap<>();
    for (int i = 0; i < nums.length; i++) {
        int complement = target - nums[i];
        if (seen.containsKey(complement)) {
            return new int[]{seen.get(complement), i};
        }
        seen.put(nums[i], i);
    }
    return new int[]{};
}
```

Same hash-map approach as Python — O(n) time, O(n) space.

---

## 2. Valid Parentheses (Easy)

```java
import java.util.Deque;
import java.util.ArrayDeque;
import java.util.Map;

public boolean isValid(String s) {
    Deque<Character> stack = new ArrayDeque<>();
    Map<Character, Character> pairs = Map.of(')', '(', ']', '[', '}', '{');
    for (char c : s.toCharArray()) {
        if (pairs.containsKey(c)) {
            if (stack.isEmpty() || stack.pop() != pairs.get(c)) {
                return false;
            }
        } else {
            stack.push(c);
        }
    }
    return stack.isEmpty();
}
```

`ArrayDeque` is the standard, more efficient choice over `Stack` in modern
Java (`Stack` is legacy and synchronized, which you don't need here).

---

## 3. Reverse a Linked List (Easy)

```java
class ListNode {
    int val;
    ListNode next;
    ListNode(int val) { this.val = val; }
}

public ListNode reverseList(ListNode head) {
    ListNode prev = null;
    ListNode curr = head;
    while (curr != null) {
        ListNode nextNode = curr.next;
        curr.next = prev;
        prev = curr;
        curr = nextNode;
    }
    return prev;
}
```

Identical pointer logic to Python — this is a language-agnostic pattern.

---

## 4. Binary Search (Easy)

```java
public int binarySearch(int[] nums, int target) {
    int left = 0, right = nums.length - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;  // prevents integer overflow
        if (nums[mid] == target) {
            return mid;
        } else if (nums[mid] < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }
    return -1;
}
```

Here `left + (right - left) / 2` isn't just style — in Java,
`(left + right) / 2` can genuinely overflow `int` when both are near
`Integer.MAX_VALUE`. This is one of the few places the "safe" version
matters more in Java than in Python.

---

## 5. First Unique Character in a String (Easy)

```java
import java.util.HashMap;
import java.util.Map;

public int firstUniqChar(String s) {
    Map<Character, Integer> counts = new HashMap<>();
    for (char c : s.toCharArray()) {
        counts.put(c, counts.getOrDefault(c, 0) + 1);
    }
    for (int i = 0; i < s.length(); i++) {
        if (counts.get(s.charAt(i)) == 1) {
            return i;
        }
    }
    return -1;
}
```

Two-pass counting, same as Python. For ASCII-only input, an `int[26]`
array is a faster alternative to a `HashMap`.

---

## 6. Merge Intervals (Medium)

```java
import java.util.Arrays;
import java.util.ArrayList;
import java.util.List;

public int[][] merge(int[][] intervals) {
    if (intervals.length == 0) return new int[0][];
    Arrays.sort(intervals, (a, b) -> a[0] - b[0]);

    List<int[]> merged = new ArrayList<>();
    merged.add(intervals[0]);
    for (int[] current : intervals) {
        int[] last = merged.get(merged.size() - 1);
        if (current[0] <= last[1]) {
            last[1] = Math.max(last[1], current[1]);
        } else {
            merged.add(current);
        }
    }
    return merged.toArray(new int[merged.size()][]);
}
```

Note: the loop above starts from `intervals[0]` again for clarity of the
merge condition — functionally equivalent to skipping index 0, since the
first comparison (`current == intervals[0]`) trivially satisfies the
overlap check against itself without changing anything.

---

## 7. Group Anagrams (Medium)

```java
import java.util.*;

public List<List<String>> groupAnagrams(String[] strs) {
    Map<String, List<String>> groups = new HashMap<>();
    for (String s : strs) {
        char[] chars = s.toCharArray();
        Arrays.sort(chars);
        String key = new String(chars);
        groups.computeIfAbsent(key, k -> new ArrayList<>()).add(s);
    }
    return new ArrayList<>(groups.values());
}
```

`computeIfAbsent` replaces Python's `defaultdict` pattern cleanly.

---

## 8. Longest Substring Without Repeating Characters (Medium)

```java
import java.util.HashMap;
import java.util.Map;

public int lengthOfLongestSubstring(String s) {
    Map<Character, Integer> seen = new HashMap<>();
    int left = 0, longest = 0;
    for (int right = 0; right < s.length(); right++) {
        char c = s.charAt(right);
        if (seen.containsKey(c) && seen.get(c) >= left) {
            left = seen.get(c) + 1;
        }
        seen.put(c, right);
        longest = Math.max(longest, right - left + 1);
    }
    return longest;
}
```

Same sliding-window invariant as Python: only shrink the window if the
repeat is inside the *current* window, not anywhere in the string.

---

## 9. Linked List Cycle Detection (Medium)

```java
public boolean hasCycle(ListNode head) {
    ListNode slow = head, fast = head;
    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
        if (slow == fast) {
            return true;
        }
    }
    return false;
}
```

Note: `==` compares object references here, which is exactly what's
needed (checking if two pointers point to the same node) — not `.equals()`.

---

## 10. LRU Cache (Medium — design)

```java
import java.util.LinkedHashMap;
import java.util.Map;

class LRUCache extends LinkedHashMap<Integer, Integer> {
    private final int capacity;

    public LRUCache(int capacity) {
        super(capacity, 0.75f, true);  // true = access-order, not insertion-order
        this.capacity = capacity;
    }

    public int get(int key) {
        return super.getOrDefault(key, -1);
    }

    public void put(int key, int value) {
        super.put(key, value);
    }

    @Override
    protected boolean removeEldestEntry(Map.Entry<Integer, Integer> eldest) {
        return size() > capacity;
    }
}
```

Java's `LinkedHashMap` with `accessOrder=true` gives you LRU behavior
almost for free — `get()` calls automatically move an entry to
most-recently-used, and overriding `removeEldestEntry` handles eviction.
Same caveat as the Python `OrderedDict` version: know the from-scratch
hash-map-plus-doubly-linked-list version too, since some interviewers
disallow built-ins specifically to test the underlying mechanism.

---

## 11. Median of Two Sorted Arrays (Hard)

```java
public double findMedianSortedArrays(int[] nums1, int[] nums2) {
    if (nums1.length > nums2.length) {
        int[] temp = nums1; nums1 = nums2; nums2 = temp;
    }
    int m = nums1.length, n = nums2.length;
    int left = 0, right = m;
    int half = (m + n + 1) / 2;

    while (left <= right) {
        int i = (left + right) / 2;
        int j = half - i;

        int nums1Left = (i > 0) ? nums1[i - 1] : Integer.MIN_VALUE;
        int nums1Right = (i < m) ? nums1[i] : Integer.MAX_VALUE;
        int nums2Left = (j > 0) ? nums2[j - 1] : Integer.MIN_VALUE;
        int nums2Right = (j < n) ? nums2[j] : Integer.MAX_VALUE;

        if (nums1Left <= nums2Right && nums2Left <= nums1Right) {
            if ((m + n) % 2 == 1) {
                return Math.max(nums1Left, nums2Left);
            }
            return (Math.max(nums1Left, nums2Left) + Math.min(nums1Right, nums2Right)) / 2.0;
        } else if (nums1Left > nums2Right) {
            right = i - 1;
        } else {
            left = i + 1;
        }
    }
    throw new IllegalArgumentException("Input arrays are not sorted");
}
```

Same partition-based binary search as Python. Java requires the explicit
`throw` at the end since the compiler can't prove the loop always returns
— worth keeping as a real guard, not just a compiler-satisfying no-op,
since it correctly signals invalid input (unsorted arrays) if that
invariant is ever violated.

---

## 12. Word Ladder (Hard)

```java
import java.util.*;

public int ladderLength(String beginWord, String endWord, List<String> wordList) {
    Set<String> wordSet = new HashSet<>(wordList);
    if (!wordSet.contains(endWord)) return 0;

    Queue<String> queue = new LinkedList<>();
    queue.offer(beginWord);
    int steps = 1;

    while (!queue.isEmpty()) {
        int size = queue.size();
        for (int k = 0; k < size; k++) {
            String word = queue.poll();
            if (word.equals(endWord)) return steps;
            char[] chars = word.toCharArray();
            for (int i = 0; i < chars.length; i++) {
                char original = chars[i];
                for (char c = 'a'; c <= 'z'; c++) {
                    chars[i] = c;
                    String nextWord = new String(chars);
                    if (wordSet.contains(nextWord)) {
                        wordSet.remove(nextWord);
                        queue.offer(nextWord);
                    }
                }
                chars[i] = original;
            }
        }
        steps++;
    }
    return 0;
}
```

Same BFS-on-implicit-graph approach, structured with level-by-level
processing (the `size` snapshot per level) rather than storing `(word,
steps)` pairs — a common Java idiom for BFS shortest-path problems.

---

## 13. Serialize and Deserialize Binary Tree (Hard)

```java
import java.util.*;

class TreeNode {
    int val;
    TreeNode left, right;
    TreeNode(int val) { this.val = val; }
}

public class Codec {
    public String serialize(TreeNode root) {
        StringBuilder sb = new StringBuilder();
        serializeHelper(root, sb);
        return sb.toString();
    }

    private void serializeHelper(TreeNode node, StringBuilder sb) {
        if (node == null) {
            sb.append("#,");
            return;
        }
        sb.append(node.val).append(",");
        serializeHelper(node.left, sb);
        serializeHelper(node.right, sb);
    }

    public TreeNode deserialize(String data) {
        Queue<String> vals = new LinkedList<>(Arrays.asList(data.split(",")));
        return deserializeHelper(vals);
    }

    private TreeNode deserializeHelper(Queue<String> vals) {
        String val = vals.poll();
        if (val.equals("#")) return null;
        TreeNode node = new TreeNode(Integer.parseInt(val));
        node.left = deserializeHelper(vals);
        node.right = deserializeHelper(vals);
        return node;
    }
}
```

Same pre-order DFS encoding as Python; a `Queue` replaces Python's
`iter()` for consuming values one at a time during deserialization.

---

## 14. Trapping Rain Water (Hard)

```java
public int trap(int[] height) {
    if (height.length == 0) return 0;
    int left = 0, right = height.length - 1;
    int leftMax = height[left], rightMax = height[right];
    int water = 0;

    while (left < right) {
        if (leftMax <= rightMax) {
            left++;
            leftMax = Math.max(leftMax, height[left]);
            water += leftMax - height[left];
        } else {
            right--;
            rightMax = Math.max(rightMax, height[right]);
            water += rightMax - height[right];
        }
    }
    return water;
}
```

Identical two-pointer logic to Python — O(n) time, O(1) space.

---

## 15. Merge K Sorted Lists (Hard)

```java
import java.util.PriorityQueue;
import java.util.Comparator;

public ListNode mergeKLists(ListNode[] lists) {
    PriorityQueue<ListNode> heap = new PriorityQueue<>(Comparator.comparingInt(n -> n.val));
    for (ListNode node : lists) {
        if (node != null) heap.offer(node);
    }

    ListNode dummy = new ListNode(0);
    ListNode curr = dummy;
    while (!heap.isEmpty()) {
        ListNode node = heap.poll();
        curr.next = node;
        curr = curr.next;
        if (node.next != null) {
            heap.offer(node.next);
        }
    }
    return dummy.next;
}
```

Java's `PriorityQueue` with a `Comparator` sidesteps the tie-breaking
index Python needed — Java's heap doesn't attempt to compare `ListNode`
objects directly unless you tell it how, so no ambiguous-comparison issue
arises. O(N log k) same as Python.

---

*Python versions: [`python-solutions.md`](./python-solutions.md)*
