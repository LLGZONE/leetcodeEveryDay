# Group Anagrams

Given an array of strings, group anagrams together.

For example, given: `["eat", "tea", "tan", "ate", "nat", "bat"]`, 
Return:

```
[
  ["ate", "eat","tea"],
  ["nat","tan"],
  ["bat"]
]
```

## Solution

```javascript
var groupAnagrams = function(strs) {
    const map = new Map()
    const result = []
    
    strs.forEach(str => {
        const key = str.split('').sort().join('')
        if (map.has(key)) {
            map.get(key).push(str)
        } else {
            map.set(key, [str])
        }
    })
    
    for (let [key, value] of map) {
        result.push(value)
    }
    
    return result
};
```

## 心得

这道题主要就是选取字母相同的字符串，很容易想到对每个字符串进行排序，然后比较即可，主要是如果通过遍历进行依次比较会很复杂而且面临着分组的问题。可以发现其实存在着一个字符串对应一个组的关系，也就很容易想到使用hashmap 来完成，从最近几次做题来说，hashmap 是一个应用很广泛的做法，可以解决许多的棘手问题。