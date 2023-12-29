+++
title = "Why I added tracking and how it works"
date = 2023-08-26
draft = false

[taxonomies]
categories = ["dev"]
tags = ["webdev", "rust", "blog"]

[extra]
lang = "en"
+++

# Tracking and privacy
I have a small update to my blog before I continue writing some more blog-posts in the Christmas-holiday (happy 2024 btw if you are reading this around new-years). I have some ideas for new blog posts, but I wanted to add user metrics first. I already here some people say: "why add tracking?? That is not privacy friendly". Well, I have great news: I hate privacy-invading tracking as much as the next guy and I agree that big tech tracking is terrible development in the web. I am a great proponent of privacy-friendly apps: I use Linux, I use Firefox with privacy plugins and I try to degoogle my life as much as possible. 

How do I rhyme this with user-metrics? Well, I think there is a difference between tracking across multiple websites and gathering user statistics. I am strongly opposed the former but actively support the latter: I purposefully set KDE (my Linux desktop of choice) to gather the most data possible. The key difference  with KDE and companies like Google is that the data KDE gathers is anonymous and serves to better understand their users to improve the product. Gathering user-metrics like this is very important to the success of products or projects. Without them, you have no idea how your users are using your product or if anyone even uses it at all. There are some proxies for the amount of users, but these methods are murky at best and completely arbitrary at worst. An example is the amount of issues on a Github project: a percentage of users will file them, but for some projects this percentage is vastly higher than for others. 

My reason for wanting user metrics is simple: I am just curious how many people are reading my blog. I like writing them regardless of viewership but it is nice to know how many people are reading your work.

# What do I use
But enough faffing about: what tracking do I use and why.

My requirements for user analytics were simple:
- No big tech (especially Google Analytics)
- Free tier. I don't care about a maximum amount of event because I have low viewership
- GDPR compliance without a banner.
- Open source

I already had a whole blog-post ready about why I chose Posthog. I had even implemented a privacy banner and a defence of it. It still didn't really sit right with me because it was still too complicated for my liking. Then I decided to look at what [fasterthanlime](fasterthanli.me) uses and I saw that he uses [Goatcounter](https://www.goatcounter.com/). It is exactly what I am looking for: simple, anonymous, free and open source. I immediately deleted all my code for Posthog and just used that instead. I wasted some time setting up Posthog, but oh well: "it is what it is". At least I learned something.

One disadvantage of Goatcounter over Posthog is that Goatcounter is included in the EasyList filter which is included in Ublock Origin. Because a relatively large part of developers/techy people use Adblockers, this is quite unfortunate. I also recommend Ublock Origin myself so it's sad to see that it blocks a privacy friendly alternative to big tech solutions. I have opened a request for them to remove Goatcounter from the list, so let's see where that goes.

In the meantime, you can whitelist Goatcounter by adding these lines to your filter rules in Ublock origin: 
```
@@gc.zgo.at
@@goatcounter.com
```

I am planning to write a few more posts soon about Markdown and Redox OS, so stay tuned for that.

As always, you can comment on here with Github and subscribe to my blog via RSS-feed.

P.S This time I listened to [Rogér Fakhrs Fine Anyway](https://youtube.com/playlist?list=OLAK5uy_lhPmHPxfBU-CZ5_Pw8NVMzTSM3tVWQscA&si=sBqbHlc7y3kN3YRu). It is a folk album from Lebanon, which is nice for a change.