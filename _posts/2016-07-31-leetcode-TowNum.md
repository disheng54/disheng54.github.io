---
layout: post
title: 1-Two Sum
category: leetcode
tags: [java, leetcode, airthmetic]
keywords: java
description: 
---

原链接:[Two Sum](https://leetcode.com/problems/two-sum/)

### 原题目
Given an array of integers, return indices of the two numbers such that they add up to a specific target.
You may assume that each input would have exactly one solution.
Example:

```
Given nums = [2, 7, 11, 15], target = 9,
Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

### 翻译

给定一个整型数组，如果该数组中有两个数值的和等于一个特定值，就返回这两个数值在数组中的索引。
假定有唯一的解决方案。
示例:

```
Given nums = [2, 7, 11, 15], target = 9,
Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

### 解决思路

* 假定有一个Map，遍历寻找`target-nums[n] `为key对应的value，如果找不到就将nums[n]和索引n作为存放于Map中。

* 先将数组排序，然后利用二分查找的方式，找到合适的索引。

### 代码示例(Java)


```
package com.yumo.java.airthmetic.leetcode;

import java.util.Arrays;
import java.util.HashMap;
import java.util.Map;

/**
 * Created by yumo on 7/31/16.
 * Given an array of integers, return indices of the two numbers such that they add up to a specific target.

 You may assume that each input would have exactly one solution.

 Example:
 Given nums = [2, 7, 11, 15], target = 9,

 Because nums[0] + nums[1] = 2 + 7 = 9,
 return [0, 1].
 */
public class TwoSum_1 {

    /**
     * 通过将数组排序,然后查找来实现
     * @param nums
     * @param target
     * @return
     */
    public static int[] twoSumByArraySort(int[] nums, int target){
        Arrays.sort(nums);
        int begin = 0;
        int end = nums.length -1;
        int[] result = new int[2];

        while (begin < end){
            int num = nums[begin] + nums[end];
            if (num == target){
                result[0] = begin + 1;
                result[1] = end + 1;
                break;
            } else if (num < target){
               begin ++;
            } else{
                end --;
            }
        }

        return result;
    }


    /**
     * 通过hashMap实现
     * @param nums
     * @param target
     * @return
     */
    public static int[] twoSumByHashMap(int[] nums, int target){
        int[] result = new int[2];
        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++){
            if(map.get(target - nums[i]) != null){
                result[0] = map.get(target - nums[i]) + 1;
                result[1] = i + 1;
                break;
            }

            map.put(nums[i], i);
        }
        return result;
    }

    public static void main(String[] args){
        int[] nums = {2,7,11,15};
        int target = 9;
        long startTime = System.nanoTime();
        int[] result = twoSumByArraySort(nums, target);
        long endTime = System.nanoTime();
        System.out.println(String.format("time :" + (endTime - startTime)+" [%d, %d]", result[0], result[1]));

        startTime = System.nanoTime();
        result = twoSumByHashMap(nums, target);
        endTime = System.nanoTime();
        System.out.println(String.format("time :" + (endTime - startTime)+" [%d, %d]", result[0], result[1]));
    }
}
``` 

