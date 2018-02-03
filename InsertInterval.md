# Insert Interval

Given a set of *non-overlapping* intervals, insert a new interval into the intervals (merge if necessary).

You may assume that the intervals were initially sorted according to their start times.

**Example 1:**
Given intervals `[1,3],[6,9]`, insert and merge `[2,5]` in as `[1,5],[6,9]`.

**Example 2:**
Given `[1,2],[3,5],[6,7],[8,10],[12,16]`, insert and merge `[4,9]` in as `[1,2],[3,10],[12,16]`.

This is because the new interval `[4,9]` overlaps with `[3,5],[6,7],[8,10]`.

## Solution

```javascript
var insert = function(intervals, newInterval) {
    let flag = true
    let len = intervals.length
    
    for (let i = 0; i < len - 1; i++) {
        if (intervals[i].start <= newInterval.start && intervals[i+1].start >= newInterval.start) {
            intervals.splice(i+1, 0, newInterval)
            flag = false
            break
        }
    }
    
    if (flag) {
        if (len === 0 || intervals[len-1].start < newInterval.start) {
            intervals.push(newInterval)
        } else if (intervals[0].start >= newInterval.start) {
            intervals.unshift(newInterval)
        }
    }
    
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

与 Merge Interval 思想类似，不过由于初始已经排好序了，故可以把时间复杂度控制在 O(n)。