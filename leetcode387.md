​	[leetcode387](https://leetcode-cn.com/problems/first-unique-character-in-a-string/submissions/)

```java
public int firstUniqChar_1(String s) {
    Map<Character,Integer> map=new HashMap();
    for (int i = 0; i < s.length(); i++) {
        map.put(s.charAt(i),map.getOrDefault(s.charAt(i),0)+1);
    }
    for (int i = 0; i < s.length(); i++) {
        if (map.get(s.charAt(i)) == 1)
            return i;
    }
    return -1;
}

public int firstUniqChar(String s) {
    if (s.trim().length() == 0) return -1;
   int[] count=new int[26];
   char[] chars=s.toCharArray();
    for (int i = 0; i < s.length(); i++) {
        count[chars[i]-'a']++;
    }
    for (int i = 0; i < s.length(); i++) {
        if (count[chars[i]-'a'] ==  1)
            return i;
    }
    return -1;
}
```