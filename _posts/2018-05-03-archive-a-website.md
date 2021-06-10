---
layout: post
published: true
title: Archive a website
date: '2018-05-03 9:14:00 +0100'
---

On occasion I find a small website that is an amazing resource, these sites are often negelected, and can occasionally disappear from the web. I find that sometimes a site is so valuable, that I'll check that it is in [the wayback machine](https://archive.org/). If it is not, then I will archive the site myself, for personal reference.

This post serves as a reference for creating that archive using `wget`.

```
wget \
    --recursive \
    --level 10 \
    --page-requisites \
    --adjust-extension \
    --convert-links \
    --domains amazingwebsite.com \
    --no-parent \
     amazingwebsite.com/posts/
```

`--recursive` Turn on recursive retrieving.

`--level 10` Increase the default recursive depth from 5 to 10.

`--page-requisites` Download all the files that are necessary to properly display a given HTML page.

`--adjust-extension` Add a suitable file extension depending on what type of file is being downloaded.

`--convert-links` After the download is complete, convert the links in the document to make them suitable for local viewing.

`--domains` Set domains to be followed.

`--no-parent` Do not ascent to the parent directory when retrieving recursively. Very useful if you only wish to archive a single page, or a small section of a site.

