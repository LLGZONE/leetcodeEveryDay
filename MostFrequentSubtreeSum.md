# Most Frequent Subtree Sum

Given the root of a tree, you are asked to find the most frequent subtree sum. The subtree sum of a node is defined as the sum of all the node values formed by the subtree rooted at that node (including the node itself). So what is the most frequent subtree sum value? If there is a tie, return all the values with the highest frequency in any order.

**Examples 1**
Input:

```
  5
 /  \
2   -3

```

return [2, -3, 4], since all the values happen only once, return all of them in any order.

**Examples 2**
Input:

```
  5
 /  \
2   -5

```

return [2], since 2 happens twice, however -5 only occur once.

**Note:** You may assume the sum of values in any subtree is in the range of 32-bit signed integer.

## Solution

**第一版答案:**

```javascript
var findFrequentTreeSum = function(root) {
    let sums = new Map()
    let max = 0
    let result = []
    ;(function subTreeSum(root) {
        if (root) {
            subTreeSum(root.left)
            subTreeSum(root.right)
            let sum = addNode(root)
            if (sums.has(sum)) {
                sums.set(sum, sums.get(sum) + 1)
            } else {
                sums.set(sum, 1)
            }
        }
    })(root)
    for (let [key, value] of sums) {
        if (value > max) {
            max = value
        }
    }
    for (let [key, value] of sums) {
        if (value === max) {
            result.push(key)
        }
    }
    return result
};


function addNode(node) {
    if (node) {
        return node.val + addNode(node.left) + addNode(node.right)
    }
    return 0
}
```

**优化后:**

```javascript
var findFrequentTreeSum = function(root) {
    let map = new Map()
    let maxes = []
    let max = 0
    subTreeSum(root, map)
    map.forEach((value, key) => {
        if (value > max) {
            max = value
            maxes = [key]
            return
        }
        if (max === value) {
            maxes.push(key)
        }
    })
    return maxes
};

function subTreeSum(root, map) {
    if (root===null) return 0
    let sum = root.val + subTreeSum(root.left, map) + subTreeSum(root.right, map)
    let prev = map.get(sum)
    map.set(sum, prev ? prev + 1 : 1)
    return sum
}
```

## 心得

仅使用 object 不能保证遍历的顺序， Map 可以按照定义时的顺序遍历。比较优化前与优化后，思路是一样的，但更简洁也更快。