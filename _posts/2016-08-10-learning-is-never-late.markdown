---
layout: post
title:  "Learning is never late"
date:   2016-08-10 
published: false
categories: jekyll update
tags: learning, git
---
On Monday, August 8th I had a talk about Git version control system at [EVO Summer Python Lab'16][evo-summer-python-lab]. The funniest thing was that guys had already developed their projects and used Git at least for a month. I really had no idea what I can tell them. This is why I asked some of my friends to help: I asked they about what would they talk about if they had had such a talk.

One of my friends I asked for a help was [@rrader][github-rrader]. We had a pretty interesting chatting about different VCSs and their benefits. To my shame I new really a little about it. So this is why I decided to read about what Git does under the hood.

I [RTFM][git-man] and discovered a lot of surprising things. Have you known that Git was initially developed as a _Framework_ for creating Version Control System and not as the VCS itself? As for me, I didn't. Have you known that Git was initially developed as a _Framework_ for creating Version Control System and not as the VCS itself? As for me, I didn't. I did not know as well that Git has its own garbage collector, what the reference is and a lot of things that are obvious for those who read the manual before usage (while I tried to use and then read a manual). I found it very interesting that Git stores different kinds of objects: commits (which was obvious), trees, blobs, etc. Learning all that things was so fascinating, that I decided to include them in my talk.

While preparing the talk I've discovered some pretty tricks as well. I have finally learnt about reflog, and now I will not panic each time I accidentally reset some useful local commits. It was a big surprise for me to learn about `git bisect` and `git submodules`. These tools would save me a lot of time earlier. While preparing demo for `git submodules` I created my first bare repository to imitate a `Github` without accessing the network.

So what I want to write is that it is never late to learn something, and the necessity to explain something to someone might be a great motivation to explore new things and get new knowledges.

P.S. The slides from my talk can be found in [neighbour repository][evo-slides-git].

[evo-summer-python-lab]: https://www.facebook.com/evosummerpythonlab
[github-rrader]: https://github.com/rrader
[git-man]: https://git-scm.com/book/en/v2/Git-Internals-Plumbing-and-Porcelain
[evo-slides-git]: https://github.com/anxolerd/evo-slides-git
