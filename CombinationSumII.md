#  Combination Sum II

Given a collection of candidate numbers (**C**) and a target number (**T**), find all unique combinations in **C** where the candidate numbers sums to **T**.

Each number in **C** may only be used **once** in the combination.

**Note:**

- All numbers (including target) will be positive integers.
- The solution set must not contain duplicate combinations.

For example, given candidate set `[10, 1, 2, 7, 6, 1, 5]` and target `8`, 
A solution set is: 

```
[
  [1, 7],
  [1, 2, 5],
  [2, 6],
  [1, 1, 6]
]
```

## Solution

```javascript
/**
 * @param {number[]} candidates
 * @param {number} target
 * @return {number[][]}
 */
var combinationSum2 = function(candidates, target) {
    candidates.sort((a, b) => a - b)
    const result = []
    function backtrace(rest, idx, tlist) {
        if (rest < 0) {
            return
        } else if (rest === 0) {
            result.push(tlist.concat())
        } else {
            for (let i = idx; i < candidates.length; i++) {
                if (i == idx || candidates[i] !== candidates[i-1]) {
                    tlist.push(candidates[i])
                    backtrace(rest - candidates[i], i + 1, tlist)
                    tlist.pop()
                }
            }
        }
    }
    backtrace(target, 0, [])
    return result
};
```

## 心得

基本思路回溯法，先对数组进行排序可以更加容易去掉重复的元素