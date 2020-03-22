[leetcode142](https://leetcode-cn.com/problems/linked-list-cycle-ii/)

* 链表总数为a+b，a为不是环的节点总数，b是环内的节点总数。
* 记快慢指针相遇时，快指针走的步数为`f=2s,f=s+nb`则`s=nb`
* 而且只要一个指针走过`nb+a`步，一定会在入口处，那么只要让慢指针再走`a`步即可。
* 我们不知道a是多少，但是从`head`走到入口处是a步，所以重设一个指针，从head开始，与慢指针一起每次走一步，最终会在入口处相遇。

```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode detectCycle(ListNode head) {
        if( head == null) return head;
        ListNode fast = head,slow = head;
        while(fast.next != null && fast.next.next != null){
            slow = slow.next;
            fast = fast.next.next;
            if(slow == fast){
                fast = head;
                while(fast != slow){
                    fast = fast.next;
                    slow = slow.next;
                }
                return slow;
            }
        }
        return null;
        
    }
}
```

