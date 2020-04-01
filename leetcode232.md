[leetcode232](https://leetcode-cn.com/problems/implement-queue-using-stacks/)

一个栈专门用于入队，一个专门负责出队，出队处空了时，将用于入队的队列倒腾过来。

```java
class MyQueue {
    Stack<Integer> spush = new Stack<>();
     Stack<Integer> spop = new Stack<>();

    /** Initialize your data structure here. */
    public MyQueue() {

    }
    
    /** Push element x to the back of queue. */
    public void push(int x) {
        
        spush.push(x);
    }
    
    /** Removes the element from in front of queue and returns that element. */
    public int pop() {
        shift();
        return spop.pop();
    }

    public void shift(){  //需要的时候再进行倒腾。
         if(spop.size() == 0){
             while(spush.size() > 0){
                 spop.push(spush.pop());
            }
        }

    }
    
    /** Get the front element. */
    public int peek() {
        shift();
       return  spop.peek();

    }
    
    /** Returns whether the queue is empty. */
    public boolean empty() {
        return (spop.isEmpty() && spush.isEmpty());
    }
}

/**
 * Your MyQueue object will be instantiated and called as such:
 * MyQueue obj = new MyQueue();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.peek();
 * boolean param_4 = obj.empty();
 */
```

