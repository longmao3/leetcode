[leetcode93](https://leetcode-cn.com/problems/restore-ip-addresses/)
解题思路
回溯法，但是没有使用共同的资源，又不像是回溯法。
回溯与递归的区别是？回溯是一种思想，递归更重要的是一种形式。

代码
```java
class Solution {
 	  public List<String> restoreIpAddresses(String s) {
        int n = s.length();
        List<String> ans = new ArrayList<>();
        backtrack(s,4,"",n,0,ans);
        return ans;
    }

    public void backtrack(String s,int flag,String temp,int n,int start,List<String> ans)		{
        if (flag == 0 && start == n){
            temp=temp.substring(0,temp.length()-1);
            ans.add(temp);
            return;
        }else if (flag <= 0 || start>=n) return;
        for (int i = start; i < start+3; i++) {
            if (i==start && s.charAt(i) == '0'){   //若是0,则必须是 ···.0.···的形式
                backtrack(s,flag-1,temp+s.charAt(i)+'.',n,i+1,ans);
                break;
            }
            if (i<n && Integer.parseInt(s.substring(start,i+1))<=255) {
                backtrack(s, flag - 1, temp + s.substring(start,i+1) + '.', n, i + 1, ans);
            }
        }
    }
}
```

