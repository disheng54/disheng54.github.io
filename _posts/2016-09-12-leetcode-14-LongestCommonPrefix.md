---
layout: post
title: 14-Longest Common Prefix
category: leetcode
tags: [java, leetcode, airthmetic]
keywords: java
description: 
---

[14. Longest Common Prefix](https://leetcode.com/problems/longest-common-prefix/)

### 原题目

Write a function to find the longest common prefix string amongst an array of strings.

### 翻译

编写一个方法来查找一个字符串数组中最长的公共前缀字符串。

### 解决思路

这道题目的意思是求取所有字符串的最长前缀公共字符串。采用暴力比较的方法是最简单。
就是循环获取第一个字符串的前缀子串，将这个子串分别和其他字符串的相同索引的子串进行比较，
如果任意一个其他字符串的前缀子串和第一字符串的前缀子串不相符，那么除去这个前缀子串的最后一个字符，就是最大的公共前缀子串

### 代码示例-Java


```
/**
 * Created by yumodev on 9/12/16.
 */
public class LongestCommonPrefix_14 {
    public static String longestCommonPrefix(String[] strs) {
        if (strs == null || strs.length == 0){
            return "";
        }


        for (int i = 0; i < strs[0].length(); i++){
            for (int j = 1; j < strs.length; j++){
                if (strs[j].length() <= i || strs[j].charAt(i) != strs[0].charAt(i)){
                    return strs[0].substring(0, i);
                }
            }
        }

        return strs[0];
    }

    public static void main(String[] args) {
        String[] str = {"121", "12", "21"};
        long startTime = System.nanoTime();
        String result = longestCommonPrefix(str);
        long endTime = System.nanoTime();
        long time = endTime - startTime;

        System.out.println("longestCommonPrefix:" + result + " time:" + time);
    }
}
```



