[leetcode155](https://leetcode-cn.com/problems/min-stack/)

* 写代码建立规则，所有地方按照规则行事。

```java
class MinStack {

    List<Integer> stack = new ArrayList<>();
    int min = Integer.MAX_VALUE;
    int indexOfMin = -1;
    public MinStack() {

    }
    
    public void push(int x) {
       stack.add(x);
       if(stack.size() == 1){
           min = x;
           indexOfMin = 0;
       }else if(indexOfMin>=0 && x < min){
           min = x;
           indexOfMin=stack.size()-1;
       }
    }
    
    public void pop() {
        stack.remove(stack.size()-1);
        if(stack.size() == 1){
           min = stack.get(0);
           indexOfMin = 0;
       }else if(stack.size() == 0 || stack.size() == indexOfMin ){
           min = Integer.MAX_VALUE;
           indexOfMin = -1;
       }
    }
    
    public int top() {
        return stack.get(stack.size()-1);
    }
    
    public int getMin() {
        if(indexOfMin >= 0) return this.min;
    
        for(int i=0;i<stack.size();i++){
            int x = stack.get(i);
            if(x<min){
                min=x;
                indexOfMin = i;
            }
        }
        return this.min;
    }
}

```

