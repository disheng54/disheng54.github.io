---
layout: post
title: 6-ZigZag Conversion
category: leetcode
tags: [java, leetcode, airthmetic]
keywords: java,c++,javascript
description: 
---

[6. ZigZag Conversion](https://leetcode.com/problems/zigzag-conversion/)

### 原题目

The string `"PAYPALISHIRING"` is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

	P 		A		H		N
	A 	P 	L	S	I	I	G
	Y		I		R	
	
And then read line by line: `"PAHNAPLSIIGYIR"`
Write the code that will take a string and make this conversion given a number of rows:

`string convert(string text, int nRows);`
`convert("PAYPALISHIRING", 3)` should return `"PAHNAPLSIIGYIR".`

### 翻译

将字符串`"PAYPALISHIRING"`按照给定的行数，转为成锯齿形的字符串。然后将该锯齿形字符串一次读成`"PAHNAPLSIIGYIR"`

	P 		A		H		N
	A 	P 	L	S	I	I	G
	Y		I		R	

编写代码将给定的字符串和行数，将字符串进行锯齿转换。
	
	string convert(string text, int nRows);

`convert("PAYPALISHIRING", 3)` 返回 `"PAHNAPLSIIGYIR"`.


### 解题思路

如果nRows = 1， 那么直接返回。
如果nRows = 2, 转换字符串为：`PYAIHRNAPLSIIG`

	P	 Y	 A	 I	 H	 R	 N
	A	 P	 L	 S	 I	 I	 G
	
如果 nRows = 3  转换字符串为：`PAHNAPLSIIGYIR`

	P 		A		H		N
	A 	P 	L	S	I	I	G
	Y		I		R	
	
如果 nRows = 4 转换字符串为：`PINALSIGYAHRPI`

	P 			I			N
	A		L	S		I	G
	Y	A		H	R
	P			I

通过上面可以总结出一个规律，第一行和最后一行两个数据的间距为: `2 * nRows -2 `
中间第 i 行，第1列和它临近字符的间距为: `2*nRows -2 - 2 * i`
		

### 代码示例-Java


```
package com.yumo.java.airthmetic.leetcode;

/**
 * Created by yumodev on 8/16/16.
 */
public class ZigZag_6 {

    public static String convert(String s, int numRows){
        if (numRows <= 1 || s == null || s.length() == 0){
            return s;
        }

        StringBuilder sb = new StringBuilder();
        int size = 2 * numRows -2;
        for (int i = 0; i < numRows; i++){
            for (int j = i; j < s.length();j+= size){
                sb.append(s.charAt(j));
                if (i != 0 && i != numRows -1){
                    int temp = j + size - 2 * i;
                    if (temp < s.length()){
                        sb.append(s.charAt(temp));
                    }
                }
            }
        }

        return sb.toString();
    }

    public static void main(String[] args) {
       // String str = "PAYPALISHIRING";
        String str = "A";
        int nRows = 1;
        long startTime = System.nanoTime();
        String zigZag = convert(str, nRows);
        long endTime = System.nanoTime();
        long time = endTime - startTime;

        System.out.println("ZigZag:" + zigZag + " time:" + time);
    }
}
```

