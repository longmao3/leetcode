[leetcode283](https://leetcode-cn.com/problems/move-zeroes/)

差点被这小东西难住，这种小题不用想得太复杂。

```java
class Solution {
    public void moveZeroes(int[] nums) {
        int step = 0;
        for(int i=0;i<nums.length;i++){
            if(nums[i]==0){
                step++;
            }else{
                nums[i-step]=nums[i];
            }
        }
        for(int i=nums.length-1;step>0;i--,step--){
            nums[i]=0;
        }

    }
}
```

