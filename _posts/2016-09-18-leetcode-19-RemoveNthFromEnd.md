---
layout: post
title: 19-Remove Nth Node From End of List
category: leetcode
tags: [java, leetcode, airthmetic]
keywords: java
description: 
---

[19. Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)

### 原题目

Given a linked list, remove the nth node from the end of list and return its head.
For example,

   `Given linked list: 1->2->3->4->5, and n = 2.
   After removing the second node from the end, the linked list becomes 1->2->3->5.`
Note:
Given n will always be valid.
Try to do this in one pass.

### 翻译

给定一个链表，删除倒数第n个节点，然后返回这链表的头部。
比如：
 `给定链表： 1->2->3->4->5,  n = 2.
  从尾部移除第2个节点, 然后链表变为： 1->2->3->5.`
  
  注意：给定的n总是有效的，尝试一次通过。

### 解题思路

建立一前一后两个节点:firstLn, secondLn.
初始化firstLn的next 指向链表头部，secondLn指向链表头部
先将firstLn移动n个位置，然后开始移动SecondLn节点。
当FirstLn移动到链表结尾后，此时需要将SecondLn的下一个节点移除即可。
时间复杂度为：O(n);
空间复杂度为：O(1);



### 代码示例-Java

```
public ListNode removeNthFromEnd(ListNode head, int n) {
        if (n == 0 || head == null){
            return head;
        }

        ListNode firstLn = head;
        ListNode secondLn = new ListNode(0);
        int pos = 1;

        while (firstNextLn != null){
            if (pos == n){
                secondNextLn.next = head;
            }else if (pos > n){
                secondNextLn = secondNextLn.next;
            }

            firstNextLn = firstNextLn.next;
            pos++;
        }

        if (secondNextLn != null){
            if (secondNextLn.next.equals(head)){
                return head.next;
            }else{
                secondNextLn.next = secondNextLn.next.next;
            }

        }


        return head;
    }
```




