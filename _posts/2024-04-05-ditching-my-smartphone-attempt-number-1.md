---
layout: post
published: true
title: 'Ditching my smartphone: Attempt number 1'
date: '2024-04-05 21:27:00 +0100'
---

## What did I want to achieve?

I am bored by my smartphone. I have owned an iPhone of some variety for thirteen years now, and I need a change. Change is good. I hate how I feel knowing it is in my pocket. This is not the right analogy, and so for want of a better way of describing this: it just feels like a ball and chain and a deadweight on my consciousness. Our time on this planet is precious, and I no longer want to waste it by staring at a phone screen. It lacks the value that I once appreciated.

Ditching my iPhone is not the only way to solve these problems, I _could_ change the way I use the phone: Get rid of apps that are a time sink; install apps that are more positive... but nostalgia tells me I am going to be happier without it.

I am not surprised that attempting this switch has turned out to be a multiple-attempt process. Because I thought this might be the case, I did not put too much effort into it. For now, I am going to call this attempt a success because I learned a bunch about the positives as well an encountering the unexpected pain points; and I now know what I need to adjust before my next attempt.

My ultimate goal is: To see if a life without a smartphone is possible for me, and whether I will be happier and more fulfilled not having one.

## What was my plan?

If I am able to ditch a smartphone I need to figure out what I am going to replace the many features that we love.

- Telephone: I bought a 4G Nokia 105, which obviously replaces the calling and text messaging features.
- Camera: Carry around my Fuji X-T1 with the flattest lens I own, which happened to be Fuji's F2 18mm, to reduce its bulkiness. I would have liked to have one of Fuji's X100 series as they are highly compact whilst producing stunning photos.
- Maps: These are a convenience of modern life, but most the time I do not really need it. If I am in an unfamiliar city, I would just buy a paper map, even a tourist map might do, or if in London an A-Z. Our main car has a built-in sat-nav, even if the UX is a bit shit, it would do.
- Group messaging: I cannot get rid of these, but I do not need them on me all the time, everywhere I go. I propose checking group chats once every day either from my iPad or one of my computers.
- Something to read: This is the key, I want to replace doomscrolling, with a book. If I am short of space in my bag, then I would carry around something smaller than whatever the current fantasy tome I am working my way through is.
- Something to listen to, music, podcasts, audiobooks: My old 5.5 generation, 30gb, white iPod. I love this little thing, but more on it later.
- 2fa: Ugh. I do not have a great solution for this. But since my old iPhone is going in a drawer next to my desk, I continued to use that. If I needed to travel for work, I would probably pack my iPhone for emergency 2fa!
- Calendar, todos, general notes: A paper notebook.

## How did it go?

Mostly OK. I managed a little under 3 weeks. But I was ill for most of this, and I did not leave the house much as I might usually. So this was not an entirely fair test. However, I learnt enough from it to have a new perspective.

The Nokia 105 4G, I chose because it was cheap, and I can tether a laptop/iPad to it. I would have preferred to have a [Punkt mp02 4G](https://www.punkt.ch/en/products/mp02-4g-mobile-phone), but I cannot drop £300 on an experiment. The main issue with the Nokia is that the audio quality on this thing is awful in comparison to a smartphone. At this price (£20), I am not surprised. But I had hoped using wired earbuds (with a mic) would have been better. They were for me, but not for the person at the other end. I need to repeat this test with some other headphones I have. If the mic in the headphones I used are to blame, then I can easily replace those and hold of buying another phone for the next attempt.

I loved having a proper camera on me when I was out and about. I took more photos, better photos, and I enjoyed the process more. Just throwing my camera in my daily bag felt rather dangerous, I am very precious about camera gear. I think that next time I will grab a small soft camera cube insert for my daily bag so that I can protect it from whatever other junk I keep on me, e.g. keys!

Other features like maps, group messaging, I did not miss when away from my computer. I enjoyed carrying a book around, and the notebook worked well to replace my calendar, todos, etc.

Overall this was a positive process.

## How did I get on with the iPod...

This is where I got stuck, and eventually switched back to the iPhone about 3 weeks in...

I loved the audio quality and after a little research it seems that this particular iPod has a highly sought after DAC chip in it. [I do not miss bluetooth one bit](/post/2017-09-23-headphones.html).

Surprisingly, I did not mind having to sync podcasts over once a day. I did not miss needing the latest podcasts injected into my device at supersonic speeds. I also found that not having the latest podcasts changed how I listen to podcasts: I prioritized them differently, and I explored others that I have subscribed to, but don't usually listen to.

My setup for syncing was, very awkward, and not a great long term solution. I use Linux on my laptop and desktop, no longer using a Mac makes syncing the iPod difficult. I tried gtkpod (which failed to build), and Rhythmbox (could not sync audiobooks or podcasts properly).

An aside... My research seems to indicate that most people are happy just copying files over to the ipod and listening to them like you would listen to music. But podcasts and audiobooks are different. Unlike music, you want to pause them, listen to something else and resume them later. Podcasts you want to be automatically removed once you have listened to them. The way the 5.5G iPod does this is by maintaining a proprietary database which is not on the hard-drive, but on a chip on the board. I believe that communicating with this has not been reverse engineered, and so open source software like Rhythmbox cannot sync podcasts and audiobooks properly.

In order to sync music, audiobooks, and podcasts properly, I installed Windows XP on VirtuaBox, and then installed iTunes 9. Ugh!

Then I discovered that despite patching WinXP, it seems that iTunes had its own SSL implementation and thus could not subscribe to any HTTPS podcasts, which they all are now. So I wrote a podcast mirror served over HTTP on my local network. This allows me to mirror the podcasts locally then pass these on to iTunes over HTTP rather than HTTPS.

Then I found that audiobooks over a certain length did not play properly. In fact when I discovered this, I was instantly taken back to the late 2000s when I remember buying an audiobook on iTunes and discovered these were split up to combat this issue. I was curious why they were split up, and never found out until now, but now I know. I now need to figure out if I want to write a script to split all of my recently backed up (de-DRM'd) audiobooks so they are iPod compatible. Ugh.

During all of this I did consider installing the Rockbox firmware on it. I may still take that route, but I think I want to see if I can set up a development version of Rockbox via a simulator or similar... I want to see what the experience of syncing from Rythmbox to Rockbox is before committing to this approach.

## Conclusion

So the reason to stop the experiment was because I needed to take some important phone calls, and the audio quality of the Nokia was not reliable.

I think I could have switched back and found solutions to the Nokia audio issues in good time, but I found the syncing issues with the iPod too painful and time-consuming to solve, so for now, I just gave up!

My todo list is as follows:

1. Test some other headphone mics with the Nokia to see if the call quality can be improved.
1. Setup Rockbox in a dev environment to test syncing with a Linux based audio app like Rythmbox.
1. If the above works, and if I still need to after using Rockbox, find/write a script to split audiobooks so that they are under a certain length, and are split on chapters.
