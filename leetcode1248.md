[leetcode1248](https://leetcode-cn.com/problems/count-number-of-nice-subarrays/)

[参考](https://leetcode-cn.com/problems/count-number-of-nice-subarrays/solution/java-hua-dong-chuang-kou-xiang-jie-zhi-xing-yong-s/)

```java
class Solution {
    public int numberOfSubarrays(int[] nums, int k) {
        int[] arr = new int[nums.length+2];
        int feed = 0,res=0;
        for(int i=0;i<nums.length;i++){
            if((nums[i] & 1)==1){
                arr[++feed] = i;
            }
        }
        arr[0]=-1;
        arr[feed+1]=nums.length;
        for(int i=1;i<=feed-k+1;i++){
            res+=(arr[i]-arr[i-1])*(arr[i+k]-arr[i+k-1]);
        }
        return res;

    }
}
```

