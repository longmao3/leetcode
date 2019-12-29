[leetcode344](https://leetcode-cn.com/problems/reverse-string/submissions/)

```java
public void reverseString(char[] s) {
    int start=0;
    int end=s.length-1;
    char temp=0;
   while (start<end){
       if (s[start] != s[end]){
           temp=s[start];
           s[start]=s[end];
           s[end]=temp;
       }
       start++;
       end--;
   }
}
```

