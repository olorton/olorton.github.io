---
layout: post
published: true
title: Finishing projects
date: '2022-05-18 19:18:00 +0100'
---

I love minimalism. I adore the Bauhaus asthetic. I enjoy reading and writing plain text files. I envy those that can throw out most of their belongings. But when it comes to writing software for pleasure, I cannot seem to embrace the MVP approach.

Having admitted that, I think it is really hard to do. I have seen colleagues and clients struggle with this as well. They have a desired feature list, and nothing is going to stop them from insisting that every feature is needed to launch their amazing application. That is until they realise how much it's going to cost. Then it seems that some of the features are more nice-to-haves. But, enough about other people, I cannot seem to finish any of _my_ projects, and I want to fix that.

I have a new project that I want to start, several actually, so to be successful by my standards I need to understand what is going on. I have brainstormed a few possible causes and improvements I can make, and it sort of boils down to two main things:

## Be brutally minimalist

Remove all the features/desires that are not needed to publish the website, app, or codebase. There should be one goal/feature. Build that, and that only. This means:

- Treat every project like a hack-day. Have a limited timeframe with which to launch it. You can fix issues or add features later.
- For example, include no user sign-up. Most of the web apps I build as personal projects are for me, and whilst I may want authentication this can be achieved by slapping http basic auth in the nginx.conf. It takes 5 mins.
- No, or very basic design/CSS. Honestly, I am not a frontend dev, and just do not care. That can come later. e.g. pinboard.in has been very popular with only minimal CSS.
- No automated tests. Some devs will find it easy to get behind this principle, and some will not. It may be faster for you to adhere to proper TDD methodologies, but if you are building something small, just build it and stick it online. Add tests later, and save TDD for bugs and maintenance issues.
- Use a framework that allows you to move quickly and doesn't get in your way. For me, this would be Flask or Django. I love the one file Flask setup that allows me to set up a few routes quickly.
- Proudly built elsewhere. Use third party code to achieve your aims, but only if it will be quicker to learn someone else's tool than to build your own.

## Be conscious about how productive you want to be

Everyone has a busy life, me included. I am not 20 anymore, and my carefree attitude to my time has gone and has been replaced by a family and house and a life that need my time. This means that every minute is sacred and must be spent wisely, so I should plan how I am going to spend my time so that my latest project gets completed and launched.

- Write down everything I need to do to complete _and launch/finish_ the project.
- Remove every step that can be faked or added later, be brutally minimalist.
- If it can be completed in an afternoon/day, set aside time to do this, and crack on with it.
- If you cannot complete it in a day, then make time to work on the project for 20 minutes every day. Regularly touching the codebase or planning tools will keep the momentum going.

## Final thoughts

Who knows if this approach will work. I will have to revisit this post to see what if any of these approaches helped.

As well as writing software, I wonder if I need a brutally minimalist approach to blogging. I want to write more here, this site is unloved.
