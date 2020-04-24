leetcode面试题[51](https://leetcode-cn.com/problems/shu-zu-zhong-de-ni-xu-dui-lcof/)

* 此题可以看做暴力求解的优化

```java
class Solution {

    public int reversePairs(int[] nums) {
        if(nums.length == 0) return 0;
        int[] temp = new int[nums.length];
        return helper(nums,temp,0,nums.length);
    }
    public int  helper(int[] nums,int[] temp,int start,int end){
        //划分数组里面只有一个数字
        int revP = 0;
        if(start+1==end){
            return revP;
        }
        int mid = start+(end-start)/2;
        revP+=helper(nums,temp,start,mid);
        revP+=helper(nums,temp,mid,end);
        int i=start,j=mid,k=start,tempRevP=0;
        while(i<mid || j<end){
            //如果i==mid 直接进入后面的复制语句。
            if( i!=mid && (j==end || nums[i]<=nums[j]) ){  //如果相等，那么应该是前面那个先
                temp[k++]=nums[i++];
                revP+=(j-mid);   // 前面的数组里面的数被放置，发现逆序。
            }else{
                temp[k++]=nums[j++];
            }
        }
        System.arraycopy(temp,start,nums,start,end-start);
        return revP;
    }
}
```

