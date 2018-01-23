---
layout: post
title: "A simple Apple Script"
date: 2018-01-22
permalink: /win/:year/:month/:day/:title
section: "technique"
---

## Introduction
Recently I get addicted to a browser game. After spending a lot of time in it, I found this game only needs simple clicks here and there. As a programmer, why shall I waste time clicking mouse by myself?

## Process
Well I'm using a MacBook so after a little investigation, AppleScript seems like a good candidate tool to me. After enable ScriptEditor to access my computer, I want to have something like:

```
tell application "System Events" to tell process "Google Chrome"
    set frontmost to trye
    repeat 14400 times
        click at {850, 620}
        delay (1)
    end repeat
end tell
``` 

For some reason, this `click at` does not work. I tried using other commands such as `say "click"` to replace `click at`, and they all worked well. This is a common issue for Mac OSX. As a solution to this, I installed Cliclick. Now the script looks like:

```
tell application "System Events" to tell process "Google Chrome"
    set frontmost to trye
    repeat 14400 times
        do shell script "/usr/local/bin/cliclick" & quoted form of "c:850,620"
        delay (random number from 1 to 3)
    end repeat
end tell
```

## Next step
In next few days I may spend some time to make a similar script to click on certain button based on different cases. The core idea is the same.

## Reference
1. [用AppleScript在Mac系统下实现按键精灵的功能以及在游戏中的运用](http://blog.xcodev.com/posts/auto-key-press-using-appscript/)
2. [Cliclick](https://www.bluem.net/en/projects/cliclick/)