[leetcode8](https://leetcode-cn.com/problems/string-to-integer-atoi/)

* 尽量使用类库Character.isDigit();
* 可以使用自动机，状态装换，减少判断。??

```java
class Solution {
    public int myAtoi(String str) {
        long ans = 0;
        int sign = 1;
        str = str.trim();
        if(str.length()==0){
            return 0;
        }
        char c = str.charAt(0);
        if(c=='-'){
          sign=-1;   
        }else if(c=='+'){
        }else if(c>='0' && c<='9'){
            ans=c-'0';
        }else{
            return 0;
        }
        for(int i = 1;i<str.length();i++){
            c=str.charAt(i);
            if(c>='0' && c<='9'){
                ans=ans*10+(c-'0')*sign;
                if(ans>Integer.MAX_VALUE){
                    return Integer.MAX_VALUE;
                }else if(ans<Integer.MIN_VALUE){
                    return Integer.MIN_VALUE;
                }
            }else{
                break;
            }
        }
        return (int)ans;
    }
}
```

