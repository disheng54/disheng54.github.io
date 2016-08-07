---
layout: post
title: 3-Longest Substring Without Repeating Characters
category: leetcode
tags: [java, leetcode, airthmetic]
keywords: java,c++,javascript
description: 
---

[Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

### 原题目

Given a string, find the length of the longest substring without repeating characters.

Examples:

Given `"abcabcbb"`, the answer is `"abc"`, which the length is 3.

Given `"bbbbb",` the answer is `"b"`, with the length of 1.

Given `"pwwkew"`, the answer is `"wke"`, with the length of 3. Note that the answer must be a substring, `"pwke"` is a subsequence and not a substring.

### 题目翻译

获取一个字符串的各个字符都不相同的子串的最大长度。
举例：

字符串 `"abcabcbb"`, 符合结果的字串为 `"abc"`, 其长度为 `3`.
字符串 `"bbbbb"`, 符合结果的字串为 `"b"`, 其长度为 `1`.
字符串 `"pwwkew"`, 符合结果的字串为 `"wke"`, 其长度为 `3`. 
注意结果必须为连续的子串， 其中`"pwke"`是不同的字符组合，但不是连续的子串

### 解决思路

首先要明白这道题目是要获取字符串中不同字符字符组成的子串的最大长度，而不是不同字符的个数。
声明一个变量start,记录不同字符串的初始索引，一个变量mxlen 记录最大程度，然后遍历字串中字符，记录该字符的索引index，并且查询该字符上次出现的索引位置，如果该字符存在上次索引LastIndex，并且该索引值不小于 start，那么将index 减去 start当做该不同字符子串的长度与maxlen，比较取其大着。通过将LastIndex赋值与start。

### 代码示例-java

```
package com.yumo.java.airthmetic.leetcode;

import java.util.HashMap;
import java.util.Map;

/**
 * Created by yumo on 8/6/16.
 * 获取字符串中不重复的字字符串的最大长度.
 */
public class LongSubNoRepeatCHar_3 {

    public static int lengthOfLongestSubstringByMap(String s) {
        if (s == null || s.isEmpty()){
            return 0;
        }

        Map<Character, Integer> map = new HashMap<>();
        int maxLen = 1;
        int start = 0;

        for (int i = 0; i < s.length(); i++){
            if (map.get(s.charAt(i)) != null){
                int j = map.get(s.charAt(i));
                if (j >= start){
                    maxLen = (i - start > maxLen) ? i - start : maxLen;
                    start = j + 1;
                    map.remove(s.charAt(i));
                }
            }

            map.put(s.charAt(i), i);
        }

        return (s.length() - start > maxLen) ? s.length() - start : maxLen;
    }

    public static int lengthOfLongestSubstringByArray(String s) {
        if (s == null || s.isEmpty()){
            return 0;
        }

        int[] chars = new int[256];
        int maxLen = 1;
        int start = 0;

        for (int i = 0; i < s.length(); i++){
            int ch = s.charAt(i);
            if (chars[ch] != 0){
                if (chars[ch] > start){
                    maxLen = (i - start > maxLen) ? i - start : maxLen;
                    start = chars[ch];
                }
            }

            chars[ch] = i + 1;
        }

        return (s.length() - start > maxLen) ? s.length() - start : maxLen;
    }

    public static void main(String[] args){
        //String str = "abcabcbb";
        //String str = "aaa";
        //String str = "pwwkew";
        // String str = "au";
        String str = "aab";
        long startTime = System.nanoTime();
        int length = lengthOfLongestSubstringByMap(str);
        long endTime = System.nanoTime();
        long time = endTime - startTime;
        System.out.println(str+" len:"+length +" time:"+ time);

        startTime = System.nanoTime();
        length = lengthOfLongestSubstringByArray(str);
        endTime = System.nanoTime();
        time = endTime - startTime;
        System.out.println(str+" len:"+length +" time:"+ time);
    }
}

```

### 代码示例-c++

```
//
// Created by yumodev on 8/6/16.
//
#include <iostream>
using namespace std;
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        if (s.size() == 0) {
            return 0;
        }

        int chars[128];
        memset(chars, 0xff, 128 * sizeof(int));
        int maxLen = 1;
        int start = 0;
        for (int i = 0; i < s.size(); ++i) {
            if (chars[s[i]] != 0 && chars[s[i]] > start) {
//                if(i - start > maxLen){
//                    maxLen = i - start;
//                }

                maxLen = i - start > maxLen ? i - start : maxLen;
                start = chars[s[i]];
            }

            chars[s[i]] = i + 1;
        }

        if (s.length() - start > maxLen) {
            maxLen = s.length() - start;
        }

        return maxLen;
    }
};

int main() {
   // string str = "auu";
    string str = "dvdf";
    //string str = "aaa";
    //string str = "pwwkew";
    // string str = "au";
    //string str = "aab";
    clock_t start, finish;
    Solution su;
    start = clock();
    int len = su.lengthOfLongestSubstring(str);
    finish = clock();
    cout << "time:"<<((double)(finish - start)/CLOCKS_PER_SEC)* 1000000 <<"  len " <<len<<endl;


    return 0;
}
```

### 代码示例-javascript

```
/**
 * @param {string} s
 * @return {number}
 */
var lengthOfLongestSubstring = function(s) {
  if (s === undefined || s.length === 0) {
   return 0;
 }
 var chars = {};
 var maxLen = 1;
 var start = 0;
 for(i = 0; i < s.length; i++){
   if (chars[s[i]] !== undefined) {
      if (chars[s[i]] >= start) {
        if(i - start > maxLen){
          maxLen = i - start;
        }
        start = chars[s[i]];
      }
   }

   chars[s[i]] = i + 1;
 }

 if(s.length - start > maxLen){
   maxLen = s.length - start;
 }

 return maxLen;
};
//var str = "auu";
var str = "dvdf"
var len = lengthOfLongestSubstring(str);
console.log(num+" "+len);
```







