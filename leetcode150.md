[leetcode150](https://leetcode-cn.com/problems/evaluate-reverse-polish-notation/)

```JAVA
class Solution {
    public int evalRPN(String[] tokens) {
        Stack<Integer> stack = new Stack<>();
        int operand_1,operand_2;
        for(String token : tokens){
            try{
                int operand = Integer.valueOf(token);
                stack.push(operand);
            }catch(Exception e){
                 operand_1=stack.pop();
                operand_2=stack.pop();
                switch(token.charAt(0)){
                    case '+':
                        stack.push(operand_1+operand_2);
                        break;
                    case '-':
                        stack.push(operand_2-operand_1);
                        break;
                     case '*':
                        stack.push(operand_1*operand_2);
                        break;
                     case '/':
                        stack.push(operand_2/operand_1);
                        break;
                }
            }
            
        }
        return stack.pop();
    }
}
```

上面一种方法使用到了异常处理，超级慢。

第二种方法

```java
class Solution {
    public int evalRPN(String[] tokens) {
        Set<String> set = new HashSet<>();
        set.add("+");
        set.add("-");
        set.add("*");
        set.add("/");
        Stack<Integer> stack = new Stack<>(); 
        int operand_1,operand_2;
        for(String token : tokens){
            if(!set.contains(token)){
                stack.push(Integer.valueOf(token));
            }else{
                operand_1 = stack.pop();
                operand_2 = stack.pop();
                switch(token.charAt(0)){
                    case '+':
                         stack.push(operand_1+operand_2);
                        break;
                    case '-':
                        stack.push(operand_2-operand_1);
                        break;
                     case '*':
                        stack.push(operand_1*operand_2);
                        break;
                     case '/':
                        stack.push(operand_2/operand_1);
                        break;
                }
            }
            
        }
        return stack.pop();
    }
}
```



