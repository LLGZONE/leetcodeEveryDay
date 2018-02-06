#  Basic Calculator II

Implement a basic calculator to evaluate a simple expression string.

The expression string contains only **non-negative** integers, `+`, `-`, `*`, `/` operators and empty spaces ``. The integer division should truncate toward zero.

You may assume that the given expression is always valid.

Some examples:

```
"3+2*2" = 7
" 3/2 " = 1
" 3+5 / 2 " = 5

```

**Note:** **Do not** use the `eval` built-in library function.

## Solution

```javascript
var calculate = function(s) {
    const stack = []
    let opt = ''
    let sign = 1
    for (let i = 0; i < s.length; i++) {
        switch (s[i]) {
            case ' ':
                break;
            case '+':
                sign = 1
            	opt = '+'
                break
            case '-':
                sign = -1
            	opt = '-'
                break
            case '*':
                opt = '*'
                break
            case '/':
                opt = '/'
                break
            default:
                let num = 0
                while (i < s.length && s[i] >= '0' && s[i] <= '9') {
                    num = num * 10 + parseInt(s[i], 10)
                    i++
                }
                i--
                if (opt === '*') {
                    stack.push(stack.pop() * num)
                } else if (opt === '/') {
                    stack.push(Math.trunc(stack.pop() / num))
                } else {
                    stack.push(num * sign)
                }
                break
        }
    }
    return stack.reduce((a, b) => a + b)
};
```

## 心得

目前这个做法倒不是最优的，不过大体思路都差不多，主要是处理乘号与除号，这道题当然也可以不用到 stack，记录下上次的值与操作符即可，而且更快，空间复杂度也小。