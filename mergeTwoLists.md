# [合并两个有序链表](https://leetcode.cn/problems/merge-two-sorted-lists/)

将两个升序链表合并为一个新的 **升序** 链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。 

**示例 1：**

![](https://assets.leetcode.com/uploads/2020/10/03/merge_ex1.jpg)

**输入：** l1 = [1,2,4], l2 = [1,3,4]
**输出：** [1,1,2,3,4,4]

**示例 2：**

**输入：** l1 = [], l2 = []
**输出：** []

**示例 3：**

**输入：** l1 = [], l2 = [0]
**输出：** [0]

**提示：**

- 两个链表的节点数目范围是 `[0, 50]`
- `-100 <= Node.val <= 100`
- `l1` 和 `l2` 均按 **非递减顺序** 排列

## 题解

### 迭代 O(m+n)

```typescript
function mergeTwoLists(list1: ListNode | null, list2: ListNode | null): ListNode | null {
    const list = new ListNode();
    let head = list;

    while (list1 && list2) {
        if (list1.val < list2.val) {
            head.next = new ListNode(list1.val);
            list1 = list1.next;
        } else {
            head.next = new ListNode(list2.val);
            list2 = list2.next;
        }

        head = head.next;
    }

    return list.next;
}
```

### 递归 O(m+n)

```typescript
function mergeTwoLists(list1: ListNode | null, list2: ListNode | null): ListNode | null {
    if (!list1) {
        return list2;
    }

    if (!list2) {
        return list1;
    }

    return deep(list1, list2);
}

function deep(list1: ListNode | null, list2: ListNode | null): ListNode | null {
    if (!list1) {
        return list2;
    }

    if (!list2) {
        return list1;
    }

    if (list1.val < list2.val) {
        list1.next = deep(list1.next, list2);
        return list1;
    } else {
        list2.next = deep(list1, list2.next);
        return list2;
    }
}
```


