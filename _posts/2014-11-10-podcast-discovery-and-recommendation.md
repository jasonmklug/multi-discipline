---
layout: post
title: "Podcast Discovery & Recommendation"
published: true
category: problems
---

If you, like me, are widely curious and always trying to expose yourself to new ideas, you *ought to* consider the rise of podcasting as a medium to be nothing short of revolutionary.  For someone who carries an intense interest in a few subjects — and a passing interest in many, many more — the *right kind* of podcast can offer the caliber of insight that used to require tuition and a lecture hall (and often does so through hosts and guests with engaging personalities and an infectious passion for the subject matter).

I’ve posted [the "Maker" subset of my podcasts subscriptions](http://multi-discipline.com/podcasts/).  That grid shows about 1/3 the *total* list of feeds through which [my podcatcher of choice](https://overcast.fm) iterates every time it checks for new episodes (most of these podcasts post on a weekly schedule).

If not for the fact that writing code (or prose) requires focus from the same part(s) of the brain which process verbal language, I’d be actively keeping up with even more.  As such, my podcast consumption is limited —  quite literally — by the number of waking non-working hours in a day.

> *"So, ladies and gentleman, if I say I'm an podcast fan, you'll agree."* -Me

## The Problem

There is a vast (and growing) landscape of podcasts available to any listener with the time and inclination to seek them out.  Most listeners, however, are *not* inclined to spend time perusing podcast directories for new must-listen shows; they have a few which suit their daily commute, and that’s as far into the landscape as they need to explore. ([Filthy casuals](http://knowyourmeme.com/memes/filthy-casual).)

Or, approached from the "recommender" side: when one listener finds a show or episode they really like, they have limited outlets through which they can recommend it to other would-be listeners.

Speaking for myself: I *almost* always tweet a link to the feed and/or episode URL of a show which I find interesting, entertaining, or useful.  But I wouldn't be surprised if those recommendation tweets (given, as they are, in a stream-of-posts context which is impermanent by design and affords no immediate action for podcast listening or subscription) are lost on many who *would have* taken a listen, but weren't in a position to immediately:

1. Stop what they were doing
2. Open their [podcatcher](http://en.wikipedia.org/wiki/List_of_podcatchers)
3. Find the show (or, if the podcatcher has no directory feature, copy/paste the show’s feed URL)
4. Subscribe to the show (or download the single episode)

## The (Proposed) Solution

A service which allows users to recommend single episodes of their favorite podcasts, and to “follow” the episode recommendations of other users, which the system compiles into a single appropriately formatted RSS/XML personal “followed” feed for each user.

As far as I can see, the best-fitting model already in existence is the humble [retweet](https://support.twitter.com/articles/77606-faqs-about-retweets-rt).

But, like the retweet — in order to enable that behavior, you first need a system to handle the basic re-share-able units of content (in our case, podcast episodes).

### Desired Behavior:

* As a user, I “follow” other users whose podcast recommendations I think I’d find interesting (probably people whose interests I already know mirror my own, thanks to their presence on other social sites/services).
* Individual episodes which have been recommended by users who I follow will be added to my “followed” feed.
* Like retweets, even if more than one user who I follow recommends an episode, that episode is only added once to my “followed” feed.
* When I want to expand my podcast horizons through a set of socially curated episode recommendations, I should be able to simply open my “followed” feed (which has all of the recommended individual episodes compiled into a single feed) in my podcatcher, and play an episode.
* The rest of my subscriptions in that podcatcher should not be affected.
* If I find an episode interesting enough that I want to subscribe to the podcast directly, there should be a button for doing just that on the individual episode’s “now playing” or “info” view.
* If someone I follow adds a recommendation for a podcast to which I’m already subscribed, that episode should not appear in my “followed” feed.

## The Tools

* **Web Site** (acts as hub for creating an account, finding users to follow, recommending podcast episodes, etc.)
* **API for Web Service** (which the site and developers of podcatchers can use to authenticate service users, pass along episode [un]recommendations, add user’s “followed” feed as subscription, etc.)
* **Cooperation of Developers** (much in the way that third-party apps have integrated with useful "personal collection" services like [Pinboard](https://pinboard.in) and [Instapaper](https://www.instapaper.com/))

## The (Proposed) Process

This remains to be seen, but I believe the first step would be to build an MVP of the website and service.  Obviously, it wouldn’t be *as* feature-rich on its own as it could eventually be once third-party podcatcher developers build integrations; but it would be a useful start for the steadfast core of Podcast Superfans&trade; who want to push and collect episode recommendations right away. ([There are dozens of us... DOZENS!](https://www.youtube.com/watch?v=lKie-vgUGdI))

Until third-party developers adopted it, service users could simply copy/paste the URL of their personal “followed” feed ([LIKE AN ANIMAL](http://www.kungfugrippe.com/post/20021002957/like-an-animal)) to subscribe in any podcatcher, just like any other podcast feed.  They could also manually add/remove podcasts to/from an “I’m already subscribed” list on the system, to prevent recommended episodes of podcasts to which they’re already subscribed appearing in their “followed” feed.

These temporary workarounds would be *tedious*, but not sufficiently *frequent* to make use of the service into a chore.

## The (Expected) Outcome

Since sharing recommendations is something done without any *real* expectation of return or interaction, it *shouldn’t* matter, at the outset, whether anyone is actually following you (meaning the inherent chicken-and-egg problem of social-dependent services *should* be avoidable).  As it stands now, this is something I do with zero feedback about whether my recommendations are appreciated, or even noticed (let alone acted upon).

And since podcasts, by their nature, require a time commitment to consume, a single-digit queue of recommendations is enough to keep a user busy for hours (unlike, say, Twitter — where a user must follow *at least* a few dozen other users to be ensured consistent fresh new content).  This means a user could conceivably fill their available podcast listening time by following just two or three recommenders.

Given the right circumstances (and eventual third-party developer integration) a service such as this could be expected to keep podcast listeners continually returning to the recommendation well for another quality dip of socially filtered podcast goodness.

It would be interesting to see how a recommendation machine constantly churning out appropriately recommended content fares when it bumps up against the inherent limit to a human’s available daily (weekly, monthly) listening hours, and how that ultimately affects the decision users make about what to consume in their preciously limited time.

If it could help casual listeners to "level up" their podcast consumption (in terms of quality, if not hours), I feel like it would be a solid win for the medium.