[leetcode34](https://leetcode-cn.com/problems/find-first-and-last-position-of-element-in-sorted-array/submissions/)

```java
public int[] searchRange(int[] nums, int target) {
    int[] ans={-1,-1};
    int start = binarySearch(nums, target - 0.5f);
    int end = binarySearch(nums, target + 0.5f);
    if (start == end)
        return ans;
    else {
        ans[0]=start;
        ans[1]=end-1;
    }
    return ans;
}

public static int binarySearch(int[] nums, float target){
    int start=0,end=nums.length-1;
    while (start <= end){
        int mid=start+(end-start)/2;
        if (nums[mid] == target) return mid;
        if (nums[mid]>target)
            end=mid-1;
        else
            start=mid+1;
    }
    return  start; //如果找不到，返回刚好大于这个数的，
}
```



* 二分法
  * 要么提前结束
  * 要么最后会start+1=end， 从此入手分析。

```java
public int[] searchRange(int[] nums, int target) {
    int[] ans={-1,-1};
    if (nums == null || nums.length == 0) return ans;
    int left = binarySearchLeft(nums, target );
    int right = binarySearchRight(nums, target);
    if (right < left)
        return ans;
    else {
        ans[0]=left;
        ans[1]=right;
    }
    return ans;
}

public static int binarySearchLeft(int[] nums, int target){
    int start=0,end=nums.length-1;
    while (start <=  end){
        int mid=start+(end-start)/2;
        if (nums[mid] >= target)
            end=mid-1; //将大于等于目标的排除在右侧
        else
            start=mid+1;
    }
    return  end+1; 
}

public static int binarySearchRight(int[] nums, int target){
    int start=0,end=nums.length-1;
    while (start <=  end){
        int mid=start+(end-start)/2;
        if (nums[mid] <= target)
            start=mid+1; //将小于等于的排除在左侧
        else
            end=mid-1;
    }
    return  start-1; 
}
```