[leetcode151](https://leetcode-cn.com/problems/reverse-words-in-a-string/)



```java
public String reverseWords(String s) {
    String[] split = s.split(" ");
    StringBuilder builder = new StringBuilder();
    for (int i = split.length-1; i >=0 ; i--) {
        if (split[i].equals("")) continue;
        if (i == split.length-1) builder.append(split[i]);
        else builder.append(" "+split[i]);
    }
    return builder.toString();
}
```