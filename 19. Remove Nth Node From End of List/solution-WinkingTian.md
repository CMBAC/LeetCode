
 - 思路：一次遍历（思路来自于网络大佬，推荐解法）
 
 <pre><code>

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
        
        ListNode p=head;      
        ListNode q=head;        
        for(int i=0;i<n;i++){            
            p=p.next;        
        }        
        if(p==null){
            head=head.next;            
            return head;        
        }        
        while(p.next!=null){            
            p=p.next;            
            q=q.next;        
        }        
        q.next=q.next.next;        
        return head;       
    }
}
</code></pre>
