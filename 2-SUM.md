# 2-SUM

Given an array of integers, return **indices** of the two numbers such that they add up to a specific target.

You may assume that each input would have **exactly** one solution, and you may not use the *same* element twice.

**Example:**

```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].

```

## 解答：

```javascript
var twoSum = function(nums, target) {
    var dict = Object.create(null)
    var result;
    for (var i = 0; i < nums.length; i++) {
        var key = dict[nums[i]]
        if (key !== undefined) {
            result = [key, i]
        } else {
            dict[target - nums[i]] = i
        }
    }
    
    return result
};
```

## 笔记 

两个数字之间是存在着关系使得他们一一对应的，这个关系就是：`nums[i] = target - nums[j]` 。为表示这种一一对应的关系，最先想到的就是键值对来存储。小知识：`Object.create(null)` 创造的对象不含有原型的，相比对象字面量而言存储数据更好。