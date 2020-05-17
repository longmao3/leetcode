[leetcode349](https://leetcode-cn.com/problems/intersection-of-two-arrays/)

```java
class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        List<Integer> list = new ArrayList<>();
        Arrays.sort(nums1);
        Arrays.sort(nums2);
        int i=0,j=0;
       while(i<nums1.length && j<nums2.length){
           while(i<nums1.length-1 && nums1[i] == nums1[i+1]){
               i++;
           }
            if(nums1[i] == nums2[j] ){
                list.add(nums1[i]);
                i++;
                j++;  //注意细节
            }else if(nums1[i] < nums2[j]){
                i++;
            }else{
                j++;
            }
        }
        int[] res = new int[list.size()];
        for(i=0;i<res.length;i++){
            res[i]=list.get(i);
        }
        return res;

    }
}
```

