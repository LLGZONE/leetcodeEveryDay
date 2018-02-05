# Basic Calculator

Implement a basic calculator to evaluate a simple expression string.

The expression string may contain open `(` and closing parentheses `)`, the plus `+` or minus sign `-`, **non-negative** integers and empty spaces ``.

You may assume that the given expression is always valid.

Some examples:

```
"1 + 1" = 2
" 2-1 + 2 " = 3
"(1+(4+5+2)-3)+(6+8)" = 23

```

**Note:** **Do not** use the `eval` built-in library function.

## Solution

```javascript
/**
 * @param {string} s
 * @return {number}
 */
var calculate = function(s) {
    const stack = []
    let sum = 0
    let sign = 1
    
    for (let i = 0; i < s.length; i++) {
        let c = s[i]
        switch (c) {
            case ' ':
                break
            case '+':
                sign = 1
                break
            case '-':
                sign = -1
                break
            case '(':
                stack.push(sum)
                stack.push(sign)
                sum = 0
                sign = 1
                break
            case ')':
                sum *= stack.pop()
                sum += stack.pop()
                break
            default: {
                let num = 0
                while(i < s.length && s[i] >= '0' && s[i] <= '9') {
                    num = num * 10 + parseInt(s[i++], 10)
                }
                i--
                sum += num * sign
                break
            }              
        }
    }
    return sum
};
```

## 心得

实现一个简易计算器，遇到左括号就将 sum与符号位 压入栈中，遇到右括号将 sum与符号位 弹出栈，还需要注意由于是一个一个字符的取，故两位数及以上要通过计算得到。