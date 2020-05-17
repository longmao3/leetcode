[leetcode455](https://leetcode-cn.com/problems/assign-cookies/submissions/)

* 贪心策略，尽量是需求与供给一致。

```java
class Solution {
    public int findContentChildren(int[] g, int[] s) {
        Arrays.sort(g);
        Arrays.sort(s);
        int count= 0;
        int indexOfG = 0,indexOfS=0;
        while(indexOfG<g.length && indexOfS<s.length){
            if(g[indexOfG] <= s[indexOfS]){
                count++;
                indexOfS++;
                indexOfG++;
            }else{
                indexOfS++;
            }
        }
        return count;
    }
}
```

