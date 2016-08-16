---
layout: post
title: 5-Longest Palindromic Substring
category: leetcode
tags: [java, leetcode, airthmetic]
keywords: java,c++,javascript
description: 
---
[Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/)

### 原题目

Given a string S, find the longest palindromic substring in S. You may assume that the maximum length of S is 1000, and there exists one unique longest palindromic substring

### 题目翻译

给定一个字符串 S，找出其中最长的回文子串。假定 S的最长长度为1000，且存在唯一的最长回文子串

### 解决思路

这个题目可以利用动态规划的方法进行处理。
假定字符串的长度为len, 声明一个二维数组：dp = new boolean[len][len]
dp[i][j] 标识字符串S 中S[i~j]的子串是不是回文字符串。
判断S[i~j]如果是回文串，必须满足两个条件：
1. S[i] = S[j] 
2. dp[i+1][j-1] = true。



### 代码示例-Java


```
/**
 * Created by wks on 8/8/16.
 */
public class LongestPalindrome_5 {
    /**
     * 利用动态规划的方法.
     * @param s
     * @return
     */
    public static String longestPalindrome(String s){
        if (s == null || s.length() == 1) {
            return s;
        }

        int len = s.length();
        boolean[][] dp = new boolean[len][len];
        int begin = 0, end = 0, max = 1;

        for (int i = len - 1; i >= 0; i--){
            for (int j = i; j < len; j++){
                if (s.charAt(i) == s.charAt(j)){
                    if (j - i <= 2 ||  (dp[i+1][j-1] && j-1 > 0)){
                        dp[i][j] = true;
                        if (max < j - i + 1){
                            max = j - i + 1;
                            begin = i;
                            end = j;
                        }
                    }
                }
            }
        }


        return s.substring(begin, end+1);
    }

    public static void main(String[] args) {
        String str = "1aba12";
        long startTime = System.nanoTime();
        String palindrome = longestPalindrome(str);
        long endTime = System.nanoTime();
        long time = endTime - startTime;

        System.out.println("palindrome:" + palindrome + " time:" + time);
    }
}
```






