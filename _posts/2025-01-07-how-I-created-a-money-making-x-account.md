---
title: "How I Created a Money Making X Account"
date: 2025-01-07
categories:
  - blog
tags:
  - automation
  - money
  - development
---

In 2018, I came up with the idea to create an *automated* Twitter account that shared posts from my favorite subreddit. At the time, I had no plans to monetize it—or even attract followers. It was purely a fun, personal side project driven by my own interests.

Like most social media accounts, it took quite a while to gain a following. I remember when I hit 1,000 follower on the account I was ecstatic. The account currently has __264k+__ followers, which is insane! 

When Elon took over Twitter (now X), it was business as usual for the account. Then came the announcement: creators could earn money through ad revenue from their posts.

For a while I didn't think much of it. I had a moral dilemma as well, as I wasn't the one coming up with the posts. Once I started seeing some user's payouts, I was intrigued to say the least. I signed up for a premium account and applied for monetization. My first payout was almost $500, from January-September 2023. 

```
+$484.28
Pay period: Jan 31, 2023 - Sep 15, 2023
```

The bi-weekly payouts for the account have pretty much all been under $100, but this account is 100% automated so I'll take it! 


## The (not so) Technical Details

The bot is powered by a cron job running on a Raspberry Pi. The job runs every 2 hours. 

I use the Reddit wrapper [`praw`](https://praw.readthedocs.io/en/stable/) to loop through posts in the subreddit. I check to see if the post already exists in my timeline by referencing a `.txt` file (I know, I know) that has the list of posts I've already posted. If the post doesn't exist, we are good to post it. 

I grab the image of the post using `urllib.request` and save it. 

I compose the tweet using the [`tweepy`](https://docs.tweepy.org/en/stable/) client. I first upload the image to X, then I compose the post with the title from the Reddit post along with a link to the source, and the `media_id` that was just uploaded. I save the text of the tweet in `tweets.txt` so we don't get duplicates on the timeline. 

```python
def send_tweet(extension):
    media = api.media_upload("images/image" + extension)
    tweet = client.create_tweet(text=caption, media_ids=[media.media_id])
```

And that is pretty much it! 

This project was never about making money—it was simply an idea I brought to life. Now, thanks to a bit of luck, it brings in some extra cash. Even without the payouts, this account would still be running, fueled by the same enthusiasm that started it all.

