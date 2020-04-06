[leetcode72](https://leetcode-cn.com/problems/edit-distance/)

使用动态规划

使用`dp[i][j]`表示，字符一前`i`个转换成字符二前`j`个需要的最小转换次数。

* 若`word1[i]`==`word2[j]`那么，`dp[i][j]=dp[i-1][j-1]`

* 否则取增删改的最小操作数：`dp[i][j]=min(dp[i][j-1],dp[i-1][j],dp[i-1][j-1])+1 `
  * `dp[i][j-1] `   :字符一前`i`个已经能转化成字符二前`j-1`个，这时在字符一上增加`word2[j]`即可。
  * `dp[i-1][j]`:字符一前`i-1`个已经能转换成字符二前`j`个，删除字符一`word1[i]``
  * `dp[i-1][j-1]`:将`word1[i]`替换为`word2[j]`                                                                                                                                                                                                                                           

```java
class Solution {
    public int minDistance(String word1, String word2) {
        int len_1 = word1.length(),len_2 = word2.length();
        int[][] dp = new int[len_1+1][len_2+1];
        for(int i=0;i<=len_1;i++){
            dp[i][0]=i;
        }
        for(int i=0;i<=len_2;i++){
            dp[0][i] = i;
        }
        for(int row = 1;row<=len_1;row++){
            for(int col = 1;col<=len_2;col++){
                if(word1.charAt(row-1) == word2.charAt(col-1)){
                    dp[row][col] = dp[row-1][col-1];
                }else{
                    dp[row][col] =Math.min( Math.min(dp[row][col-1],dp[row-1][col]),dp[row-1][col-1])+1;
                }
            }
        }
        return dp[len_1][len_2];
    }
}
```

