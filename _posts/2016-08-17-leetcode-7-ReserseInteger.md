---
layout: post
title: 7-Reverse Integer
category: leetcode
tags: [java, leetcode, airthmetic]
keywords: java,c++,javascript
description: 
---

[7. Reverse Integer](https://leetcode.com/problems/reverse-integer/)

### 原题目

Reverse digits of an integer.

```
Example1: x = 123, return 321
Example2: x = -123, return -321
```

Have you thought about this?
Here are some good questions to ask before coding. Bonus points for you if you have already thought through this!

If the integer's last digit is 0, what should the output be? ie, cases such as 10, 100.

Did you notice that the reversed integer might overflow? Assume the input is a 32-bit integer, then the reverse of 1000000003 overflows. How should you handle such cases?

For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.

### 翻译

反转一个整数数据

```
Example1: x = 123, return 321
Example2: x = -123, return -321
```

注意：在编码之前有一些问题需要考虑，如果你已经考虑了这些问题，这将是你的加分点。
如果该整数的最后一位是0，那么僵该输出什么呢？比如 10， 100
反转后的整数也许会产生溢出，假定输入的是一个32位的整数，如果反转`1000000003`将产生溢出，那这种情况该如何处理呢？
如果发生了溢出，就直接返回为0.

### 解决思路

需要考虑三个方面的问题。
1. 需要考虑负数的反转。
2. 如果整数的末尾是0，比如10， 100， 那么反转后为1， 1
3. 如果反转后产生了溢出，那么就直接返回 0

解决思路为：
定义一个long 类型的变量result，来存储反转后的整数
然后循环反转,注意负数的问题，同时检测到发生了溢出，就返回0

### 代码示例-Java


```
package com.yumo.java.airthmetic.leetcode;

/**
 * Created by yumodev on 8/17/16.
 * 反正整形字符串
 */
public class ReverseInteger_7 {
    public static int reverse(int x) {
        long result = 0;
        while (x != 0){
            result = result * 10 + x % 10;
            x = x / 10;

            if (result > Integer.MAX_VALUE || result < Integer.MIN_VALUE){
                result = 0;
                break;
            }
        }

        return (int)result;
    }

    public static void main(String[] args) {
        int x  = 1000000003;
        long startTime = System.nanoTime();
        int result = reverse(x);
        long endTime = System.nanoTime();
        long time = endTime - startTime;

        System.out.println("reverse:" + result + " time:" + time);
    }
}
```






