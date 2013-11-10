---
layout: post
title: "Essential SublimeText Packages"
date: 2013-11-10 19:41
comments: true
categories:
- development
- productivity
---

[SublimeText](http://www.sublimetext.com/) is an excellent text editor. It's quick, light, extendable and does just enough to make you super productive then gets out of your way.

<!-- more -->

Using [Package Manager](https://sublime.wbond.net/), it's very easy to add extensions to the base SublimeText install.

For a great guide to getting SublimeText set up fully, check out Alex Maccaw's [blog post on the subject](http://blog.alexmaccaw.com/sublime-text). I'll deal with packages only.

Without further ado, here is my list:

1. [**All Autocomplete**](https://sublime.wbond.net/packages/All%20Autocomplete)
Sublime's autocomplete is wonderfully simple - by default it prompts you with any words in the current file. This package extends the default autocomplete to find matches in *all open files*.

2. [**Git**](https://sublime.wbond.net/packages/Git)
You can push, pull, diff and much more as you might expect. I have to admit, though, I only really use this package to *Git Blame* a file (or a highlighted section of a file) when I need to check out *who* authored a certain block of code and *when*. Event for that narrow use-case I'd recommend it.

3. [**Modific**](https://sublime.wbond.net/packages/Modific)
Highlights lines changed since the last commit. Currently-supported are: Git, SVN, Bazaar and Mercurial. Very cool to be able to see where you've deleted lines, added lines or modified existing ones with some simple iconography.

4. [**PrettyJSON**](https://sublime.wbond.net/packages/Pretty%20JSON)
Simple, really: you select some JSON, hit ```cmd + shift + p``` (to bring up the God menu) and start typing 'pretty' until you can select 'PrettyJSON'. That'll format the JSON for you.

5. [**RubyTest**](https://sublime.wbond.net/packages/RubyTest)
Like Git, I only really use one feature of this package. But it's a cracker. Assuming your spec and implementation files are organised in a predictable way, this give you a ```cmd + .``` shortcut that will jump you from the spec to the implementation and back again. If you're like me and like to TDD in two vertical columns, this is perfect.

6. [**SideBarEnhancements**](https://sublime.wbond.net/packages/SideBarEnhancements)
Gives you enhanced file and folder options. Good for moving things around rapidly.

7. [**Ruby 1.9 Hash Converter**](https://sublime.wbond.net/packages/Ruby%201.9%20Hash%20Converter)
This is is pretty controversial, but I thought I'd add it in as it's a great trolling tool. Gives you a shortcut ```cmd + option + h``` to convert all Ruby hashes in the current file to the new 1.9 syntax.

Please get in touch if you know any hidden gems that I'm missing!