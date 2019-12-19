![](C:\Users\Administrator\Desktop\programingNote\力扣做题总结\捕获.PNG)

## 动态规划

* 动态规划的关键是找到最优子结构，找到递推关系，这样可以避免重复计算；

* 有些问题直接就可以DP [word-break](https://leetcode-cn.com/problems/word-break/)

* 但是有些问题需要进行转化才能使用DP [本题](https://leetcode-cn.com/problems/maximum-product-subarray/);

### 本题解法

问题转化为：以某下标结束的最大乘积子序列积，记为`f(n)`

* 则`f(n)=max{f(n-1)*nums[n],nums[n]}`

* 但是有负数，所以还要记录当前最小值`f_min`​	

  ```java
  public static int maxProduct_1(int[] nums) {
      int ans=nums[0];
      int cur_max=nums[0];
      int cur_min=nums[0];
      for (int i = 1; i < nums.length; i++) {
          if (nums[i]>=0) {
              cur_max = Math.max(cur_max*nums[i],nums[i]);
              cur_min = Math.min(cur_min*nums[i],nums[i]);
          }else {
              int temp=cur_max;
              cur_max = Math.max(cur_min*nums[i],nums[i]);
              cur_min = Math.min(temp*nums[i],nums[i]);
          }
          ans=Math.max(cur_max,ans);
      }
      return ans;
  }
  ```

或者也可以从后往前遍历，这是就是以某下标**开始**积记为`f(n)`

```java
public static int maxProduct(int[] nums) {
    int ans=nums[nums.length-1];
    int cur_max=nums[nums.length-1];
    int cur_min=nums[nums.length-1];
    for (int i = nums.length-2; i>=0; i--) {
        if (nums[i]<0){
            int temp = cur_max;
            cur_max=cur_min;
            cur_min=temp;
        }
        cur_max = Math.max(cur_max*nums[i],nums[i]);
        cur_min = Math.min(cur_min*nums[i],nums[i]);
        ans=Math.max(ans,cur_max);
    }
    return ans;
}
```