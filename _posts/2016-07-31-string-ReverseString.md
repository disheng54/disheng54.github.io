---
layout: post
title: 反转一个字符串
category: 字符串
tags: [java, String, airthmetic]
keywords: java 字符串 算法
description: 
---
### 题目

将一个字符串反转

### 解决思路

这是一个常见的问题，在实际的开发中也经常用到，解决的方法有很多种。我使用下面四种方法进行，并且最后比较其中的效率。
 
* 利用系统自带的StringBuilder.reverse()  进行反转。
* 使用将字符串转换为字符数据，然后进行二分反转。
* 使用字符的异或进行转换。
* 使用Stack数据结构进行反转。

### 实例代码


```
/**
     * 利用系统自带的StringBuilder.reverse() 进行反转
     * @param str
     * @return
     */
    public static String reverseByStringBuilder(String str){
        if (str == null){
            return "";
        }
        return new StringBuilder(str).reverse().toString();
    }

    /**
     * 使用字符串进行二分反转
     * @return
     */
    public static String reverseByCharArray(String str){
        if (str == null){
            return "";
        }

        char[] chArr = str.toCharArray();
        int len = chArr.length;
        for (int i = (len-1) / 2; i >= 0; i--){
            char c = chArr[i];
            chArr[i] = chArr[len - i -1];
            chArr[len - i -1] = c;
        }

        return new String(chArr);
    }

    /**
     * 使用异或进行翻转
     * 将二进制 a = 1101, b = 1000 进行反转.
     * 1  a = 1101 ^ 1000 此时 a = 1010, b = 1000
     * 2  b = 1000 ^ 1010 此时 a = 1010, b = 1101
     * 3  a = 1101 ^ 1010 此时 a = 1000, b = 1101
     * @return
     */
    public static String reverseByXor(String str){
        if (str == null){
            return "";
        }

        char[] chArr = str.toCharArray();
        int len = chArr.length ;
        for (int i = 0, j = len -1; i < len/2; i++, j--){
            chArr[i] = (char)(chArr[i]^chArr[j]);
            chArr[j] = (char)(chArr[j]^chArr[i]);
            chArr[i] = (char)(chArr[j]^chArr[i]);
        }

        return new String(chArr);
    }

    /**
     * 使用栈进行翻转
     * @param str
     * @return
     */
    public static String reverseByStack(String str){
        if (str == null){
            return "";
        }

        Stack<Character> stack = new Stack<>();
        int len = str.length();
        for (int i = 0; i < len; i++){
            stack.push(str.charAt(i));
        }

        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < len; i++){
            sb.append(stack.pop());
        }
        return sb.toString();
    }



    public static void main(String[] args){
        System.out.println("testList");
        String str="";
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i<= 10000; i++){
            sb.append(i+"");
        }
        str = sb.toString();


        long startTime = System.nanoTime();
        String str1 = reverseByStringBuilder(str);
        long endTime = System.nanoTime();
        System.out.println(" time:"+(endTime - startTime)+"    StringBuilder.reverse(): "+str1);


        startTime = System.nanoTime();
        str1 = reverseByCharArray(str);
        endTime = System.nanoTime();
        System.out.println(" time:"+(endTime - startTime)+"    reverseByCharArray: "+str1);

        startTime = System.nanoTime();
        str1 = reverseByXor(str);
        endTime = System.nanoTime();
        System.out.println(" time:"+(endTime - startTime)+"    reverseByXor: "+str1);

        startTime = System.nanoTime();
        str1 = reverseByStack(str);
        endTime = System.nanoTime();
        System.out.println(" time:"+(endTime - startTime)+"    reverseByStack: "+str1);
    }
}
```


### 效率比较 单位是纳秒

* 对长度为10的字符串进行反转

		StringBuilder.reverse() time:14000  
		reverseByCharArray time:7000 
		reverseByXor time:4000 
		reverseBystack time:315000 
		
		
* 对长度为100的字符串进行反转

        StringBuilder.reverse() time:29000  
	    reverseByCharArray time:11000 
        reverseByXor time:9000 
        reverseBystack time:589000 
        
* 对长度为1000的字符串进行反转

		StringBuilder.reverse() time:295000 
		reverseByCharArray time:72000 
		reverseByXor time:76000
		reverseBystack time:3949000
		
* 对长度为10000的字符串进行反转

		StringBuilder.reverse() time:3321000
		reverseByCharArray time:966000 
		reverseByXor time:1421000
		reverseBystack time:18414000 
		
		
* 结果比较

   在字符串较短的情况下通过异或反转所用的时间是最短的，二分数组仅次之。
   在字符串较长的情况下使用二分数组的是花费时间最短的。
   使用栈进行反转花费的时间时间最长是二分数组反转的两个数量级。
   





