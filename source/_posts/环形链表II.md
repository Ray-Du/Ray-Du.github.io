---
title: Linked List Cycle II
date: 2023-04-10 12:06:36
tags:
---

## 环形链表II
给定一个链表的头节点  head ，返回链表开始入环的第一个节点。 如果链表无环，则返回 null。
如果链表中有某个节点，可以通过连续跟踪 next 指针再次到达，则链表中存在环。 为了表示给定链表中的环，评测系统内部使用整数 pos 来表示链表尾连接到链表中的位置（索引从 0 开始）。如果 pos 是 -1，则在该链表中没有环。注意：pos 不作为参数进行传递，仅仅是为了标识链表的实际情况。
不允许修改 链表。
```java
public class Solution {
    public ListNode detectCycle(ListNode head) {
        ListNode fast = head, slow = head;
        while(fast != null && fast.next != null){
            fast = fast.next.next;
            slow = slow.next;
            if(fast == slow){
                fast = head;
                while(fast != slow){
                    fast = fast.next;
                    slow = slow.next;
                }
                return fast;
            }
        }
        return null;
    }
}
```
本题使用双指针，让快指针一次走两步，慢指针一次走一步，当两者相遇，证明链表有环；设链表长度为a，环长度为b，，快指针走了f，慢指针走了s，f = 2s，f比s多走了n圈，f = s + nb，以上两式相减得：f = 2nb，s = nb；slow指针位置不变 ，将fast指针重新指向链表头部节点，slow和fast同时每轮向前走1步，当 fast 指针走到f = a步时，slow指针走到步s = a + nb，此时 两指针重合，并同时指向链表环入口，返回fast