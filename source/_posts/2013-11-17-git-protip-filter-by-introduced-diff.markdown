---
layout: post
title: "Git Protip: Filter by Introduced Diff"
date: 2013-11-17 13:56
comments: true
categories:
- protip
- git
---

One of those Git commands you won't need regularly, but when you do, it'll save your day.

<!-- more -->

```
git log -S
```

What if you're tracking something down but you (or one of your colleagues) writes horrible commit messages?

Git blaming is really good for investigating who touched specific lines last, but you often find that the *last* change on any
specific line is not the one you're looking for. Maybe you want to find who introduced a method, but another colleague has formatted
the line since then.

Even tougher; perhaps what you're looking for is when a particular piece of code was *removed*.

Situations like these are when **Filter by Introduced Diff** comes to your rescue.

The command tells Git to look through the diff of each commit for a particular string. For example, if we wanted to find which commits modified
anything that looked like the function name ```Squeryable_by```, we would run this: (note there is no ```=``` between the ```-S``` and what you are searching for)

```
$ git log -Squeryable_by

commit 7fa49b6c8d18583a7a8279c5a50c056cc16f2857
Author: Stuart Liston <stuart.liston@gmail.com>
Date:   Wed Nov 13 15:17:12 2013 +1100

    Update README.md

commit 33b210008469fcc37a73516f6246a85398c72c3f
Author: Stuart Liston <stuart.liston@gmail.com>
Date:   Sun Nov 10 00:09:28 2013 +1100

    Starting to spec-out the module's DSL
```
You can see that I introduced a method on Nov 10 and then added some info to the README about the method (3 days later, YOLO!).

Hopefully that'll get you out of jail one day.

