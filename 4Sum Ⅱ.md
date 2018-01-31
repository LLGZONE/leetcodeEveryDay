



# 4Sum Ⅱ

Given four lists A, B, C, D of integer values, compute how many tuples `(i, j, k, l)` there are such that `A[i] + B[j] + C[k] + D[l]` is zero.

To make problem a bit easier, all A, B, C, D have same length of N where 0 ≤ N ≤ 500. All integers are in the range of -228 to 228 - 1 and the result is guaranteed to be at most 231 - 1.

**Example:**

```
Input:
A = [ 1, 2]
B = [-2,-1]
C = [-1, 2]
D = [ 0, 2]

Output:
2

Explanation:
The two tuples are:
1. (0, 0, 0, 1) -> A[0] + B[0] + C[0] + D[1] = 1 + (-2) + (-1) + 2 = 0
2. (1, 1, 0, 0) -> A[1] + B[1] + C[0] + D[0] = 2 + (-1) + (-1) + 0 = 0
```

## Solution

```javascript
var fourSumCount = function(A, B, C, D) {
    const len = A.length
    const map = new Map()
    let result = 0
    
    for (let i = 0; i < len; i ++) {
        for (let j = 0; j < len; j ++) {
            let sum = A[i] + B[j]
            map.set(sum, map.has(sum) ? map.get(sum) + 1 : 1)
        }
    }
    
    for (let i = 0; i < len; i ++) {
        for (let j = 0; j < len; j ++) {
            let sum = C[i] + D[j]
            if (map.has(-sum)) {
                result += map.get(-sum)
            }
        }
    }
    
    return result
};
```

## 心得

题目思路与 2-sum 类似，需要注意的是相加的值可能相同，故用 value 来统计 key 出现次数