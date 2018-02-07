# Spiral Matrix

Given a matrix of *m* x *n* elements (*m* rows, *n* columns), return all elements of the matrix in spiral order.

For example,
Given the following matrix:

```
[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]

```

You should return `[1,2,3,6,9,8,7,4,5]`.

## Solution

```javascript
/**
 * @param {number[][]} matrix
 * @return {number[]}
 */
var spiralOrder = function(matrix) {
    if (matrix.length === 0) {
        return []
    }
    const w = matrix[0].length
    const h = matrix.length
    const arr = Array(w).fill(false)
    const m = (Array(h).fill(0)).map(a => arr.concat())
    const result = []
    let x = 0
    let y = 0
    let direction = 'r'
    
    while (x < w && x >= 0 && y < h && y >= 0) {
        if (m[y][x]) {
            break
        }
        result.push(matrix[y][x])
        m[y][x] = true
        switch (direction) {
            case 'r':
                if (x === w - 1 || m[y][x+1]) {
                    direction = 'd'
                    y ++
                } else {
                    x++
                }
                break
            case 'd':
                if (y === h - 1 || m[y+1][x]) {
                    direction = 'l'
                    x--
                } else {
                    y++
                }
                break
            case 'l':
                if (x === 0 || m[y][x-1]) {
                    direction = 'u'
                    y--
                } else {
                    x--
                }
                break
            case 'u':
                if (y === 0 || m[y-1][x]) {
                    direction = 'r'
                    x++
                } else {
                    y--
                }
                break
        }
    }
    
    return result
};

// 最快的方法
var spiralOrder = function(matrix) {
    if (!matrix || matrix.length === 0 || matrix[0].length === 0) return [];
    const row = matrix.length;
    const col = matrix[0].length;
    
    let top = 0;
    let bottom = row - 1;
    let left = 0;
    let right = col - 1;
    
    const dirs = [
        [0, 1],
        [1, 0],
        [0, -1],
        [-1, 0],
    ];
    
    let dirIndex = 0;
    
    const soln = [];
    let i = 0;
    let j = 0;
    
    while (left <= right && top <= bottom) {
        //console.log(i, j);
        soln.push(matrix[i][j]);
        i += dirs[dirIndex][0];
        j += dirs[dirIndex][1];
       // console.log(i, j);
        if (i < top || i > bottom || j < left || j > right) {
            i -= dirs[dirIndex][0];
            j -= dirs[dirIndex][1];
           // console.log(i, j);
            
            switch (dirIndex) {
                case 0:
                    top++;
                    break;
                case 1:
                    right--;
                    break;
                case 2:
                    bottom--;
                    break;
                case 3:
                    left++;
                    break;
            }
            
            dirIndex = (dirIndex + 1) % dirs.length;
            i += dirs[dirIndex][0];
            j += dirs[dirIndex][1];
            //console.log(i, j);
        }
        //console.log(i, j);
        //console.log('---')
    }
    return soln;
};
```

## 心得

这道题主要思路是按照方向进行遍历，到达边界时或者下一格已经遍历过时便改变方向，第一种方法基本就是按照这个思路，第二种方法则是每改变一次方向，则边界向里进一行，这样就没有必要再判断是否已经遍历过，节省了创造二维数组的时间。