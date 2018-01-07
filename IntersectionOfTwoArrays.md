# IntersectionOfTwoArrays

Given two arrays, write a function to compute their intersection.

**Example:**
Given *nums1* = `[1, 2, 2, 1]`, *nums2* = `[2, 2]`, return `[2]`.

**Note:**

- Each element in the result must be unique.
- The result can be in any order.

## solution

```javascript
var intersection = function(nums1, nums2) {
    var map = {}
    nums1.forEach(num => map[num]=false)
    return nums2.filter(num => {
        if (map[num] !== undefined && map[num] === false) {
            map[num] = true
            return true
        }
        return false
    })
};

//use set
var intersection = function(nums1, nums2) {
    var arr = nums1.filter(num => nums2.includes(num))
    return [...new Set(arr)]
};
```

## 笔记

js 中对于数组去重，在 ES5 中可以使用对象字面量的方法（也即是 hash, 这种方法在去除重复元素的时候要能够及时的想到），有条件的话在 ES6 中使用 Set 可以更加很方便的去重。