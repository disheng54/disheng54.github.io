---
layout: post
title: 20-Valid Parentheses
category: leetcode
tags: [java, leetcode, airthmetic]
keywords: java
description: 
---

[20. Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)

### 原题目

Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.
The brackets must close in the correct order, "()" and "()[]{}" are all valid but "(]" and "([)]" are not.

### 翻译

给一个仅包含'(', ')', '{', '}', '[' 和 ']'的字符串，然后判断这个字符串是否是有效的。
括号必须按照顺序进行闭合，比如"()" 和 "()[]{}" 都是有效的，但是 "(]" 和 "([)]" 不是有效的.

### 解题思路

这是一个典型的栈应用的例子。如果是字符'('，'[', '{', 将其压入栈，如果是')',']','}'
就从栈中取顶部字符，如果栈为空或者不相匹配，那么就可以认定是无效的。
如果和栈顶元素匹配，就继续遍历字符串判定。
时间复杂度：O(n)
空间复杂度：O(2)

### 代码示例


```
 public static boolean isValid(String s) {
        if (s == null ||s.length() <= 1){
            return false;
        }

        Stack<Character> stack = new Stack<>();
        for (int i = 0; i <= s.length()-1;i++){
            Character ch = s.charAt(i);
            if (ch == '(' || ch == '[' || ch == '{'){
                stack.push(ch);
            }else{
                if (stack.size() == 0){
                    return false;
                }

                Character sch = stack.pop();

                if (ch == ')'){
                    if (sch != '('){
                        return false;
                    }
                }else if (ch == ']'){
                    if (sch != '['){
                        return false;
                    }
                }else if (ch == '}'){
                    if (sch != '{'){
                        return false;
                    }
                }
            }
        }
        return stack.size() == 0;
    }
```



