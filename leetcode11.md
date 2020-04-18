[leetcode11](https://leetcode-cn.com/problems/container-with-most-water/)

* 使用++、--运算符号要小心。

```java
class Solution {
    public int maxArea(int[] height) {
        int start = 0;
        int end = height.length-1;
        int maxWater = 0;
        while(start<end){
            if(height[start]<height[end]){
                maxWater=Math.max(maxWater,height[start]*(end-start));
                start++;
            }else{
                maxWater=Math.max(maxWater,height[end]*(end-start));
                end--;
            }
        }
        return maxWater;
    }

}
```

