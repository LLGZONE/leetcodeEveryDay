# Merge Intervals

Given a collection of intervals, merge all overlapping intervals.

For example,
Given `[1,3],[2,6],[8,10],[15,18]`,
return `[1,6],[8,10],[15,18]`.

## Solution

```javascript
var merge = function(intervals) {
    if (intervals.length === 0) {
        return []
    }
    intervals.sort(function(a,b){return a.start - b.start})
    const result =[intervals[0]]
    let last = 0

    intervals.forEach(function(interval) {
        const iv = result[last]
        if (interval.start > iv.end) {
            result.push(interval)
            last++
        } else if (interval.end > iv.end) {
                iv.end = interval.end
        }
    })
    
    return result
};
```

## 心得

对数组进行排序后可以省下很多的判断步骤，排序后数组后一个 interval start 总会大于前一个 interval，接下来的判断也就很简单了。做与数组相关的题目，乱序变为有序后，做起来会简单很多