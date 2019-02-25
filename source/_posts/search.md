---
title: 查找算法-JAVA版本
date: 2017-09-11 11:53:10
tags: search
categories: 学习笔记
---


这篇文章占坑，要梳理一下查找算法。
--------------
<!--more-->
```
package Offer;

import java.util.Arrays;

public class search {
    public static void main(String[] args) {
        int[] numbers = { 10, 50, 20, 30, 100, 900, 400, 400 };
        System.out.println(SequelSearch(numbers, 100));
        System.out.println(BinarySearch(numbers, 100));

    }

    // 顺序查找

    public static int SequelSearch(int[] numbers, int a) {
        for (int i = 0; i < numbers.length; i++) {
            if (numbers[i] == a) {
                return i;
            }
        }
        return -1;
    }

    // 二分查找
    // 针对已排序从小到大.
    public static int BinarySearch(int[] numbers, int a) {
        int low = 0, high = numbers.length - 1;
        while (low <= high) {
            int mid = (low + high) / 2;
            if (numbers[mid] < a) {
                low = mid + 1;
            } else if (numbers[mid] > a) {
                high = mid - 1;
            } else
                return mid;
        }
        return -1;
    }
}


```