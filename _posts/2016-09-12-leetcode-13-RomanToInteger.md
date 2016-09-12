---
layout: post
title: 13-Roman to Integer
category: leetcode
tags: [java, leetcode, airthmetic]
keywords: java
description: 
---

[13. Roman to Integer](https://leetcode.com/problems/roman-to-integer/)

### 原题目

Given a roman numeral, convert it to an integer.
Input is guaranteed to be within the range from 1 to 3999.

### 题目翻译

将给定的一个罗马数字字符串转换为整数
假定的输入范围是1到3999.

### 解决思路

这道里面本身很简单，其实难点在于必须要明白罗马数字的标识方法。
罗马数字一共有七个大写字符，分别是：`I、V、X、L、C、D、M`。
下面是罗马字符和整数的对应关系。

罗马字符 | 整数
------ | ------
I  | 1|
V  |  5
X  | 10
L | 50
C | 100
D | 500
M | 1000

罗马字符串的计算规则就是
1、从左向右一次计算。
2、如果一个罗马字符对应的整数比它后面的字符对应的整数小，那么就讲后面的字符对应的整数减去它对应的整数。
如果一个罗马字符对应的整数不小于它后面的字符对应的整数，那么就讲后面的字符对应的整数加上它对应的整数。
下面是一个罗马字符串和整数的对应计算实例

罗马字符串|整数
------|------
III | 3
IV | 4
VI | 6
IX | 9
XI | 11
IL | 49
LX| 60
IM | 999
VM | 995
XM | 990
LM | 950
CM | 900
DM | 500 
MI | 1001
MV | 1005
MX | 1010
ML | 1050
MC | 1100
MD | 1500
MDCCCLXXXIV | 1884


### 代码示例


```
/**
 * Created by yumodev on 9/12/16.
 */
public class RomanToInteger_13 {
    public static int romanToInt(String s) {
        if (s == null || s.length() == 0){
            return 0;
        }

        int result = 0;
        for (int i = 0; i < s.length();i++){
            char ch = s.charAt(i);
            switch (ch){
                case 'I':{
                    if (i < s.length() -1  && s.charAt(i + 1) != 'I'){
                        result -= 1;
                    }else{
                        result += 1;
                    }
                    break;
                }
                case 'V':{
                    if (i < s.length() -1  && (s.charAt(i + 1) != 'I' && s.charAt(i + 1) != 'V')){
                        result -= 5;
                    }else{
                        result += 5;
                    }
                    break;
                }
                case 'X':{
                    if (i < s.length() -1  && ( s.charAt(i + 1) == 'C' || s.charAt(i + 1) == 'L' || s.charAt(i + 1) == 'M' || s.charAt(i + 1) == 'D')){
                        result -= 10;
                    }else{
                        result += 10;
                    }
                    break;
                }
                case 'L':{
                    if (i < s.length() -1  && ( s.charAt(i + 1) == 'C' || s.charAt(i + 1) == 'M' || s.charAt(i + 1) == 'D')){
                        result -= 50;
                    }else{
                        result += 50;
                    }
                    break;
                }
                case 'C':{
                    if (i < s.length() -1  && (s.charAt(i + 1) == 'M' || s.charAt(i + 1) == 'D')){
                        result -= 100;
                    }else{
                        result += 100;
                    }
                    break;
                }
                case 'D':{
                    if (i < s.length() -1  && s.charAt(i + 1) == 'M'){
                        result -= 500;
                    }else{
                        result += 500;
                    }
                    break;
                }
                case 'M':{
                    result += 1000;
                    break;
                }

            }

        }

        return result;
    }

    public static void main(String[] args) {
        String str = "MDCCCLXXXIV";
        long startTime = System.nanoTime();
        int result = romanToInt(str);
        long endTime = System.nanoTime();
        long time = endTime - startTime;

        System.out.println("romanToInt:" + result + " time:" + time);
    }
}
```

