[leetcode341](https://leetcode-cn.com/problems/flatten-nested-list-iterator/)

* 好好学英语。
* 所谓嵌套，是每个NestedInteger表示成一个组件，要么是一个Integer要么是一个List,里面又包含NestedInteger对象，那么只要深度遍历即可。

```java
/**
 * // This is the interface that allows for creating nested lists.
 * // You should not implement it, or speculate about its implementation
 * public interface NestedInteger {
 *
 *     // @return true if this NestedInteger holds a single integer, rather than a nested list.
 *     public boolean isInteger();
 *
 *     // @return the single integer that this NestedInteger holds, if it holds a single integer
 *     // Return null if this NestedInteger holds a nested list
 *     public Integer getInteger();
 *
 *     // @return the nested list that this NestedInteger holds, if it holds a nested list
 *     // Return null if this NestedInteger holds a single integer
 *     public List<NestedInteger> getList();
 * }
 */
public class NestedIterator implements Iterator<Integer> {
    Queue<Integer> queue = new LinkedList<>();

    public NestedIterator(List<NestedInteger> nestedList) {
        for(NestedInteger n : nestedList){
            DFS(n);
        }  
    }

    @Override
    public Integer next() {
        return queue.poll();
        
    }

    @Override
    public boolean hasNext() {
       return queue.size()>0;
    }

    public void DFS(NestedInteger nestedList){
        if(nestedList.isInteger()){
            queue.offer(nestedList.getInteger());
        }
        for(NestedInteger n:nestedList.getList()){
            DFS(n);
        }
    }
}

/**
 * Your NestedIterator object will be instantiated and called as such:
 * NestedIterator i = new NestedIterator(nestedList);
 * while (i.hasNext()) v[f()] = i.next();
 */
```

