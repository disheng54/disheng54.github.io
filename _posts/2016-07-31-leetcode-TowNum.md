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

### 示例代码-Java


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
                result[0] = map.get(target - nums[i]);
                result[1] = i;
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
        int[] result = twoSumByHashMap(nums, target);
        long endTime = System.nanoTime();
        System.out.println(String.format("time :" + (endTime - startTime)+" [%d, %d]", result[0], result[1]));
    }
}
``` 

### 示例代码-c++


```
#include <iostream>
#include <vector>
#include <map>


using namespace std;

vector<int> twoSumByArraySort(vector<int>& nums, int target)
{
    map<int, int> ht;
    for (int i = 0; i < nums.size(); i++) {
        ht.insert(map<int,int>::value_type(nums[i], i));
    }
    vector<int> res(2, -1);
    sort(nums.begin(), nums.end());
    int begin = 0;
    int end = nums.size() -1;

    while(begin < end){
        if(nums[begin] + nums[end] == target){
            res[0] = min(ht.find(nums[begin])->second, ht.find(nums[end])->second);
            res[1] = max(ht.find(nums[begin])->second, ht.find(nums[end])->second);
            break;
        }else if (nums[begin] + nums[end] < target){
            begin ++;
        }else {
            end --;
        }
    }
    return res;
}

int main() {
    vector<int> nums = {2,7,11,15};
    int target = 9;

    clock_t start, finish;

    start = clock();
    vector<int> result = twoSumByMap(nums, target);
    finish = clock();
    cout << "time:"<<((double)(finish - start)/CLOCKS_PER_SEC)* 1000000 <<" twoSumByMap:" <<"["<<result[0]<<","<<result[1]<<"]"<<endl;


    return 0;
}
```

### 示例代码-JavaScript


```
var twoSumByMap = function(nums, target) {
    var map = {};
    for(var i in nums){
      if(map[target-nums[i]] !== undefined){
        return [parseInt(map[target-nums[i]]),parseInt(i)];
      }else{
      map[nums[i]] = i;
      }
    }
};

var nums = [0,4,3,0];
var target = 0;
var beginTime = new Date().getTime();
var result = twoSumByMap(nums, target);
var endTime = new Date().getTime();
console.log("Time:"+(endTime - beginTime)+" result:"+result);
```




