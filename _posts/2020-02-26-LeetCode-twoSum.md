---
layout: post
title:  "Coding LeetCode"
categories: algorithm
tags:  数组 哈希表
author: LWL
---

* content
{:toc}

## 题目：两数之和

给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。

你可以假设每种输入只会对应一个答案。但是，你不能重复利用这个数组中同样的元素。

Given an array of integers, return **indices** of the two numbers such that they add up to a specific target.

You may assume that each input would have ***exactly\*** one solution, and you may not use the *same* element twice.

示例:

给定 nums = [2, 7, 11, 15], target = 9

因为 nums[0] + nums[1] = 2 + 7 = 9
所以返回 [0, 1]



## Python：

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        dicts = {}
        for i, val in enumerate(nums):
            if target - val in dicts:
                return [dicts[target-val], i]
            dicts[val] = i
```



- 上述代码使用哈希表来解决问题，此方法效率是最高的，时间复杂度O(n)。但是消耗了一些额外空间，空间复杂度O(n)
- 其实暴力法是最容易想到的，也就是两次循环，不需要额外空间，但是时间复杂度是n**2。还有一些其他方法包括哈希表都是在暴力法上的优化。优化时间复杂度的一个思想就是空间换时间。实际应用中时间空间是需要我们来进行取舍的。



## Go：

```golang
func twosum(nums []int, target int) []int{
	maps := make(map[int]int)
	result := make([]int, 0)
	for index, num := range nums {
		_, isTrue := maps[target - num]
		if isTrue {
			result = append(result, maps[target - num])
			result = append(result, index)
			break
		}
		maps[num] = index
	}
	return result
}
```








