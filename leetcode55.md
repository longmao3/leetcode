[leetcode55](https://leetcode-cn.com/problems/jump-game/submissions/)

<img src="C:\Users\Administrator\Desktop\programingNote\leetcode\微信图片_20200110092216.jpg" alt="微信图片_20200110092216" style="zoom:33%;" />

​	

```java
public boolean canJump(int[] nums) {
    int len = nums.length;
    if (len<=1) return true;
    boolean[] canReach = new boolean[nums.length];
    canReach[0]=true;
    for (int i = 1; i < len; i++) {
        for (int j = i-1; j >= 0; j--) {
            if (canReach[j] && nums[j] >= i-j){
                canReach[i] = true;
                break;
            }
        }
    }
    return canReach[len-1];
}
```

