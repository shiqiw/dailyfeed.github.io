---
layout: post
title: "Random topic about video download and upload"
date: 2018-07-08
permalink: /win/:year/:month/:day/:title
section: "technique"
---

## Introduction
I recently become a fan of an actor, wanted to download some of his videos, make video clips and then upload to Youtube, for entertainment and criticism only.

In this blog post, I'll cover the following topics:

1. Build Chrome extension to download videos
2. Use iMovie to make video clips
3. Upload to Youtube (understand Content ID)

## Chrome extension
Not in favor of manually click the download button for every episode I watch - what if I missed one or downloaded duplicated ones? Is it possible to make a Chrome extension to download while I'm watching?

The answer is yes:
1. Chrome dev tool enables user to inspect network traffic
2. Video request are marked as media - the request response content MIME-type is something like *video*
3. Trigger automatic downloads (Curl does not work, cannot find video in local cache)

Here are the steps:
1. [Build basic extension](https://developer.chrome.com/extensions/getstarted)
    - [Resize icon](https://www.quora.com/How-do-you-reduce-the-size-of-a-JPEG-file-on-MAC)
2. [Create dev tool extension](https://developer.chrome.com/extensions/devtools)
    - Add devtools.html which reference devtools.js
    - Intercept network traffic: chrome.devtools.network.onRequestFinished.addListener
    - Filter out duplicated requests
    - Pass request information to background.js
    - Open download page
    - TODO: force download

## iMovie
1. Trim video clips: go to the right frame, cmd+shift+s, ctrl+click -> split, delete unwanted section
2. Export to video type and size you wanted
3. TODO: tutorial about basic effects

## Upload to Youtube and Content ID
1. [How Content ID works](https://hkitblog.com/youtube-content-id-%E5%85%A7%E5%AE%B9%E8%AD%98%E5%88%A5%E7%B3%BB%E7%B5%B1-%E9%81%BF%E5%85%8D%E7%89%88%E6%AC%8A%E5%95%8F%E9%A1%8C%EF%BC%81/)
2. Respect Copyright, but you have right to dispute for reason such as criticism etc.