---
title: 排序算法-JAVA版本
date: 2017-08-21 11:53:10
tags: sort
categories: 学习笔记
---


这篇文章占坑，要梳理一下排序算法。
--------------
<!--more-->
```
package Offer;

import java.util.Arrays;

public class Sorting {
	public static void main(String[] args) {
		int[] numbers = {10, 50, 20, 30, 100, 900, 400, 400};
		System.out.println("冒泡排序:" + Arrays.toString(bubbleSort(numbers)));
		System.out.println("选择排序:" + Arrays.toString(selectSort(numbers)));
		System.out.println("插入排序:" + Arrays.toString(insertSort(numbers)));
		System.out.println("希尔排序:" + Arrays.toString(shellSort(numbers)));
		System.out.println("归并排序:" + Arrays.toString(mergeSort(numbers,0,numbers.length-1)));
		System.out.println("快速排序:" + Arrays.toString(quickSort(numbers,0,numbers.length-1)));
	}

	// 冒泡排序
	// 遍历比较全体元素,如果相邻两个元素顺序不一致,则交换.
	public static int[] bubbleSort(int[] numbers) {
		int temp = 0;
		int size = numbers.length;
		for (int i = 0; i < size - 1; i++) {
			for (int j = 0; j < size - 1 - i; j++) {
				if (numbers[j] > numbers[j + 1]) // 交换两数位置
				{
					temp = numbers[j];
					numbers[j] = numbers[j + 1];
					numbers[j + 1] = temp;
				}
			}
		}
		return numbers;
	}
	//选择排序
	//寻找未排序最小元素与自身交换位置
	public static int[] selectSort(int[] numbers) {
		int temp = 0;
		int size = numbers.length;
		for(int i = 0; i < size ; i++) {
			int k = i ; 
			// 选取最小元素
			for(int j = i + 1; j < size ; j++){
				if (numbers[j] < numbers[k]) {
					k = j;
				}
			}
			// 交换位置z，自身最小无须交换
			if(i != k) {
				temp = numbers[i];
				numbers[i] = numbers[k];
				numbers[k] = temp;
			}
		}		
		return numbers;
	}
	//插入排序
	//将未排序元素向前扫描，插入在小于后面且大于前面的位置
	public static int[] insertSort(int[] numbers) {
		int temp = 0;
		int size = numbers.length;
		int j = 0;
		for(int i = 0; i < size ; i++) {
			temp = numbers[i];
			//后移较大元素
			for(j = i; j > 0 && temp < numbers[j-1]; j--) {
				numbers[j] = numbers[j-1];
			}
			numbers[j] = temp;
		}			
		return numbers;
	}
	//希尔排序 插入排序的变形
    public static int[] shellSort(int[] arr){
    	int gap = 1, i, j, len = arr.length;
        int temp;
        while (gap < len / 3)
            gap = gap * 3 + 1;      // <O(n^(3/2)) by Knuth,1973>: 1, 4, 13, 40, 121, ...
        for (; gap > 0; gap /= 3) {
            for (i = gap; i < len; i++) {
                temp = arr[i];
                for (j = i - gap; j >= 0 && arr[j] > temp; j -= gap)
                    arr[j + gap] = arr[j];
                arr[j + gap] = temp;
            }
        }
        return arr;
    }
	//归并排序
	public static int[] mergeSort(int[] nums, int low, int high) {
        int mid = (low + high) / 2;
        if (low < high) {
            // 左边
        	mergeSort(nums, low, mid);
            // 右边
        	mergeSort(nums, mid + 1, high);
            // 左右归并
            merge(nums, low, mid, high);
        }
        return nums;
    }
    public static void merge(int[] nums, int low, int mid, int high) {
        int[] temp = new int[high - low + 1];
        int i = low;// 左指针
        int j = mid + 1;// 右指针
        int k = 0;

        // 把较小的数先移到新数组中
        while (i <= mid && j <= high) {
            if (nums[i] < nums[j]) {
                temp[k++] = nums[i++];
            } else {
                temp[k++] = nums[j++];
            }
        }

        // 把左边剩余的数移入数组
        while (i <= mid) {
            temp[k++] = nums[i++];
        }

        // 把右边边剩余的数移入数组
        while (j <= high) {
            temp[k++] = nums[j++];
        }

        // 把新数组中的数覆盖nums数组
        for (int k2 = 0; k2 < temp.length; k2++) {
            nums[k2 + low] = temp[k2];
        }
    }
    //快速排序       
    private static int getMiddle(int[] list, int low, int high) {  
        int tmp = list[low];    //数组的第一个作为中轴  
        while (low < high) {  
            while (low < high && list[high] >= tmp) {  
                high--;  
            }  
      
      
            list[low] = list[high];   //比中轴小的记录移到低端  
            while (low < high && list[low] <= tmp) {  
                low++;  
            }  
      
      
            list[high] = list[low];   //比中轴大的记录移到高端  
        }  
        list[low] = tmp;              //中轴记录到尾  
        return low;                  //返回中轴的位置  
    }  
      
      
    private static int[] quickSort(int[] list, int low, int high) {  
        if (low < high) {  
            int middle = getMiddle(list, low, high);  //将list数组进行一分为二  
            quickSort(list, low, middle - 1);      //对低字表进行递归排序  
            quickSort(list, middle + 1, high);      //对高字表进行递归排序  
        }  
        return list;
    }  
    
}


```