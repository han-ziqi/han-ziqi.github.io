---
title: 'LeetCode Day 01'
date: 2023-08-04
permalink: /posts/2023/08/LeetCodeDay1/
tags:
  - LeetCode
  - Algorithm

---

Before I start:

I recommend [installing a plugin](https://github.com/XYShaoKang/refined-leetcode) It can help to keep track of the time spent on the questions and understand your proficiency level.

1 [LeetCode 704 Binary search](https://leetcode.com/problems/binary-search/)

> Description: 
>
> Given an array of integers nums which is sorted in ascending order, and an integer target, write a function to search target in nums. If target exists, then return its index. Otherwise, return -1.
>
> You must write an algorithm with O(log n) runtime complexity.
> 
> 

Intuition:  use a binary search, which took 4 minutes and 40 seconds. Here is my solution: 

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        l, r = 0, len(nums)-1
        while l <= r:
            mid = (l + r) // 2
            if nums[mid] == target:
                return mid
            elif nums[mid] < target:
                l = mid + 1
            elif nums[mid] > target:
                r = mid - 1
        return -1
```

Because the given array is ascending order, it is possible to increase or decrease the ordinal number of the nums array directly after comparing and target's size in `elif`, which is the essence of binary lookup.

---

2 [LeetCode 27 remove element](https://leetcode.com/problems/remove-element/)

>Given an integer array `nums` and an integer `val`, remove all occurrences of `val` in `nums` [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm). The order of the elements may be changed. Then return *the number of elements in* `nums` *which are not equal to* `val`.
>
>Consider the number of elements in `nums` which are not equal to `val` be `k`, to get accepted, you need to do the following things:
>
>- Change the array `nums` such that the first `k` elements of `nums` contain the elements which are not equal to `val`. The remaining elements of `nums` are not important as well as the size of `nums`.
>- Return `k`.

Please note:

>**in-place algorithm** is an [algorithm](https://en.wikipedia.org/wiki/Algorithm) that operates directly on the input [data structure](https://en.wikipedia.org/wiki/Data_structure) without requiring extra space proportional to the input size. In other words, it modifies the input in place, without creating a separate copy of the data structure. An algorithm which is not in-place is sometimes called **not-in-place** or **out-of-place**.

Since the requirement is in place, there is no extra space to consider, only operations like swapping can be used.

For this question I used a double pointer, one head and one tail. As long as the head pointer is smaller than the tail pointer, the following operation is always performed:

- If the head pointer is pointing to a number that is not equal to the target, the head pointer goes forward one place.
- If the head pointer is the target number and the tail pointer is not the target number, then swap two number (there's no reason to swap the positions if the tail pointer also points to the target number), and then the head pointer goes forward one place, and the tail pointer goes backward one place.
- If neither of them is met (e.g. the head pointer is the target number, or both the head and tail pointers are the target number), then the tail pointer goes one place forward.

Time: 11 minutes 46 seconds

```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        i ,j = 0 ,len(nums) - 1
        while i <= j:
            if nums[i] != val:
                i += 1
            elif nums[i] == val and nums[j] != val:
                nums[i] , nums[j] = nums[j],nums[i]
                i +=1
                j -= 1
            else:
                j -=1
        return i
```

Attention, when solving problems with double pointers, don't forget to let a certain pointer move in every `if`, `elif`, otherwise it will cause the `while` dead loop.

The questions on the first day were not very difficult, I used my previous knowledge to get through them.
