
## leetcode-gloang
leetcode解答golang语言版本

题目来源请参考力扣（LeetCode）

链接：https://leetcode-cn.com/problems

## 1. 两数之和

待补充

## 2. 两数相加

**解答思路**

这个题目有点类似于链表入门题”两个有序链表的合并“，大小的判断改成值的求和进制位

**解答代码**
```golang
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */

func addTwoNumbers(l1 *ListNode, l2 *ListNode) *ListNode {
    // 定义头指针
    var headNode *ListNode
    // 定义当前指针
    var current *ListNode
    // 进制位
    lastvalue := 0

    for l1 != nil || l2 != nil || lastvalue != 0 {
        // 默认为0
        v1 := 0
        v2 := 0
        // l1还有数据
        if l1 != nil {
            v1 = l1.Val
            // 跳动到下一个节点
            l1 = l1.Next
        }
        // l2还有数据
        if l2 != nil {
            v2 = l2.Val
            // 跳动到下一个节点
            l2 = l2.Next
        }
        // 结算，第一条+第二条+进制位
        resultVal := v1 + v2 + lastvalue

        var addNode ListNode
        addNode.Val = resultVal % 10
        lastvalue = resultVal / 10

        // 头结点为空，表示第一个节点
        if headNode == nil {
            // 头结点就是这个结点
            headNode = &addNode
            // 当前结点也是头结点
            current = headNode            
        } else {
            // 下一个节点是当前节点
            current.Next = &addNode
            // 当前节点滑动到下一个节点
            current = current.Next 
        }
    }
    
    return headNode
}
```

## 3.无重复字符串的最长子串

**解答思路**

最能想到的是暴力破解方法，但是更为优雅的左右滑动的窗口的办法

**解答代码**

```golang
// 暴力破解法
func havechongfu(s string) bool {
    l := len(s)
    for i:=0;i<l;i++ {
        for j:=i;j<l;j++ {
            if strings.Contains(s[j+1:l], string(s[i])) {
                return false
            }
        }
    }
    return true
}

func lengthOfLongestSubstring(s string) int {
 
    l := len(s)
    if l ==0 {
        return 0
    }
    
    for i:=0;i<l;i++ {
        findlen := l - i
        if findlen > 256 {
            continue
        }
        for j:=0;j<=l-findlen;j++ {
            strcut := s[j:j+findlen]
            if havechongfu(strcut) {
                return findlen
            }
        }
    }

    return 1
}
```

```golang
// 窗口滑动

```





