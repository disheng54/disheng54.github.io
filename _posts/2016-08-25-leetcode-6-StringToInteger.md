---
layout: post
title: 8-String to Integer
category: leetcode
tags: [java, leetcode, airthmetic]
keywords: java,c++,javascript
description: 
---

[8. String to Integer (atoi)](https://leetcode.com/problems/string-to-integer-atoi/)

### 原题目

Implement atoi to convert a string to an integer.

Hint: Carefully consider all possible input cases. If you want a challenge, please do not see below and ask yourself what are the possible input cases.

Notes: It is intended for this problem to be specified vaguely (ie, no given input specs). You are responsible to gather all the input requirements up front.

Requirements for atoi:
The function first discards as many whitespace characters as necessary until the first non-whitespace character is found. Then, starting from this character, takes an optional initial plus or minus sign followed by as many numerical digits as possible, and interprets them as a numerical value.

The string can contain additional characters after those that form the integral number, which are ignored and have no effect on the behavior of this function.

If the first sequence of non-whitespace characters in str is not a valid integral number, or if no such sequence exists because either str is empty or it contains only whitespace characters, no conversion is performed.

If no valid conversion could be performed, a zero value is returned. If the correct value is out of the range of representable values, INT_MAX (2147483647) or INT_MIN (-2147483648) is returned.

### 翻译

实现方法 `atoi` 将一个字符串转换为整数
提示：请考虑到所有输入的情况。如果你想要挑战一下自己，就可以不用开下面的注意事项然后问题自己，都有哪些输入情况。
注意：这道题目的定义是模糊的(没有给输入的限定条件)，你需要自己考虑所有的输入情况。

`atoi ` 方法的要求：
该方法要求忽略字符串开始的空白字符，一直到第一个非空白字符为止。然后从这个字符开始，先判断初始的正负字符，然后选取尽可能多的数字字符，并将它们转换为一个数值。
也许该字符串的有效数字后面还有一些额外的非数字字符，那么将忽略这些字符。
如果第一个非空白字符不是数字字符，或者改字符串是个空串，或者只包含空白字符，则不执行转换。
如果未执行有效的转换，就返回 `0` .如果转换后的数字超出了 `int` 类型标识数字的的范围，那么返回`INT_MAX (2147483647) 或者 INT_MIN (-2147483648)` 


### 解决思路

这道题目比较简单，正如题目的里面的讲的那样，难点是要考虑到各种的情况。
1、空字符串、空白字符串、没有有效数字的字符串，返回0
2、需要去除前面的无效空白字符。
3、考虑第一个非空字符，如果是 `+` 标识正值，如果是` -` 标识负值。
4、忽略有效数字字符后面的所有无效字符，比如：`'   -123&456' `转换为 `-123`
5、如果转换后的整数值，超过了返回就返回返回`INT_MAX (2147483647) 或者 INT_MIN (-2147483648)` 

### 代码示例-Java


```
package com.yumo.java.airthmetic.leetcode;

/**
 * Created by yumodev on 8/22/16.
 */
public class Atoi_8 {
    public static int myAtoi(String str) {
        if (str == null ||str.trim().length() == 0){
            return  0;
        }

        int index = 0;
        while ((index < str.length()) && (str.charAt(index) == ' ')){
            index ++;

        }

        int sign = 1;
        if (str.charAt(index) == '+'){
            sign = 1;
            index ++;
        }else if (str.charAt(index) == '-'){
            sign = -1;
            index ++;
        }

        long result = 0L;
        for (int i = index; i < str.length(); i++){
           if( str.charAt(i) >=  '0' && str.charAt(i) <= '9'){
                result = result * 10 + (str.charAt(i) - '0');
               if (sign == 1){
                   if(result > Integer.MAX_VALUE){
                       result = Integer.MAX_VALUE;
                       break;
                   }
               }else{
                   if (result*sign < Integer.MIN_VALUE){
                       result = Integer.MIN_VALUE;
                       break;
                   }
               }
           }else{
               break;
           }
        }

        return (int)result * sign;
    }

    public static void main(String[] args) {
        //String str = "  -214748364734dd";
        String str = "  -00134";
        long startTime = System.nanoTime();
        int result = myAtoi(str);
        long endTime = System.nanoTime();
        long time = endTime - startTime;

        System.out.println("reverse:" + result + " time:" + time);
    }
}

```



