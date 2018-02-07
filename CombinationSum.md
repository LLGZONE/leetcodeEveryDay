# Combination Sum

Given a **set** of candidate numbers (**C**) **(without duplicates)** and a target number (**T**), find all unique combinations in **C** where the candidate numbers sums to **T**.

The **same** repeated number may be chosen from **C** unlimited number of times.

**Note:**

- All numbers (including target) will be positive integers.
- The solution set must not contain duplicate combinations.

For example, given candidate set `[2, 3, 6, 7]` and target `7`, 
A solution set is: 

```
[
  [7],
  [2, 2, 3]
]
```

## Solution

```javascript
/**
 * @param {number[]} candidates
 * @param {number} target
 * @return {number[][]}
 */
var combinationSum = function(candidates, target) {
    const sol = []
    candidates.sort((a,b) => a - b)
    function backtrace(target, index, tlist) {
        if (target < 0) return
        else if (target === 0) {
            sol.push(tlist)
        } else {
            for (let i = index; i < candidates.length; i++) {
                tlist.push(candidates[i])
                backtrace(target - candidates[i], i, tlist.slice())
                tlist.pop() // 回溯
            }
        }
    }
    
    backtrace(target, 0, [])
    return sol
};
```

## 心得

使用回溯法的思想可以很快地做出此题。