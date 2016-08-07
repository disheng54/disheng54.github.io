---
layout: post
title: 4-Median of Two Sorted Arrays
category: leetcode
tags: [java, leetcode, airthmetic]
keywords: java,c++,javascript
description: 
---
[Median of Two Sorted Arrays](https://leetcode.com/problems/median-of-two-sorted-arrays/)

### 题目
There are two sorted arrays nums1 and nums2 of size m and n respectively.
Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).

Example 1:

```
nums1 = [1, 3]
nums2 = [2]
```

The median is 2.0
Example 2:

```
nums1 = [1, 2]
nums2 = [3, 4]
```

The median is (2 + 3)/2 = 2.5

### 翻译

有两个排序且长度分别为m和n的数组nums1 和 nums2。找出这两个排序的中间值。
要求运行时间为O(log(m+n))

示例1:

```
nums1 = [1, 3]
nums2 = [2]
```

中位值为： 2.0
示例2：

```
nums1 = [1, 2]
nums2 = [3, 4]
```

中位值： (2 + 3)/2 = 2.5

### 解决思路

题目的意思是将两个数组合并后，如果是奇数个，就返回中间的那个值，如果是偶数个，就返回中间两个数的平均值

* 合并的解决的方式

   首先想到的时候合并的方式解决，其原理就是合并两个数组，算出中位值，其运行时间为O((m+n)/2) .
   但是不能满足题目运行时间要求。
   
* 递归方式解决

   这种方式是在讨论区发现的。具体实现的原理：寻找数组中第 k(k=（m+n）/ 2+1)个最小的数字.
   将nums1[k] 和 nums2[k] 进行比较，会有三种情况：
   如果nums1[k] == nums2[k] 那么这个值就是要找的值。
   如果nums1[k] < nums2[k],那么第k个数值，必定出现在nums1[ (k+1) ~ m ] 和 nums2[ 0 ~ (k - 1)] 区间中
   如果nums1[k] > nums2[k],那么第k个数值，必定出现在nums1[ 0 ~ (k - 1)] 和 nums2[ (k+1) ~ n ] 区间中

### 代码示例-java


```
package com.yumo.java.airthmetic.leetcode;

/**
 * Created by yumodev on 8/7/16.
 */
public class MedianTwoSortedArrays_4 {

    /**
     * 通过合并的方式进行字符串处理.
     */
    public static double findMedianSortedArraysByMerge(int[] nums1, int[] nums2) {
        if (nums1.length == 0 && nums2.length == 0) return 0;
        int leftMedian = (nums1.length+nums2.length+1)/2;
        int rightMedian = (nums1.length+nums2.length+2)/2;
        if (nums1.length == 0){
            return (nums2[leftMedian - 1]+ nums2[rightMedian - 1]) / 2.0;
        }else if(nums2.length == 0){
            return (nums1[leftMedian - 1]+ nums1[rightMedian - 1]) / 2.0;
        }

        int num = 0, firstNum = 0;
        int n1 = 0, n2 = 0, index = 1;
        while (true){
            if (n1 < nums1.length){
                if (n2 < nums2.length){
                    if(nums1[n1] > nums2[n2]){
                        num = nums2[n2++];
                    }else{
                        num = nums1[n1++];
                    }
                }else{
                    num = nums1[n1++];
                }
            }else{
                num = nums2[n2++];
            }

            if (index == leftMedian && rightMedian == leftMedian){
                return num;
            }else if (index == leftMedian && rightMedian != leftMedian){
                firstNum = num;
            }else if (index == rightMedian){
                return (firstNum + num)/2.0;
            }

            index++;
        }
    }

    /**
     * 通过递归的方式实现.
     * @param nums1
     * @param nums2
     * @return
     */
    public static double findMedianSortedArraysByRecursive(int[] nums1, int[] nums2) {
        if (nums1.length == 0 && nums2.length == 0) return 0;
        int leftMedian = (nums1.length+nums2.length+1)/2;
        int rightMedian = (nums1.length+nums2.length+2)/2;

        if (nums1.length == 0){
            return (nums2[leftMedian - 1]+ nums2[rightMedian - 1]) / 2.0;
        }else if(nums2.length == 0){
            return (nums1[leftMedian - 1]+ nums1[rightMedian - 1]) / 2.0;
        }

        if (rightMedian != leftMedian){
            return (getMedianNum(nums1,0,nums2,0,leftMedian)+ getMedianNum(nums1,0,nums2,0,rightMedian))/2.0;
        }else{
            return getMedianNum(nums1,0,nums2,0,leftMedian);
        }
    }

    public static double getMedianNum(int[] nums1, int start1, int[]nums2, int start2, int index){
        if(start1 > nums1.length-1) return nums2[start2+index-1];
        if(start2 > nums2.length-1) return nums1[start1+index-1];
        if(index == 1) return Math.min(nums1[start1],nums2[start2]);

        if(start2+index/2-1 > nums2.length-1){
            return getMedianNum(nums1,start1+index/2,nums2,start2,index-index/2);
        } 
        if(start1+index/2-1 > nums1.length-1){
            return getMedianNum(nums1,start1,nums2,start2+index/2,index-index/2);
        } 

        if(nums1[start1+index/2-1] < nums2[start2+index/2-1]){
            return getMedianNum(nums1,start1+index/2,nums2,start2,index-index/2);
        }else{
            return getMedianNum(nums1,start1,nums2,start2+index/2,index-index/2);
        }
    }

    public static void main(String[] args){
        int[] nums1 = {1,3};
        int[] nums2 = {2};

//        int[] nums1 = {1,3};
//        int[] nums2 = {2};
        long startTime = System.nanoTime();
        double median = findMedianSortedArraysByMerge(nums1, nums2);
        long endTime = System.nanoTime();
        long time = endTime - startTime;
        System.out.println(" median:"+median +" time:"+ time);
        
        startTime = System.nanoTime();
        median = findMedianSortedArraysByRecursive(nums1, nums2);
        endTime = System.nanoTime();
        time = endTime - startTime;
        System.out.println(" median:"+median +" time:"+ time);
    }
}

```





