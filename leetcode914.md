[leetcode914](https://leetcode-cn.com/problems/x-of-a-kind-in-a-deck-of-cards/)

```java
class Solution {
    public boolean hasGroupsSizeX(int[] deck) {
        if(deck.length < 2) return false;
        List<Integer> map = new ArrayList<Integer>();
        Arrays.sort(deck);
        int count = 1,maxCommonDivisor;
        for(int i=1;i< deck.length;i++){
            if(deck[i] == deck[i-1]){
                count++;
            }else{
                if(count == 1) return false;
                map.add(count);
                count=1;
            }
        }
        map.add(count);
        if(map.size() == 1) return true;
        maxCommonDivisor = maxCommonDivisor(map.get(0),map.get(1));
        for(int i=2;i<map.size();i++){
            maxCommonDivisor=maxCommonDivisor(maxCommonDivisor,map.get(i));
            if(maxCommonDivisor == 1) break;
        }   
        return maxCommonDivisor>1;
    }
    public int maxCommonDivisor(int x,int y){
         int max = Math.max(x,y);
         int min = Math.min(x,y);
         int tmp;
         while( x % y !=0){
            tmp = x%y;
            x=y;
            y=tmp;
         }
         return y;
    }
}
```

改进：

```java
class Solution {
    public boolean hasGroupsSizeX(int[] deck) {
        if(deck.length < 2) return false;
        int[] count = new int[10000]; //由于给定的数字大小不太大，可以这样使用。
        for(int i=0;i< deck.length;i++){
            count[deck[i]]++;
        }

        int  g = -1;
        for(int c : count){
            if(c == 0) continue;
            g=g>0? gcd(g,c):c;
            if(g == 1) break;
        }   
        return g>1;
    }
    public int gcd(int x,int y){    //最大公约数的简洁写法，假设x>y,否则会在第一次递归时将两个数字                                      //进行交换。
        if(y == 0){
            return x;
        }
         return gcd(y,x%y);
    }
}
```

