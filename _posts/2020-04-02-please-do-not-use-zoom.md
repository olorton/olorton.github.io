---
layout: post
published: true
title: Please do not use Zoom
date: '2020-04-02 10:18:00 +0100'
---

Zoom is a video call/conference software that has become very popular of late. The prime minister has been seen using it, my family have asked to use it, colleagues want to use it; however, I will not, and I encourage you not to as well.

All software developers have a responsibility to protect their users' data, audio, and video leaking from systems they have designed. They also have a responsibility to ensure that the systems that they run on are not open to being attacked or compromised. Zoom have repeatedly shown that they do not care about doing this. I do not really understand why though, other than the privacy/security issues, they have usable and popular software. They could be very, very successful in the long term. I suspect, but have no evidence, that management team or product owners are not listening to the development team; or possibly, the development team is incompetent. Either way, something is very wrong at Zoom.

Here are a few examples of their behaviour:

* [Last summer - a security researcher pointed out that malicious websites could activate the user's webcam without the user's permission.](https://medium.com/bugbountywriteup/zoom-zero-day-4-million-webcams-maybe-an-rce-just-get-them-to-visit-your-website-ac75c83f4ef5) Zoom would not agree that this was a security issue, instead claiming it was required to improve usability. Essentially, saying that usability is more important than security. Eventually, Apple had to step in an fix the vulnerability themselves.
* After pointing out the above issue, the security researcher had to decline the bug bounty payout because they wanted him to sign an NDA.
* [This month - a security researcher has disclosed that Macs are vulnerable to webcam and mic takeover again.](https://9to5mac.com/2020/04/01/new-zoom-bugs-takeover-macs-cam-mic-root/)
* [Zoom has been sending users activity to Facebook without their knowledge](https://9to5mac.com/2020/03/27/zoom-ios-app/), whether they have a Facebook account, or not. This feature/bug has now been removed, but not before the New York AG has started an investigation.
* [When installing Zoom on a Mac Zoom circumvents the standard installation process to install their software.](https://twitter.com/c1truz_/status/1244737672930824193) I believe that this is a flaw in the Apple installation system, and not really Zoom's responsibility; however, they choose to bypass it when they do not need to. Apple does need to take a look at this, they should be able to prevent Zoom from doing this.
* If you Windows users thought that only Macs were vulnerable to Zooms half-arsed approach to security, then you should be aware that the [Zoom Windows client is vulnerable to UNC path injection](https://www.bleepingcomputer.com/news/security/zoom-lets-attackers-steal-windows-credentials-run-programs-via-unc-links/).

I would love to go into the many issues with Zoom in more detail, but since I do not have time today, I think I'll leave you a list of other articles I have been reading on Zoom.

These are in no particular order ...

* [Jonathan Leitschuh - Zoom Zero Day: 4+ Million Webcams & maybe an RCE? Just get them to visit your website!](https://medium.com/bugbountywriteup/zoom-zero-day-4-million-webcams-maybe-an-rce-just-get-them-to-visit-your-website-ac75c83f4ef5)
* [John Gruber - Regarding Zoom](https://daringfireball.net/2020/03/regarding_zoom)
* [BBC News - Zoom is in everyone's living room - how safe is it?](https://www.bbc.co.uk/news/technology-52033217)
* [Engadget - There's another macOS update to fix Zoom security exploits](https://www.engadget.com/2019-07-16-macos-security-update-zoom-ringcenter-zhumu.html?guccounter=1&guce_referrer=aHR0cHM6Ly93d3cuZ29vZ2xlLmNvbS8&guce_referrer_sig=AQAAAH1oUyIdytMtBUO1YuLKEn95bAHccYVFfhJYRLSv4A0NUI-Rj4msloKqN9R1yBzqZ32IvDkZzPzQ7b-8VbZdzLfXdHLoBsscUDx950YLmVlJSh-FiRs0erEqFh65Mew4puzFROKR6Hvrt82j4ASNVKF0dPt7KtvlKaQT0J1gEjMx)
* [Wired - Zoom Will Fix the Flaw That Let Hackers Hijack Webcams](https://www.wired.com/story/zoom-flaw-web-server-fix/)
* [Doc Searls - Zoom needs to clean up its privacy act](https://blogs.harvard.edu/doc/2020/03/27/zoom/)
* [Business Insider - 'Alcohol is soooo good': Trolls are breaking into AA meetings held on Zoom video calls and harassing recovering alcoholics](https://www.businessinsider.com/aa-intergroup-meetings-zoom-bombing-trolls-alcoholics-anonymous-2020-3?r=US&IR=T)
* [twitter.com/DanAmodio - zoomAutenticationTool will run whatever script you give it](https://twitter.com/DanAmodio/status/1245329512889487361)
* [Hacker News - Zoom truncates passwords to 32 chars](https://news.ycombinator.com/item?id=22749706)
* [9to5mac.com - Ex-NSA hacker finds new Zoom flaws to takeover Macs again, including webcam, mic, and root access](https://9to5mac.com/2020/04/01/new-zoom-bugs-takeover-macs-cam-mic-root/)
* [objective-see.com - The 'S' in Zoom, Stands for Security](https://objective-see.com/blog/blog_0x56.html)
* [theintercept.com - Zoom meetings aren’t end-to-end encrypted, despite misleading marketing](https://theintercept.com/2020/03/31/zoom-meeting-encryption/)
* [An example of Boris Johnson using Zoom with the cabinet](https://mobile.twitter.com/borisjohnson/status/1244985949534199808)
* [twitter.com/c1truz_ - Hacky installation scripts](https://twitter.com/c1truz_/status/1244737672930824193)
