
# leetcode-gloang
leetcode解答golang语言版本

来源：力扣（LeetCode）

链接：https://leetcode-cn.com/problems


## 1. 两数之和

待补充

## 2. 两数相加

**题目描述**

给出两个 非空 的链表用来表示两个非负的整数。其中，它们各自的位数是按照 逆序 的方式存储的，并且它们的每个节点只能存储 一位 数字。

如果，我们将这两个数相加起来，则会返回一个新的链表来表示它们的和。

您可以假设除了数字 0 之外，这两个数都不会以 0 开头。

示例：
```
输入：(2 -> 4 -> 3) + (5 -> 6 -> 4)
输出：7 -> 0 -> 8
原因：342 + 465 = 807
```

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



