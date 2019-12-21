



![](C:\Users\Administrator\Desktop\programingNote\力扣做题总结\1.PNG)

思路借鉴[力扣unique-paths](https://leetcode-cn.com/problems/unique-paths/)

### 解法一

​	

```
//不优雅
public int maximalSquare_1(char[][] matrix) {
    if (matrix.length == 0) return 0;
    int[][] dp=new int[matrix.length][matrix[0].length];
    for (int i = 0; i < matrix[0].length; i++) {
        if (matrix[0][i] == '1') dp[0][i] = 1;
    }
    for (int i = 1; i < matrix.length; i++) {
        if (matrix[i][0] == '1') dp[i][0]=1;
        for (int j = 1; j < matrix[0].length; j++) {
            if (matrix[i][j] == '1') dp[i][j]=1;
            else continue;
            for (int k = 1; k < dp[i-1][j-1]+1; k++) {
                if (matrix[i-k][j] == '1' && matrix[i][j-k]=='1')
                    dp[i][j]++;
                else break;
            }
        }
    }
    int max=0;
    for (int i = 0; i < dp.length; i++) {
        for (int j = 0; j < dp[0].length; j++) {
            if (dp[i][j] > max) max=dp[i][j];
        }
    }
    return max*max;
}
```

没有充分利用已知信息，起始条件的设置也不优雅

* 其实`dp[i][j]=1+min{dp[i-1][j-1],dp[i-1][j],dp[i][j-1]`

  ​	

  ```
  public int maximalSquare(char[][] matrix) {
      int m=matrix.length;
      if (m<1) return 0;
      int n=matrix[0].length;
      int[][] dp = new  int[m+1][n+1];
      int max=0;
      for (int i = 1; i < m+1; i++) {
          for (int j = 1; j < n+1; j++) {
              if (matrix[i-1][j-1] == '1') {
                  dp[i][j] = 1 + Math.min(dp[i - 1][j - 1], Math.min(dp[i - 1][j], dp[i][j - 1]));
                  max=Math.max(dp[i][j],max);
              }
          }
      }
      return max*max;
  }
  ```