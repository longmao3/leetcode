[leetcode62](https://leetcode-cn.com/problems/yuan-quan-zhong-zui-hou-sheng-xia-de-shu-zi-lcof/)

[参考](https://leetcode-cn.com/problems/yuan-quan-zhong-zui-hou-sheng-xia-de-shu-zi-lcof/solution/yuan-quan-zhong-zui-hou-sheng-xia-de-shu-zi-by-lee/)

* DP需要从底向上和向下两方面进行思考问题。
* 编程不要拘泥于形似，不要拘泥于形式。

```java
class Solution {
    public int lastRemaining(int n, int m) {
        int firstDeleted=0;
        if(n == 1) return 0;
        else {
            firstDeleted=m%n;
            return (firstDeleted+lastRemaining(n-1,m))%n;
        }
    }
}
```

迭代解法

```java
class Solution {
    public int lastRemaining(int n, int m) {
       int p = 0;
       if(n==1) return p;
       for(int i=2;i<=n;i++){
           p=(p+m)%i;  //每次迭代的数组里面的总数是不同的。
       }
       return p;
    }
}
```

