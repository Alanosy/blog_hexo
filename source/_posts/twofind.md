---
title: 二分查找
date: 2022/11/18 21:52:22
tags: [C]
---
## 1 . 算法思想：

二分查找又称折半查找，适合对已经排好序的数据集合进行查找，时间复杂度为O(log2n),效率高。对一升序的数据集合，先找出升序数据集合最中间的元素，将数据划分为两个子集，将最中间的元素和关键字进行比较，如果相等则返回，如果大于关键字，则在前一个数据子集中查找，如果想小于反之，直至找到为止

## 2 . 查找步骤：

(1) 首先确定查找区间的中间位置（假定是一个升序的数组），那么mid = left + ( right - left ) / 2 ;
//为了防止越界
(2) 用待查找值与中间位置值进行比较，若相等，则找到，输出
(3) 若大于，则在后半区域中继续进行折半查找
(4) 若小于，则在前半区域中继续进行折半查找
(5) 查找成功，则返回数值的数组下标


## 3 . 代码实现
```
include <stdio.h>
int main()
{
	int arr[10] = { 1,2,3,4,5,6,7,8,9,10 };
	int k = 7;
	int sz = sizeof(arr) / sizeof(arr[0]);
	int left = 0;
	int right = sz - 1;

	while (left<=right)
	{
		//int mid = (left + right) / 2;
		int mid = left + (right - left) / 2;//防止数据过大，越界

		if (arr[mid] < k)
		{
			left = mid + 1;
		}
		else if (arr[mid] > k)
		{
			right = mid - 1;
		}
		else
		{
			printf("找到了，下标是:%d\n", mid);
			break;
		}
	}
	if (left > right)
		printf("找不到\n");

	return 0;
}



``` 