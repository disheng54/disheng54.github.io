---
layout: post
title: 26-Remove Duplicates from Sorted Array
category: leetcode
tags: [java, leetcode, airthmetic]
keywords: java
description: 
---

[26. Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)

### 原题目
Given a sorted array, remove the duplicates in place such that each element appear only once and return the new length.

Do not allocate extra space for another array, you must do this in place with constant memory.

For example,
Given input array nums =` [1,1,2]`,

Your function should return length = `2`, with the first two elements of nums being 1 and 2 respectively. It doesn't matter what you leave beyond the new length.

### 翻译

给定一个排好序的数组，移除重复的元素，然后返回新的数组长度。
要求不能额外一个数组大小的空间来实现，要求使用空间实现，
比如：输入数组=` [1,1,2]`,
你的方法将返回长度为=`2`，两个元素分别是1和2。这个方法并不关心新长度。

### 解题思路

首先这是一个已经排好序的数组，又要求不能额外的分配一个数组空间来实现。
所以我们可以利用遍历一遍数组来实现。利用前后两个索引值i,j分别向后移动来
实现去重有序数组的大小。
时间复杂度为O(n)
空间复杂度为O(2)

### 代码示例-Java


```
/**
 * Created by yumodev on 9/18/16.
 */
public class RemoveDuplicates_26 {

    public static int removeDuplicates(int[] nums){
        if (nums == null){
            return 0;
        }

        if (nums.length <= 1){
            return 1;
        }

        int i = 0, j = 1;
        while (i <nums.length && j < nums.length){
            if (nums[i] == nums[j]){
                j++;
            }else{
                nums[++i] = nums[j];
                j++;
            }
        }

        return i+1;
    }

    public static void main(String[] args){
        int[] nums = {2,7,11,15};
        long startTime = System.nanoTime();
        int result = removeDuplicates(nums);
        long endTime = System.nanoTime();
        long time = endTime - startTime;

        System.out.println(" removeDuplicates:" + result + " time:" + time);
    }
}
```



