[leetcode287](https://leetcode-cn.com/problems/find-the-duplicate-number/)

关注题目的条件，二分法查找。[参考](https://leetcode-cn.com/problems/find-the-duplicate-number/solution/er-fen-fa-si-lu-ji-dai-ma-python-by-liweiwei1419/)

```java
class Solution {
    public int findDuplicate(int[] nums) {
        int end = nums.length-1,start=1,mid;
        while(start < end){
            mid = start+(end-start)/2;
            int count = 0;
            for(int i=0;i<nums.length;i++ ){
                 if(nums[i] >=start && nums[i] <= mid){
                         count++;
                    }
             }
            if(count>mid-start+1){
                end=mid;
            }else{
                start=mid+1;
            }
        }
        return start;
    }
    public int count(int[] nums,int lo,int hi){
        int count = 0;
        for(int i=0;i<nums.length;i++ ){
            if(nums[i] >=lo && nums[i] <= hi){
                count++;
            }
        }
        return count;
    }
}
```

