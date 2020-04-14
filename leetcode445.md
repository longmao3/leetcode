[leetcode445](https://leetcode-cn.com/problems/add-two-numbers-ii/)

* 使用三目运算，减少代码长度。
* 链表也可以从前向后生长。

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
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        Stack<Integer> stack_1 = new Stack<>();
        Stack<Integer> stack_2 = new Stack<>();
        while(l1 != null){
            stack_1.push(l1.val);
            l1=l1.next;
        }
         while(l2 != null){
            stack_2.push(l2.val);
            l2=l2.next;
        }
        ListNode head = null;
        //ListNode cur = head;
        int carry = 0;
        // while(!stack_1.empty() && !stack_2.empty()){
        //     int oprand_1 = stack_1.poll();
        //     int oprand_2 = stack_2.poll();
        //     int sum = oprand_1+oprand_2+tmp;
        //     cur.next = new ListNode(sum%10);
        //     tmp = sum/10;
        //     cur=cur.next;
        // }
        //int sum = carry;
        while(!stack_1.isEmpty() || !stack_2.isEmpty() || carry>0){
            int sum=carry;
            sum+=stack_1.isEmpty()?0:stack_1.pop();
            sum+=stack_2.isEmpty()?0:stack_2.pop();
            ListNode node  = new ListNode(sum%10);
            node.next = head;
            head=node;
            carry=sum/10;
        }
        return head;
    }
}
```

