[leetcode649](https://leetcode-cn.com/problems/dota2-senate/)

```java
class Solution {
    public String predictPartyVictory(String senate) {
        Queue<Integer> queue = new LinkedList<>();
        int[] people = {0,0};
        int[] bans = {0,0};
        int temp;
        for(char p : senate.toCharArray()){
            temp = p=='R'?0:1;
            people[temp]++;
            queue.add(temp);
        }
        while(people[0] > 0 && people[1] > 0){
            temp = queue.poll();
            if(bans[temp] > 0){
                people[temp]--;
                bans[temp]--;
            }else{
                bans[temp^1]++;
                queue.add(temp);
            }
        }
        return people[0]>0?"Radiant":"Dire";
    }
}
```

