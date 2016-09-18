---
layout: post
title: 21-Merge Two Sorted Lists
category: leetcode
tags: [java, leetcode, airthmetic]
keywords: java
description: 
---

[21. Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/)

### 原题目

Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

### 翻译

将两个有序链表合并成一个新的链表。新的链表应该有由这两个链表的头部拼接而成。

### 解题思路

按照题意新链表有这两个有序链表的头部拼接而成，所以需要先找到比较两个链表的头部，
将较小的那个当做新链表的头部，然后同时遍历两个链表进行拼接就行了。
时间复杂度为:O(m+n)
空间复杂度为:O(0)

### 代码示例-Java

```
public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if (l1 == null ){
            return l2;
        }

        if (l2 == null){
            return l1;
        }

        ListNode ln;
        ListNode head;
        if (l1.val < l2.val){
            head = ln = l1;
            l1 = l1.next;
        }else{
            head = ln = l2;
            l2 = l2.next;
        }

        while (l1 != null || l2 != null){
            if (l1 == null){
                ln.next = l2;
                break;
            }else if (l2 == null){
                ln.next = l1;
                break;
            }

            if (l1.val < l2.val){
                ln.next = l1;
                ln = ln.next;
                l1 = l1.next;
            }else{
                ln.next = l2;
                ln = ln.next;
                l2 = l2.next;
            }
        }

        return head;
    }
```


