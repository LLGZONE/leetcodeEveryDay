

# Add 2-NUMS

You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order** and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Example**

```
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.
```

## solution

```javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */
var addTwoNumbers = function(l1, l2) {
    var list, rest = 0, head
    list = head = new ListNode(0)
    var sum = l1.val + l2.val
    if (sum >= 10) {
        head.val = sum - 10
        rest = 1
    } else {
        head.val = sum
        rest = 0
    }
    l1 = l1.next
    l2 = l2.next
    while(l1) {
        list.next = new ListNode(0)
        sum = l1.val + l2.val
        if (sum >= 10) {
            list.val = sum - 10 + rest
            rest = 1
        } else {
            list.val = sum + rest
            rest = 0
        }
        l1 = l1.next
        l2 = l2.next
        list = list.next
    }
    if (rest) {
        list.next = new ListNode(rest)
    }
    return head
};
```

## 笔记

题目难度不大，写得有些啰嗦，个人觉得其他人不错的解答如下:

```javascript
var addTwoNumbers = function(l1, l2) {
    var nextNode = new ListNode(0);
    var head = nextNode;
    var carryover = 0;
    
    while(true){      
        
        if(l1 != null ){
            nextNode.val += l1.val;
            l1 = l1.next;
        }
        
        if(l2 != null){
            nextNode.val += l2.val;
            l2 = l2.next;
        }
        
        if(nextNode.val > 9){
            var r = nextNode.val % 10;
            carryover = (nextNode.val - r) / 10;
            nextNode.val = r;
        }
        
        if(carryover == 0 && l1 == null && l2 == null){
            return head;
        }
        
        nextNode.next = new ListNode(carryover);
        nextNode = nextNode.next;
        carryover = 0;
    }
 
    return head;
};
```

