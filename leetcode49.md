[leetcode49](https://leetcode-cn.com/problems/group-anagrams/submissions/)

​	

```java
public List<List<String>> groupAnagrams(String[] strs) {
    List<List<String>> ans = new ArrayList<>();
    if (strs.length == 0) return ans;
    Map<String,List<String>> map = new HashMap<>();
    for (int i = 0; i < strs.length; i++) {
        char[] chars = strs[i].toCharArray();
        Arrays.sort(chars);
        String s = new String(chars);
        if (map.containsKey(s)){
            map.get(s).add(strs[i]);
        }else {
            List<String> list = new ArrayList<>();
            list.add(strs[i]);
            map.put(s,list);
        }
    }
    for (Map.Entry<String, List<String>> stringListEntry : map.entrySet()) {
        ans.add(stringListEntry.getValue());
    }
    return ans;
}
```

