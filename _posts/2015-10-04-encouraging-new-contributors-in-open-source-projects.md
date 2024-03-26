---
layout: post
published: true
title: Encouraging new contributors in open-source projects
date: '2015-10-04 18:49:59 +0100'
categories:
  - PHPNW
  - Open-Source
---
This weekend I attended PHPNW15, a fantastic conference with excellent talks, a great atmosphere, and a real community feeling. I particularly enjoyed the Friday evening hackathon where I joined the [Joind.in](https://joind.in/) team and submitted a couple of patches to the codebase. Having not contributed to the project before, it was great to sit down at the same table as the project maintainers, ask questions, make mistakes, and learn the codebase.

Compared to most projects, the interesting difference for me was that the Joind.in team have issues [marked as easy picks on Jira](https://joindin.jira.com/browse/JOINDIN-622?filter=10510), so that new developers can get contributing to the project from the second that they have downloaded the codebase. I'm aware that Joind.in are not the first open source project to do this, but it is not that common, and it should be. It made a real difference to my experience as a new contributor.

I decided to take a very quick and unscientific look at trending PHP projects on GitHub to see if my assumption is correct.

## Criteria

*   The contributing guide should be very easy to find from github readme or project website.
*   The easy issues should be clearly defined in the contributing guide or clearly labelled/tagged in the issue tracker.

## Results

| GitHub Project       | Easy Issues Marked | Contributor Guide |
|----------------------|--------------------|-------------------|
| delight-im/FreeGeoDB | no                 | no                |
| laravel/laravel      | no                 | yes               |
| symfony/symfony      | yes (8 open)       | yes               |
| bcit-ci/CodeIgniter  | not really         | yes               |
| yiisoft/yii2         | yes                | yes               |
| octobercms/october   | no                 | yes               |
| PHPOffice/PHPExcel   | no                 | yes, brief        |
| cachethq/Cachet      | no                 | yes               |
| WordPress/WordPress  | no                 | yes               |
| PHPMailer/PHPMailer  | no                 | yes, brief        |
| slimphp/Slim         | no                 | yes               |
| sphido/cms           | no                 | no                |
| dingo/api            | no                 | yes               |
| owncloud/core        | yes                | yes               |

I only spent a few minutes looking at each project in order to prove my point, but if I have made any errors in any of the above ratings please do let me know! [twitter.com/olorton](http://twitter.com/olorton)

I've also been generous to CodeIgniter, because they do not have clearly marked easy issues, but they do have an issue tag called "size:small" which is probably a good place to start.

## Conclusion

The results are quite clear, whilst most projects do have contributing guidelines which are required to help get a new developer started, only a handful of projects actually have clearly marked issues that are ready for new developers to get their teeth stuck into. In preparation for the PHPNW hackathon, I forked the project, read the contributor guidelines, ran tests, found an easy issue to fix, fixed it, and created a PR in under an hour and twenty minutes. How many other projects can honestly say that it is that easy to get started?

I'd like to put a call out to maintainers, developers, and organisers of other open source projects. Take a critical look at your project, how easy is it to get started on your project and contribute back? How much work is it to document and implement an easy-pick tag to your issue tracker? Lowering the barrier to entry is so important, please do it!
