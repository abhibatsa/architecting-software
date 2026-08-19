# Coding Interview Questions — 15 Problems

Classic, high-frequency problems, each with a working solution in Python
and Java, explained — not just pasted. Language coverage will expand to
JavaScript, TypeScript, and Go in a later pass (see note at the bottom).

## How to use this

Solve it yourself first, timed (15-20 min for Easy, 25-35 for Medium/Hard),
*then* check the explanation — the explanation is written to teach the
pattern, not just justify the answer, so it's most useful after a real
attempt.

## Index

| # | Problem | Difficulty | Pattern | Dev focus | SDET focus |
|---|---|---|---|---|---|
| 1 | Two Sum | Easy | Hash map | Time/space trade-off | Edge cases: duplicates, no solution |
| 2 | Valid Parentheses | Easy | Stack | Stack mechanics | Input validation, malformed strings |
| 3 | Reverse a Linked List | Easy | Pointers | In-place manipulation | Null/single-node edge cases |
| 4 | Binary Search | Easy | Divide & conquer | Off-by-one correctness | Boundary/empty-array testing |
| 5 | First Unique Character in a String | Easy | Hash map / counting | Frequency counting | Unicode/empty-string edge cases |
| 6 | Merge Intervals | Medium | Sort + sweep | Sorting-based merge logic | Overlapping/adjacent edge cases |
| 7 | Group Anagrams | Medium | Hash map | Canonical-key design | Case sensitivity, empty strings |
| 8 | Longest Substring Without Repeating Characters | Medium | Sliding window | Window invariant maintenance | Off-by-one window bugs |
| 9 | Linked List Cycle Detection | Medium | Fast/slow pointers | Floyd's algorithm | Detecting vs. proving no cycle |
| 10 | LRU Cache (design) | Medium | Hash map + doubly linked list | System design in miniature | State-mutation test coverage |
| 11 | Median of Two Sorted Arrays | Hard | Binary search on partitions | O(log(min(m,n))) technique | Even/odd length edge cases |
| 12 | Word Ladder | Hard | BFS on implicit graph | Shortest-path via BFS | No-path-exists case |
| 13 | Serialize & Deserialize Binary Tree | Hard | Tree traversal + encoding | Round-trip correctness | Format-parsing robustness |
| 14 | Trapping Rain Water | Hard | Two pointers | Prefix-max technique | Flat/monotonic array edge cases |
| 15 | Merge K Sorted Lists | Hard | Heap / divide & conquer | Complexity trade-offs (heap vs. D&C) | Empty-list-in-input handling |

## Language coverage

- **Now:** Python, Java (both fully solved, see below)
- **Next:** JavaScript, TypeScript, Go — same 15 problems, same
  explanations, ported. Flagging honestly: porting 15 problems × 3 more
  languages accurately (not just syntax-translated, actually idiomatic per
  language) is real effort — plan this as its own batch rather than
  something added in passing.

## Solutions

- [`python-solutions.md`](./python-solutions.md)
- [`java-solutions.md`](./java-solutions.md)

## A note on Dev vs SDET framing(who is this for)

Rather than maintaining two separate question banks, every problem here is
tagged with both a **Dev focus** and an **SDET focus** column above. The
core algorithm is identical either way — what differs is the follow-up:
a Dev interview pushes on complexity/optimization, an SDET interview
pushes on "what inputs would you test this against, and how would you
prove this is correct." Prep the same solution, prep both follow-up
angles.
