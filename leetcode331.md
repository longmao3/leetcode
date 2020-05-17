[leetcode331](https://leetcode-cn.com/problems/verify-preorder-serialization-of-a-binary-tree/)

```java
class Solution {
    public boolean isValidSerialization(String preorder) {
        String[] token = preorder.split(",");
        int slot = 1;
        for(String s : token){
            slot--;  //先使用slot
            if(slot<0) return false;
            if(!s.equals("#")){
               slot+=2;
            }
            
        }
        return slot==0;
    }
}
```

