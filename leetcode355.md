[leetcode355](https://leetcode-cn.com/problems/design-twitter/)

```java
class Twitter {
    Map<Integer,Set<Integer>>  followings;
    Map<Integer,Tweet>  tweets;
    PriorityQueue<Tweet> maxHeap;
    int localTimeStamp;

    /** Initialize your data structure here. */
    public Twitter() {
        followings  = new HashMap<>();
        tweets = new HashMap<>();
        maxHeap = new PriorityQueue<>((o1,o2)->o2.timeStamp-o1.timeStamp);
    }
    
    /** Compose a new tweet. */
    public void postTweet(int userId, int tweetId) {
        if(tweets.containsKey(userId)){
          Tweet oldHead = tweets.get(userId);
          Tweet newHead = new Tweet(tweetId,userId,localTimeStamp++);
          tweets.put(userId,newHead);
          newHead.next = oldHead;
        }else{
            Tweet head = new Tweet(tweetId,userId,localTimeStamp++);
            tweets.put(userId,head);
        }

    }
    
    /** Retrieve the 10 most recent tweet ids in the user's news feed. Each item in the news feed must be posted by users who the user followed or by the user herself. Tweets must be ordered from most recent to least recent. */
    public List<Integer> getNewsFeed(int userId) {
        List<Integer> res = new ArrayList<>(10);
        maxHeap.clear();
        if(tweets.containsKey(userId)){
            maxHeap.offer(tweets.get(userId));
        }
        if(followings.containsKey(userId)){
            Set<Integer> followingList = followings.get(userId);
            for(Integer followee : followingList){
                if(tweets.containsKey(followee)){
                     Tweet head = tweets.get(followee);
                     maxHeap.offer(head);
                }  
            }
        }
        while(!maxHeap.isEmpty() && res.size()<10){
            Tweet head = maxHeap.poll();
            res.add(head.id);
            if(head.next != null){
                maxHeap.offer(head.next);
            }
        }
        return res;

    }
    
    /** Follower follows a followee. If the operation is invalid, it should be a no-op. */
    public void follow(int followerId, int followeeId) {
        if(followeeId == followerId){
            return;
        }
        if(followings.containsKey(followerId)){
            Set<Integer> followingList = followings.get(followerId);
            followingList.add(followeeId);
        }else{
            Set<Integer> followingList = new HashSet<>();
            followingList.add(followeeId);
            followings.put(followerId,followingList);
        }
    }
    
    /** Follower unfollows a followee. If the operation is invalid, it should be a no-op. */
    public void unfollow(int followerId, int followeeId) {
         if(followeeId == followerId){
            return;
        }
        if(followings.containsKey(followerId)){
            Set<Integer> followingList = followings.get(followerId);
            followingList.remove(followeeId);
        }else{
            return;
        }

    }

    public class Tweet{
        int id;
        int timeStamp;
        int userId;
        Tweet next;
        Tweet(int id,int userId,int timeStamp){
            this.id = id;
            this.timeStamp = timeStamp;
            this.userId = userId;
        }
    }
}

/**
 * Your Twitter object will be instantiated and called as such:
 * Twitter obj = new Twitter();
 * obj.postTweet(userId,tweetId);
 * List<Integer> param_2 = obj.getNewsFeed(userId);
 * obj.follow(followerId,followeeId);
 * obj.unfollow(followerId,followeeId);
 */
```

