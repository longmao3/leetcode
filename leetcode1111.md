[leetcode1111](https://leetcode-cn.com/problems/maximum-nesting-depth-of-two-valid-parentheses-strings/)

```java
class Solution {
    public int[] maxDepthAfterSplit(String seq) {
        int[] ans = new int[seq.length()];
        int d = 0;
        char[] chars = seq.toCharArray();
        for(int i=0;i<chars.length;i++){
            if(chars[i] == '('){
                d+=1;
                ans[i]=d%2;
            }else if( chars[i] == ')'){
                ans[i]=d%2;
                d--;
            }
        }
        return ans;
    }
}
```

