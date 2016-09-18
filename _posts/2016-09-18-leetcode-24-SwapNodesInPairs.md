---
layout: post
title: 23-Swap Nodes in Pairs
category: leetcode
tags: [java, leetcode, airthmetic]
keywords: java
description: 
---

[24. Swap Nodes in Pairs](https://leetcode.com/problems/swap-nodes-in-pairs/)

### 原题目

Given a linked list, swap every two adjacent nodes and return its head.

For example,
Given `1->2->3->4,` you should return the list as `2->1->4->3`.

Your algorithm should use only constant space. You may not modify the values in the list, only nodes itself can be changed.

### 翻译

给定一个链表，交互相邻的两个节点，并返回链表的头部。
比如：给定链表`1->2->3->4,` 应该返回`2->1->4->3`
应当使用常量空间时间，不能修改节点的值，但是可以修改节点本身。

### 解题思路

这道题目有两个限定条件：
1、使用常量空间实现；2、不能修改节点的值。
所以声明一个节点为ln(0),其next指向head, temp节点为临时节点。
ln.next表示第一个节点，ln.next.next 标识第二个节点。
现在需要的工作就是讲ln.next, ln.next.next 交互位置。
通过下面方法来实现ln.next 和 ln.next.next 位置的呼唤。

```
      temp = ln.next;
      ln.next = ln.next.next;
      temp.next = ln.next.next;
      ln.next.next = temp;     
``` 
      
  时间复杂度为O(n),
  空间夫再度为O(2);
### 代码示例-Java

```
/**
 * Created by yumodev on 9/13/16.
 */
public class SwapPairs_24 {

    public static class ListNode {
        int val;
        ListNode next;

        ListNode(int x) {
            val = x;
        }
    }

    public static ListNode swapPairs(ListNode head) {
        if (head == null || head.next == null){
            return head;
        }

        int n = 1;

        ListNode ln = new ListNode(0);
        ln.next = head;
        head = head.next;
        ListNode temp;
        while (true){
            if (n % 2 == 0){
                temp = ln.next;
                ln.next = ln.next.next;
                temp.next = ln.next.next;
                ln.next.next = temp;
                ln = ln.next.next;
            }

            if (ln.next == null || ln.next.next == null){
                break;
            }

            n++;
        }

        return head;
    }

    public static ListNode initListNode(int num) {
        int mod = 0;
        int temp = num;
        ListNode ln = null;
        ListNode nextLn = null;
        while (temp > 0) {
            mod = temp % 10;
            temp = temp / 10;
            if (ln == null){
                nextLn = ln = new ListNode(mod);
            }else{
                nextLn.next = new ListNode(mod);
                nextLn = nextLn.next;
            }
        }

        return ln;
    }

    public static String ListNodeToString(final ListNode listNode) {
        StringBuilder sb = new StringBuilder();
        ListNode ln = listNode;
        while (ln != null) {
            sb.append(ln.val + " ");
            ln = ln.next;
        }

        return sb.toString();
    }

    public static void main(String[] args) {
        ListNode l1 = initListNode(4321);
        //ListNode l1 = initListNode(321);
        long startTime = System.nanoTime();
        ListNode l2 = swapPairs(l1);
        long endTime = System.nanoTime();
        long time = endTime - startTime;

        System.out.println("removeNthFromEnd:" + ListNodeToString(l2) + " time:" + time);
    }

}
```


