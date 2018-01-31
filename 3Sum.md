# 3Sum

Given an array *S* of *n* integers, are there elements *a*, *b*, *c* in *S* such that *a* + *b* + *c* = 0? Find all unique triplets in the array which gives the sum of zero.

**Note:** The solution set must not contain duplicate triplets.

```
For example, given array S = [-1, 0, 1, 2, -1, -4],

A solution set is:
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```

## Solution

```javascript
var threeSum = function(nums) {
    nums.sort((a, b) => a - b)
    let len = nums.length
    let result = []
    
    for (let i = 0; i < len - 2; i++) {
        if (i === 0 || (i > 0 && nums[i] !== nums[i-1])) {
            let sum = 0 - nums[i]
            let left = i + 1
            let right = len - 1
            
            while (left < right) {
                if (nums[left] + nums[right] === sum) {
                    result.push([nums[i], nums[left], nums[right]])
                    let cur = nums[left]
                    while (left < right && nums[left] === cur) left++
                    cur = nums[right]
                    while (left < right && nums[right] === cur) right--
                } else if (nums[left] + nums[right] > sum) {
                    right--
                } else {
                    left++
                }
            }
        }
    }
    
    return result
}
```

## 心得

遇到数组的问题，先将其进行排序是一个很好的思路。3Sum 通过转化可以变为 2Sum 的问题，主要还是利用两边夹逼来进行比较。