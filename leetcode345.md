​	[leetcode345](https://leetcode-cn.com/problems/reverse-vowels-of-a-string/)

```java
public String reverseVowels(String s) {
    char[] chars = s.toCharArray();
    int start=0,end=s.length()-1;
    Set<Character> set = new HashSet<>();
    set.add('a');
    set.add('e');
    set.add('i');
    set.add('o');
    set.add('u');
    set.add('A');
    set.add('E');
    set.add('I');
    set.add('O');
    set.add('U');
    while (start < end){
        while (start<end &&  !set.contains(chars[start])) start++;
        while (start<end && !set.contains(chars[end]))    end--;
        char temp=chars[start];
        chars[start]=chars[end];
        chars[end]=temp;
        start++;
        end--;
    }
    return new String(chars);
}
```

