---
layout: post
title: 2-Add Two Numbers
category: leetcode
tags: [java, leetcode, airthmetic]
keywords: java,c++,javascript
description: 
---

[题目原地址](https://leetcode.com/problems/add-two-numbers/)

### 原题目

You are given two linked lists representing two non-negative numbers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8

### 翻译

给出两个标识非负整数的链表，整数在链表中反向存储且链表中的每个节点只存储一个数字。
将两个整数链表相加，将结果用链表返回
输入: (2 -> 4 -> 3) + (5 -> 6 -> 4)
输出: 7 -> 0 -> 8

### 解决思路

这是一个简单的问题，只是稍微注意下两个链表长度不一致就可以了。

### 代码示例-Java 
     
```     
/**
 * Created by wks on 8/5/16.
 * You are given two linked lists representing two non-negative numbers.
 * The digits are stored in reverse order and each of their nodes contain a single digit.
 * Add the two numbers and return it as a linked list.
 * <p>
 * Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
 * Output: 7 -> 0 -> 8
 */
public class AddTwoNumbers_2 {

    public static class ListNode {
        int val;
        ListNode next;

        ListNode(int x) {
            val = x;
        }
    }

    public static ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        int lso = 0;
        int sum = 0;
        ListNode ls = null;
        ListNode nextLn = null;
        while (l1 != null || l2 != null || lso != 0) {
            sum = lso;
            if (l1 != null) sum += l1.val;
            if (l2 != null) sum += l2.val;

            lso = sum / 10;
            ListNode temp = new ListNode(sum % 10);
            if (ls == null) nextLn = ls = temp;
            else{
                nextLn.next = temp;
                nextLn = nextLn.next;
            }

            if (l1 != null) l1 = l1.next;
            if (l2 != null) l2 = l2.next;
        }
        return ls;
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
        ListNode l1 = initListNode(1027633061);
        ListNode l2 = initListNode(1696698036);
//
//        ListNode l1 = initListNode(342);
//        ListNode l2 = initListNode(465);

//        ListNode l1 = initListNode(5);
//        ListNode l2 = initListNode(5);
        System.out.println("listNode1 " + ListNodeToString(l1));

        System.out.println("listNode2 " + ListNodeToString(l2));

        ListNode ls = addTwoNumbers(l1, l2);
        System.out.println("listNodes " + ListNodeToString(ls));
    }
}
```

### 代码示例-c++


```
//
// Created by yumo on 8/5/16.
//
#include <iostream>
using namespace std;

struct ListNode
{
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(NULL) { }
};

class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        int lso = 0;
        ListNode* ln = NULL;
        ListNode* nextLn = NULL;
        while (true){
            int sum = lso;
            if(l1 != NULL){
                sum += l1->val;
                l1 = l1->next;
            }
            if(l2 != NULL){
                sum += l2->val;
                l2 = l2->next;
            }
            lso = sum /10;
            ListNode* node = new ListNode(sum %10);
            if(ln == NULL){
                nextLn = ln = node;
            }else{
                nextLn->next = node;
                nextLn = node;
            }

            if(l1 == NULL && l2 == NULL && lso == 0){
                break;
            }
        }

        return ln;
    }

    ListNode* initListNode(int num){
        int mod = 0;
        int temp = num;
        ListNode* ln = NULL;
        ListNode* nextLn = NULL;
        while(num  > 0){
            mod = num % 10;
            num = num / 10;
            ListNode* node = new ListNode(mod);
            if(ln == NULL){
                nextLn = ln = node;
            }else{
                nextLn->next = node;
                nextLn = node;
            }
        }
        return ln;
    }

    string listNodeToString(ListNode *ln){
        ListNode* next = ln;
        string sb;
        while(next != NULL){
            int val = next->val;
            next = next->next;
            sb += to_string(val)+" ";
        }
        return sb;
    }
};

int main()
{
//     int num1 = 342;
//     int num2 = 465;

//    int num1 = 5;
//    int num2 = 5;

      int num1 = 1027633061;
      int num2 = 1696698036;
     Solution solution;

     ListNode* l1 = solution.initListNode(num1);
     ListNode* l2 = solution.initListNode(num2);

     cout<<"l1 "<<solution.listNodeToString(l1)<<endl;
     cout<<"l2 "<<solution.listNodeToString(l2)<<endl;


    clock_t start, finish;

    start = clock();
    ListNode* ln = solution.addTwoNumbers(l1, l2);
    finish = clock();
    cout << "time:" << ((double) (finish - start) / CLOCKS_PER_SEC) * 1000000 <<"result: "<<solution.listNodeToString(ln) << endl;


    return 0;
}
```

### 代码示例-JavaScript


```
function ListNode(val) {
     this.val = val;
     this.next = null;
}

function initListNode(num){
   var mod = 0;
   var ln = null;
   var nextLn = null;
   while(num > 0){
      mod = num % 10;
      num = parseInt(num / 10);
      if(ln == null){
        ln = new ListNode(mod);
        nextLn = ln;
      }else{
        nextLn.next = new ListNode(mod);
        nextLn = nextLn.next;
      }
   }

   return ln;
}

function listNodeToString(ln){
  var str ="";
  var next = ln;
  while(next != null){
    str += next.val+" ";
    next = next.next;
  }
  return str;
}

var addTwoNumbers = function(l1, l2) {
    var los = 0;
    var ln = null;
    var nextLn = null;
    while(true){
      var sum = los;
      if(l1 != null){
        sum += l1.val;
        l1 = l1.next;
      }

      if(l2 != null){
        sum += l2.val;
        l2 = l2.next;
      }
      if(ln == null){
        nextLn = ln = new ListNode(sum % 10);
      }else{
        nextLn.next = new ListNode(sum % 10);
        nextLn = nextLn.next;
      }

      los = parseInt(sum / 10);
      if(l1 == null && l2 == null && los == 0){
         break;
      }
    }

    return ln;
};

// var num1 = 342;
// var num2 = 465;

var num1 = 5;
var num2 = 5;

// var num1 = 342;
// var num2 = 465;

var l1 = initListNode(num1);
var l2 = initListNode(num2);
console.log("l1:"+listNodeToString(l1));
console.log("l2:"+listNodeToString(l2));
var ln = addTwoNumbers(l1, l2);
console.log("result:"+listNodeToString(ln));

```



