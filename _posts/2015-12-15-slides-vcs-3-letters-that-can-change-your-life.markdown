---
layout: post
title:  "VCS. Three letters that can change your life"
date:   2015-12-15 00:23:05
categories: dev
author: anxolerd
image: '/images/posts/slides-vcs-3-letters-that-can-change-your-life/cover.png'
---

It is difficult to imagine a modern developer who knows nothing about version control systems or does not use them. There are a lot of articles all over the Internet about VCS and this one is not better than the others.
However I strongly believe I have to write it, because not everyone understands the importance and the beauty of Version Control Systems.

About a week ago I had a talk in my university about VCS. I talked about basics of VCS and provides a live demo on Git VCS. Here I'll try to recall my memories and write down all the points of that speech. So here I start.  

### Why do I write about version control systems?

- It is vital to modern programmer to know how to use version control systems
- Version control systems simplify software development
- VCS simplify collaboration on source code
- Using them might help you to save months of your work!!!

Indeed, version control systems simplify software development. It often happens that someone messes the whole project with a bunch of changes. You can try to find all his changes manually and undo them. You'll definitely spend a lot of time doing this.
But why do not you rely on VCS for that? It stores all your history and you can easily control changes done by someone. Moreover, there are commands which allows to undo specific set of changes! It is just useful when you work on project alone and 
extremely needed when you work on team.

![undo.gif][undo.gif]{: .responsive-image}

By the way, how do you share code when work in the team? If you do that using flash drives o email attachments, I have a pretty bad news for you. Doing that is like using stone instruments in the 21st century...

![stone-age.jpg][stone-age.jpg]{: .responsive-image}


### Bunch of theory.
So what is this magical Version Control System? According to _[Wikipedia][wikipedia]_:

> A component of software configuration management, version control is the management of changes to documents, computer programs, large web sites, and other collections of information.

Another definition can be found in the [official documentation][git-scm-about-vcs] of Git VCS:
 
> Version control is a system that records changes to a file or set of files over time so that you can recall specific versions later.

So, in general __VCS__ is something that saves all versions of project files and allows you to restore any of them quickly. Not so scary. huh?

There are two classes of such systems:

#### Centralized Version Control Systems

![cvcs-workflow.png][cvcs-workflow.png]{: .responsive-image}

These were the first ones. The idea of CVCS is that there is a single `"central"` repository somewhere (typically on the server) and everyone commits their changes to it. Committing a change mean recording the change in the system. Other contributors can see this change. 
Typical workflow with centralized systems is described here:
 
1. Pull down any changes other people have made from the central server.
2. Make your changes. As there is only one copy of repository be careful and make sure your changes work properly.
3. Commit your changes to the central server, so other programmers can see them.

Pretty straightforward, isn't it?

#### Distributed Version Control Systems
Unlike CVCS, where only one repository exists, the idea of distributed Version Control Systems is that there are many copies of the repository. Every single developer has his own copy and works with it. That means, everybody who has a copy of repository also has a whole editing history, not only the latest revision.
 
![dvcs-workflow.png][dvcs-workflow.png]{: .responsive-image}

In general distributed VCS are better than centralized ones.

- __DVCS are faster.__ 
  Performing actions other than pushing and pulling changesets is extremely fast because the tool only needs to access the hard drive, not a remote server.
- __Nobody sees unfinished work.__ 
  Committing new changesets can be done locally without anyone else seeing them. Once you have a group of changesets ready, you can push all of them at once.
- __Less dependent on the internet.__ 
  Everything but pushing and pulling can be done without an internet connection. So you can work on a plane, and you won’t be forced to commit several bugfixes as one big changeset.
  
#### There are three most popular VCS now:

##### Subversion
![subversion_logo.png][subversion_logo.png]{: .responsive-image}

Centralized version control system. It is used in a lot of big projects, which were started, when there were no DVCS. Subversion is developed by _Apache Software Foundation_

##### Mercurial
![mercurial_logo.png][mercurial_logo.png]{: .responsive-image}

Mercurial is a cross-platform, distributed revision control tool for software developers. It is mainly implemented using the Python programming language, but includes a binary diff implementation written in C

#### Git
![git_logo.png][git_logo.png]{: .responsive-image}

Git is a widely used version control system for software development. It is a distributed revision control system with an emphasis on speed, data integrity, and support for distributed, non-linear workflows. Git was initially designed and developed by _Linus Torvalds_ for Linux kernel development in 2005.

### Hello Git
Let get started with Git VCS. First of all wee need to install it. If you use Windows, go to [official website][git-scm-downloads] and download the latest version.
If you use Linux, you can install Git using your package manager. In `Gentoo` for example just execute

{% highlight bash %}
emerge -av git
{% endhighlight %}

In the following steps I assume you use either `Git Bash` on Windows or `bash` on Linux system.

Now you have to configure git. Just setup your name and e-mail address:

{% highlight bash %}
~ $ git config --global user.name "Cute Cthulhu"
~ $ git config --global user.email "fhtagn@example.com"
{% endhighlight %}

Now we are going to create a project and add it to the repository.

{% highlight bash %}
~ $ mkdir my-proj
~ $ cd my-proj
~/my-proj $ git init # initialize empty git repository
~/my-proj $ echo "hello world" > hello.txt # write "hello world" to file hello.txt
~/my-proj $ git add hello.txt # add hello.txt to version control
~/my-proj $ git commit -m "initial commit" hello.txt # commit changes
{% endhighlight %}

That's all! If you have followed my steps you have just created a new git repository and have done your first commit to it!
There is a good 15-minutes long [tutorial][git-tutorial] on Git VCS. If you are new to Git, I strongly recommend it to you.

### Links
As I have mentioned, I have talked about VCS at my university. If you wish you can watch out my slides [here][slides].
Of course, the main source of knowledge is the official [git][git-scm] documentation.
There is also a good [tutorial][atlassian-tutorial] provided by _Atlassian_. And just in case if you messed your repository, you can find the rescue recipe in [this article][git-fix-all].


[undo.gif]: /images/posts/slides-vcs-3-letters-that-can-change-your-life/undo.gif
[stone-age.jpg]: /images/posts/slides-vcs-3-letters-that-can-change-your-life/stone-age.jpg
[cvcs-workflow.png]: /images/posts/slides-vcs-3-letters-that-can-change-your-life/cvcs-workflow.png
[dvcs-workflow.png]: /images/posts/slides-vcs-3-letters-that-can-change-your-life/dvcs-workflow.png
[subversion_logo.png]: /images/posts/slides-vcs-3-letters-that-can-change-your-life/subversion_logo.png
[mercurial_logo.png]: /images/posts/slides-vcs-3-letters-that-can-change-your-life/mercurial_logo.png
[git_logo.png]: /images/posts/slides-vcs-3-letters-that-can-change-your-life/git_logo.png

[wikipedia]: https://en.wikipedia.org/wiki/Version_control
[git-scm-about-vcs]: https://git-scm.com/book/en/v2/Getting-Started-About-Version-Control
[git-scm-downloads]: https://git-scm.com/downloads
[git-tutorial]: http://try.github.io
[slides]: http://anxolerd.github.io/kpi-slides-vcs/
[git-scm]: https://git-scm.com/
[atlassian-tutorial]: https://www.atlassian.com/git/tutorials/
[git-fix-all]: https://github.com/blog/2019-how-to-undo-almost-anything-with-git