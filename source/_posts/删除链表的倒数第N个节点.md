---
title: Remove Count Backwards N th Node
date: 2023-04-10 11:06:19
tags:
---

## 删除链表的倒数第N个节点
给定一个链表，删除链表的倒数第 n 个结点，并且返回链表的头结点。
```java
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        int cnt = 0;
        ListNode dummy = new ListNode();
        dummy.next = head;
        ListNode fast = dummy;
        ListNode slow = dummy;
        for(int i = 0; i < n; i++){
            fast = fast.next;
        }
        while(fast != null && fast.next != null){
            fast = fast.next;
            slow = slow.next;
        }
        slow.next = slow.next.next;
        return dummy.next;
    }
}
```
本题要点是让快指针从`dummy`先走n步，再让快慢指针同时走，直到快指针走到结尾，让慢指针`slow.next = slow.next.next`