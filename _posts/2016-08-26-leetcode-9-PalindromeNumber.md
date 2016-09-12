---
layout: post
title: 9-Palindrome Number
category: leetcode
tags: [java, leetcode, airthmetic]
keywords: java
description: 
---

[9. Palindrome Number](https://leetcode.com/problems/palindrome-number/)

### 原题目

Determine whether an integer is a palindrome. Do this without extra space.

Some hints:
Could negative integers be palindromes? (ie, -1)

If you are thinking of converting the integer to string, note the restriction of using extra space.

You could also try reversing an integer. However, if you have solved the problem "Reverse Integer", you know that the reversed integer might overflow. How would you handle such case?

There is a more generic way of solving this problem.

### 翻译

在不需要额外空间的情况下，判定一个整数是否是回文字符串。
一些提示：
一个负整数是回文字符串吗?(比如 `-1`)
如果你想把一个整数转换为字符串，需要注意不需要额外的空间的限制。
也许你会反转整数，如果你已经解决了这道题目"Reverse Integer", 你就会知道反转字符串也许会发生溢出，然后你该如何处理这种情况呢。
有一个更加通用的方式来解决这个问题。


### 解题思路

这道题目需要考虑一些特殊的情况，比如负数不认为是一个负数
判断一个整数 x 是不是回文字符串，那么就把这个整数反转后，判断和 x 是不是相等就可以了。
题目中整数溢出问题，是不需要考虑的，凡是反转后发生溢出的，那么肯定不是回文串。
 
### 代码示例-Java


```
package com.yumo.java.airthmetic.leetcode;

/**
 * Created by yumodev on 8/25/16.
 */
public class PalindromeNumber_9 {
    public static  boolean isPalindrome(int x) {
        if (x < 0){
            return false;
        }

        int los = 0;
        int temp = x;

        while (temp > 0){
            los = los * 10 + temp % 10;
            temp = temp / 10;
        }

        return los == x;
    }

    public static void main(String[] args) {
        int number = 121;
        long startTime = System.nanoTime();
        boolean result = isPalindrome(number);
        long endTime = System.nanoTime();
        long time = endTime - startTime;

        System.out.println("reverse:" + result + " time:" + time);
    }
}
```






