[leetcode 300](https://leetcode-cn.com/problems/longest-increasing-subsequence/submissions/)

解法一：动态规划

* dp[i]存放以nums[i]结尾的LIS子串长度；

*  若是nums[i+1]大于nums[k]则dp[i+1]可以更新为dp[k]+1;

  ```java
  //效率有点低
  public int lengthOfLIS_1(int[] nums) {
      if (nums.length == 0) return 0;
      int[] LIS = new int[nums.length];
      int ans=1;
      Arrays.fill(LIS,1);
      for (int i = 1; i < nums.length; i++){
          for (int j = i-1; j >= 0; j--) {
              if (nums[j]<nums[i]) {
                  LIS[i] = Math.max(LIS[i], LIS[j]+1);
              }
          }
          ans = Math.max(ans,LIS[i]);
      }
      return ans;
  }
  ```

解法二：[参考](https://leetcode-cn.com/problems/longest-increasing-subsequence/solution/zui-chang-shang-sheng-zi-xu-lie-dong-tai-gui-hua-2/)

* dp[i]存放长度为i+1的升序子串的最小的结尾值。

  ​	

  ```java
  //漂亮
  public static int lengthOfLIS(int[] nums) {
     int[] dp = new int[nums.length];
     int len=0;
      for (int i = 0; i < nums.length; i++) {
          int minimalTail = Arrays.binarySearch(dp, 0, len, nums[i]);
          if (minimalTail < 0) { //没有查找到；
              minimalTail=-(minimalTail+1);
              dp[minimalTail] = nums[i];
              if (minimalTail == len) len++;
          }
      }
      return len;
  }
  ```


