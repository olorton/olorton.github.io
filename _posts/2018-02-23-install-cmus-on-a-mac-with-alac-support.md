---
layout: post
published: true
title: Installing Cmus on a mac with alac support
date: '2018-02-23 15:19:00 +0000'
---

The aim of these instructions are:

- Install Cmus on a mac via homebrew.
- Include lossless ALAC support via ffmpeg.
- Get the Mac media controls working.

## Installing Cmus with ALAC support

This assumes that you already use [homebrew](https://brew.sh/) installed.

    brew install ffmpeg
    brew install cmus --HEAD --with-ffmpeg

    cmus --plugins

And you should see an entry for ffmpeg included in the output:

    ffmpeg:
      Priority: 30
      File Types: aa aac ac3 aif aifc aiff ape au fla flac m4a m4b mka mkv mp+ mp2
    mp3 mp4 mpc mpp ogg shn tak tta wav webm wma wv
      MIME Types:

To ensure that alac support is enabled, check that in the File Types of this section is: m4a - If that is missing something has gone wrong.

These instructions are based on a comment on this [GitHub issue](https://github.com/Homebrew/legacy-homebrew/issues/28752#issuecomment-42735025).

## Media keys

To get media keys working, install using the instructions on the [cmus-control GitHub page](https://github.com/TheFox/cmus-control)

