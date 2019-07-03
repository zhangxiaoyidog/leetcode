## 355.Design Twitter

## 题目描述

设计一个简化版的推特(Twitter)，可以让用户实现发送推文，关注/取消关注其他用户，能够看见关注人（包括自己）的最近十条推文。你的设计需要支持以下的几个功能：

1. postTweet(userId, tweetId): 创建一条新的推文
2. getNewsFeed(userId): 检索最近的十条推文。每个推文都必须是由此用户关注的人或者是用户自己发出的。推文必须按照时间顺序由最近的开始排序。
3. follow(followerId, followeeId): 关注一个用户
4. unfollow(followerId, followeeId): 取消关注一个用户

**示例:**

```
Twitter twitter = new Twitter();

// 用户1发送了一条新推文 (用户id = 1, 推文id = 5).
twitter.postTweet(1, 5);

// 用户1的获取推文应当返回一个列表，其中包含一个id为5的推文.
twitter.getNewsFeed(1);

// 用户1关注了用户2.
twitter.follow(1, 2);

// 用户2发送了一个新推文 (推文id = 6).
twitter.postTweet(2, 6);

// 用户1的获取推文应当返回一个列表，其中包含两个推文，id分别为 -> [6, 5].
// 推文id6应当在推文id5之前，因为它是在5之后发送的.
twitter.getNewsFeed(1);

// 用户1取消关注了用户2.
twitter.unfollow(1, 2);

// 用户1的获取推文应当返回一个列表，其中包含一个id为5的推文.
// 因为用户1已经不再关注用户2.
twitter.getNewsFeed(1);
```



```python
class Twitter:
    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.post = {}
        self.follows = {}
        self.time_post = 0

    def postTweet(self, userId: int, tweetId: int) -> None:
        """
        Compose a new tweet.
        """
        if userId not in self.post:
            self.post[userId] = []
            self.post[userId].append((self.time_post, tweetId))
        else:
            self.post[userId].append((self.time_post, tweetId))
        self.time_post += 1

    def getNewsFeed(self, userId: int) -> 'List[int]':
        """
        Retrieve the 10 most recent tweet ids in the user's news feed. Each item in the news feed must be posted by users who the user followed or by the user herself. Tweets must be ordered from most recent to least recent.
        """

        all_post = []
        if userId in self.post:
            all_post += self.post[userId]
        if userId in self.follows:
            for usr in self.follows[userId]:
                if usr in self.post:
                    all_post += self.post[usr]
        res = []

        if all_post:
            all_post.sort(key=lambda a: a[0], reverse=True)
            res = [a[1] for a in all_post] 
        return res[:10]

    def follow(self, followerId: int, followeeId: int) -> None:
        """
        Follower follows a followee. If the operation is invalid, it should be a no-op.
        """
        if followerId not in self.follows and followerId != followeeId:
            self.follows[followerId] = [] 
            self.follows[followerId].append(followeeId)
        elif followerId != followeeId and followeeId not in self.follows[followerId]:
            self.follows[followerId].append(followeeId)


    def unfollow(self, followerId: int, followeeId: int) -> None:
        """
        Follower unfollows a followee. If the operation is invalid, it should be a no-op.
        """
        if followerId in self.follows:
            print(self.follows)
            if followeeId in self.follows[followerId]:
                self.follows[followerId].remove(followeeId)
```



