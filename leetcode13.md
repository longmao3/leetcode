[leetcode13](https://leetcode-cn.com/problems/roman-to-integer/submissions/)

```java
public int romanToInt(String s) {
    Map<String,Integer> map = new HashMap<>();
    map.put("I",1);
    map.put("IV",4);
    map.put("V",5);
    map.put("IX",9);

    map.put("X",10);
    map.put("XL",40);
    map.put("L",50);
    map.put("XC",90);

    map.put("C",100);
    map.put("CD",400);
    map.put("D",500);

    map.put("CM",900);
    map.put("M",1000);

    int index=0;
    int ans=0;
    while (index < s.length()){
        if (index+1<s.length() && map.containsKey(s.substring(index,index+2))){
            ans+=map.get(s.substring(index,index+2));
            index+=2;
        }else {
            ans+=map.get(s.substring(index,index+1));
            index+=1;
        }
    }
    return ans;
}
```