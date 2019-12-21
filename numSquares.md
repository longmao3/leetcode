

![](C:\Users\Administrator\Desktop\programingNote\力扣做题总结\2.PNG)

[参考](https://leetcode-cn.com/problems/perfect-squares/solution/bu-zhi-shi-da-an-er-shi-dong-tai-gui-hua-lei-ti-de/)

* 动态规划是递归进行剪枝（或者说保存子问题结果）的解题方式。

* 动态规划思考方式是自顶向下，写代码是自底向上。

  ​	

```java
public static int numSquares(int n) {
    int[] dp = new int[n+1];
    for (int i = 0; i < n + 1; i++) {
        dp[i]=i;
        for (int j = 1; i-j*j >= 0; j++) {
            dp[i]=Math.min(dp[i],dp[i-j*j]+1);
        }
    }
    return dp[n];
}
```

