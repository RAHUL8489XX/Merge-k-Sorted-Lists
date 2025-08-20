# 🧩 Merge k Sorted Lists — Divide and Conquer

🔗 [LeetCode Problem Link](https://leetcode.com/problems/merge-k-sorted-lists/submissions/1741524263/)  
📁 Difficulty: Hard  
🧠 Tags: Linked List, Divide and Conquer, Recursion

---

## 🚀 Problem Statement

You are given an array of `k` linked lists, each sorted in ascending order.  
Merge all the linked lists into one sorted linked list and return its head.

---

## 📊 Complexity Analysis

- **Time Complexity**: `O(N log k)`  
  - Each merge operation combines two lists in linear time.
  - The recursive divide-and-conquer strategy performs `log k` levels of merging.
  - Total nodes across all lists = `N`.

- **Space Complexity**: `O(log k)`  
  - Due to recursion stack depth from `mergeRange`.
  - No extra data structures used beyond recursion and result list.


## ✅ Approach: Divide and Conquer

Instead of merging all lists at once, we recursively merge pairs of lists.  
This reduces the problem size logarithmically and improves performance.

---

## 🧪 Example Test Cases
Input: lists = [[1,4,5],[1,3,4],[2,6]]
Output: [1,1,2,3,4,4,5,6]

Input: lists = []
Output: []

Input: lists = [[]]
Output: []

## 🔧 Python Code

```python
class Solution(object):
    def mergeKLists(self, lists):
        if not lists:
            return None
        return self.mergeRange(lists, 0, len(lists) - 1)

    def mergeRange(self, lists, left, right):
        if left == right:
            return lists[left]
        mid = (left + right) // 2
        l1 = self.mergeRange(lists, left, mid)
        l2 = self.mergeRange(lists, mid + 1, right)
        return self.mergeTwoLists(l1, l2)

    def mergeTwoLists(self, l1, l2):
        dummy = ListNode(0)
        current = dummy
        while l1 and l2:
            if l1.val < l2.val:
                current.next = l1
                l1 = l1.next
            else:
                current.next = l2
                l2 = l2.next
            current = current.next
        current.next = l1 or l2
        return dummy.next
