---
layout: post
title: 判断一个字符串里面的字符都是不相同的
category: airthmetic
tags: [java, String, airthmetic]
keywords: java 字符串 算法
description: 
---
### 题目

判断一个字符串里面的字符都是不相同的。

### 解决思路

这个问题有很多种解决方案，并且可以根据字符串字符集的不同，可以做不同的优化。有下面几种解决问题的思路

* 遍历字符串中的字符与字符串中的其他的字符比较。
* 可以将字符串进行排序，然后比较相邻的字符是否相等。
* 可以利用String方法的lastIndexOf() 方法进行比较。这个方法原理同上。
* 可以借助第三方的数据结构进行，比如Set，List， Map等等。
* 如果是ASCII字符集，那么通过构建一个长度为256默认为false的布尔数组，存在的字符设置为true，将该索引位置第二次设置为true时，就标志着有相同的字符。

### 实例代码

```
package com.yumo.java.string.test;

import java.util.Arrays;
import java.util.HashSet;
import java.util.Set;

/**
 * Created by yumo on 7/31/16.
 * 实现一个算法,判断一个字符串中的所有字符是否全都不同.
 */
public class AnalyzingStringsNoSame {
    private static final String LOG_TAG = "AnalyzingStringsNoSame";

    /**
     * 将字符串里面的字符取出放入到set中, 如果add 返回false,即认为有相同的字符
     * @param str
     * @return
     */
    public static boolean isSameBySet(String str){
        if (str == null){
            return false;
        }

        boolean noSame = true;
        Set<Character> set = new HashSet<>();
        for (int i = 0; i < str.length(); i++){
            if(!set.add(str.charAt(i))){
                noSame = false;
                break;
            }
        }
        return !noSame;
    }


    /**
     * 利用String 的 lastIndexOf(int) 来查找
     * @param str
     * @return
     */
    public static boolean isSameByIndex(String str){
        if (str == null){
            return false;
        }

        boolean noSame = true;

        for (int i = 0; i < str.length(); i++){
            if(str.lastIndexOf(str.charAt(i)) != i){
                noSame = false;
                break;
            }
        }
        return !noSame;
    }

    /**
     * 将字符串里面的字符和其他的字符串进行比较
     * @param str
     * @return
     */
    public static boolean isSameByTraverse(String str){
        if (str == null){
            return false;
        }

        boolean noSame = true;

        for (int i = 0; i < str.length(); i++){
            int ca = str.charAt(i);
            for (int j = i+1; j < str.length(); j++){
                if (ca == str.charAt(j)){
                    noSame = false;
                    break;
                }
            }
        }
        return !noSame;
    }


    /**
     * 将字符串排序,然后比较相邻的字符是否相等.
     * @param str
     * @return
     */
    public static boolean isSameBySort(String str){
        if (str == null){
            return false;
        }

        char[] caArr = str.toCharArray();
        Arrays.sort(caArr);

        boolean noSame = true;
        for (int i = 0; i < caArr.length-1;){
            if (caArr[i] == caArr[++i]){
                noSame = false;
                break;
            }
        }
        return !noSame;
    }

    /**
     * 如果字符串的为ASCII编码,如果字符串的长度大于256,就肯定存在相同的字符.
     * @param str
     * @return
     */
    public static boolean isAsciiSame(String str){
        if (str == null){
            return false;
        }

        if (str.length() > 256){
            return true;
        }

        boolean[] caArr = new boolean[256];

        boolean noSame = true;
        for (int i = 0; i < str.length(); i++){
            int ch = str.charAt(i);
            if (caArr[ch]){
                noSame = false;
                break;
            }
            caArr[ch] = true;
        }
        return !noSame;
    }

    public static void main(String[] args){
        System.out.println("testList");
        String str = "15234d";
        System.out.println("字符串:"+str);
        System.out.println("isSameBySet: "+AnalyzingStringsNoSame.isSameBySet(str));
        System.out.println("isSameByIndex: "+AnalyzingStringsNoSame.isSameByIndex(str));
        System.out.println("isSameByTraverse: "+AnalyzingStringsNoSame.isSameByTraverse(str));
        System.out.println("isSameBySort: "+AnalyzingStringsNoSame.isSameBySort(str));
        System.out.println("isAsciiSame: "+AnalyzingStringsNoSame.isAsciiSame(str));
    }
}
```






