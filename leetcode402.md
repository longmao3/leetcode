[leetcode402](https://leetcode-cn.com/problems/remove-k-digits/)

* 维护一个单调递增的栈，若是后面的数字大于栈顶则入栈，小于栈顶元素则出栈，保持单调性。

```java
class Solution {
    public String removeKdigits(String num, int k) {
        int index=0;
        Stack<Character> s = new Stack<>();
        while(k>0 && index<num.length()){
            Character c  = num.charAt(index++);
            while(!s.empty() && s.peek()>c && k>0){
                s.pop();
                k--;
            }
            if(c != '0' || s.size()>=1) { // 前导零不用入栈，也不用被删除，节省一次删除的机会。
                 s.push(c);
            }
        }
        while(k>0 && !s.empty()){  //防止出现类似于从前到后数字是单调递增（所有数字入栈，则删除掉后                                     //面的即可）的情况
            s.pop();
            k--;
        }
        StringBuilder builder = new StringBuilder();
        while(!s.empty()){
            builder.append(s.pop());
        }
        builder=builder.reverse();
        builder.append(num.substring(index));
        return builder.toString().equals("")?"0":builder.toString();
    }
}
```

