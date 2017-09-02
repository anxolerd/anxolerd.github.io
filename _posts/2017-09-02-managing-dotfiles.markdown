---
layout: post
title:  "Managing dotfiles"
date: 2017-09-02 22:51:58 +0300
categories: personal dev
---

Recently I switched from jetbrains IntelliJ platform to neovim editor. That was
a complete accident and it is still a surprise for me that it happened. On the
first time I played with editor configuration a lot: testing different plugins
for completion, checkers, syntax highlighting, search, etc. And it was hell of a
pain to sync that configuration between personal laptop and work machine. And
this article is about that pain.

First of all, I discovered that there was a complete mess in my dotfiles. I did
not understood why do I need half of them. So I started deleting them one-by-one
and broke some things a few times. However that helped me to minimize
configuration files and find only those I really needed.

Secondly when I started to sync files using a simple scp (yes, i know how dumb
is that) I had to deal with badly-written config files which had a lot of
hardcoded non-relative paths which caused crashes because of different usernames
on machines. So the second step was to fix those by replacing `/home/username`
with just `$HOME` in every single configuration file.

After that I decided to do something with my [old tmux configuration][old tmux
configuration], which was messy and 90% copy-pasted from somewhere I do not
even remember. I started to love the default green color and discovered a great
[tmux plugin manager][tmux plugin manager]. This allowed me to keep a
configuration file much cleaner and easier to support. The rule I followed is to
use as little plugins as possible, anyway I couldn't remember all the shortcuts
form all plugins.

As for session management I decided to use [tmuxp][tmuxp] instead of
[tmuxinator][tmuxinator] or [tmux-ressurect][tmux-ressurect]. The reason for
that was simple: tmuxp uses python to run and I already need python on my
machine, which is not true about ruby which was used by most of tools like
tmuxinator.  As for tmux-ressurect, it loads/saves all sessions at once, while
tmuxp allows to load only single session i need right now and do not run others.  
I do not want to say that tmux-ressurect is bad, all I mean is that it does not
fit my workflow while tmuxp does.

The next step was to improve the shell prompt. I used to use a modification of
[geometry theme][geometry theme], which was nice, but required me to make some
modifications to display several things I wanted. With [spaceship][spaceship]
I can forget about manually editing a theme and use it out-of-the-box. This
allowed me to remove a bunch of custom (my) code from my configuration and make
it cleaner.

![desktop.png](/public/images/posts/managing-dotfiles/desktop.png)

I have also played a little with window manager configurations and other stuff,
which is not actually interesting, so I'll skip this part.

So now I have all the configurations which work pretty good and do not depend 
on username, but I still have to keep them in sync between machines. Previous
solution with just copying files is not that good and has the following major
issues:

- Copies are not linked with the source, thus making any changes in copies won't
  affect the original configuration files which will lead to the two or more
  completely separated configurations, which will be hard to merge together.
- There are plenty of config files and it is not convenient to always remember
  where to copy what. As the number of files grows, it becomes harder to update
  configs.

While the first issue can be simply resolved by symlinking configurations to the
files from repository, the second one is a bit harder. There are a bunch of
tools out there listed in the [GitHub ❤ ~/][GitHub ❤ ~/], and it is hard
to choose. Some of them (as I understood from their READMEs) just keeping a git
repo in the home directory, which is an overhead, if you ask me. Some of them
require copying themselves in the user's dotfiles repository, which I do not
like because that means I'll have to update the script alongside with updating
my configurations. So I asked for help from my colleagues. Surprisingly I
received two answers. First one was like

> If you do not edit your dotfiles you do not have to worry about syncing them

![wise](/public/images/posts/managing-dotfiles/you-do-not-have-to-worry.jpg)

While this being true, it does not fit my needs, as I sometimes experiment with
configurations trying to make things more convenient for me. And when I
experiment with them, i do a lot of changes which I want to move between my
machines. Moreover, I need a way to bootstrap my dotfiles at new machine if
needed. Just in case, you know.

The second answer was a little bit more constructive:

> Instead of writing a guide what to copy where, just write a script which does
> that.

That sounds better. While I still have to keep the script updated, I will be
completely sure that script updates will not break anything in my workflow 
because it is only me who manages that script. Moreover it is one more chance to
practice shell scripting, so why not give it a try?

There is one point I need to mention: I need some software dependencies to make
my configurations work. This is why my script not only symlinks configuration
files to the proper location, but also installs the dependencies. Here is [how
it looks][how it looks]. There is one thing I highly dislike about the
installation script I wrote: it works only on systems which use [dnf package
manager][dnf package manager] as software installation commands are hardcoded in
the script.

In conclusion I'd like to say that despite being a pain, it was also funny and
interesting to prettify and improve my system configurations. And what I liked
the most is writing the installation script. However I'm still looking for the
perfect dotfiles management tool and if someone knows a good one, I'd really
appreciate if you let me know about it.


[old tmux configuration]: https://github.com/anxolerd/dotfiles/blob/4f0b8a5ac60fc17945e87e915cd6074ffe293743/tmux/.tmux.conf
[tmux plugin manager]: https://github.com/tmux-plugins/tpm
[tmuxinator]: https://github.com/tmuxinator/tmuxinator
[tmux-ressurect]: https://github.com/tmux-plugins/tmux-resurrect
[tmuxp]: https://github.com/tony/tmuxp
[geometry theme]: https://github.com/geometry-zsh/geometry
[spaceship]: https://github.com/denysdovhan/spaceship-zsh-theme
[GitHub ❤ ~/]: https://dotfiles.github.io/
[how it looks]: https://github.com/anxolerd/dotfiles/blob/d3b912c118c17cc097998b8e7a4c8776205bea94/install.sh
[dnf package manager]: http://dnf.readthedocs.io/
