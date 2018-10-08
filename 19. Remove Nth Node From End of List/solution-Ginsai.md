给定一个链表，删除链表的倒数第 n 个节点，并且返回链表的头结点。

示例：

给定一个链表: 1->2->3->4->5, 和 n = 2.

当删除了倒数第二个节点后，链表变为 1->2->3->5.

- 思路：
双指针，一个指针提前走n+1个节点，随后两个指针一起往后走，当前面的指针为null时，此时后面的指针位于要删除节点之前，再进行节点删除，
使用一个dummy节点来避开只有一个节点的情况

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode dummy=new ListNode(-1);
        dummy.next=head;
        ListNode p1=dummy;
        ListNode p2=dummy;
        for(int i=0;i<n+1;i++){
            p2=p2.next;
        }
        while(p2!=null){
            p1=p1.next;
            p2=p2.next;
        }
            p1.next=p1.next.next;
        return dummy.next;
    }
}
```
