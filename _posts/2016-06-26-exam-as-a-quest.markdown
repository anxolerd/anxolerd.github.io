---
layout: post
date: 2016-06-26
title: "Exam as a quest"
categories: updates
published: false
tags: kpi, education, personal
---

## Preambula 

Exams are over and now I have some free time to write to my blog. This year at university my friends and me had a networks course which was partially based on [Cisco's CCNA][cisco-ccna] course. That was pretty interesting course and we learned a lot of interestings there. The most amazing thing was our teacher who really wanted us to learn something, not just complete the course. We could answer questions for half an hour until we finally started to understand what we are trying to do. And that was really inspiring and motivating.

But the most interesting part was the exam for this course. Teacher asked some of my friends and me to help him with exam preparations because he wanted it to be something more interesting and useful than a bunch of standard questions.

## So here we started.

We had really little time to create a great idea and implement it. There was some hackathon spirit in this. We spent two days just gathering the ideas and exploring possibilities of their implementation. After that we met and tried to combine all the ideas together as well as reject extremely difficult ones. We've generated about 40 questions and ideas and rejectedabout half of them. We did our bests to find the balance between complexity, engagement and possibility to solve the questions. Of course, if we had a little more time, we could find even better solutions than we did, but in my opinion we did it even better than we expected.

After we were done with list of questions and ideas we had only two days to implement and test them. Actually we had only two evenings and two mornings to do that all becasue we all have a job to do at the daylight. So we were in rush. In the last evening before deadline (the exam) we sat till 11 p.m. trying to find and fix bugs we did during creating and implementing tasks.

## The curtain falls 

And here is the exam. We were so excited to present our creation to other students. It was a quest. Students had to solve quizzes and do practical tasks to find keys to the next stages of our simple quest. We used Cisco's Packet Tracer as quest environment because that was the software we used during the course.

![student-topology][student-topology]{: .responsive-image}

Our quest consisted of two topologies in Packet Tracer and the instruction which was given as *.pdf file. Students had access only to one topology and the instruction. The other topology was unaccessible to them. To complete the quest they had to recall a bunch of theory from our course as well as to do some things they used to do as assignments during the whole course. These things included:

- Knowledge of OSI model layers
- Knowledge of main protocols used on different layers
- Configuring (using GUI) DHCP server
- Configuring (using GUI) dynamic routing (RIP)
- Using some network diagnostics utilities
- Using some basic applications
- etc

As I wrote student had access to one of the topologies. They had really **full** access to it, wo it was a challenge for us to prepare tasks there. We used some static webpages on HTTP servers which used some simple `JavaScript` code to hide/show the key for the next step. We had to encrypt keys there to avoid students just look into the page source to proceed. We used a [viginere cipher][viginere-cipher] for that. _I really enjoyed the moment when one of student tried to look for answer in the sources but found an encrypted string there. He said very loudly something like:_

> "Oh you are tricky guys!"

In order to reduce compatibility issues students did their quest on remote server. And to access the tasks in the other topology they had to connect to one more remote server.

In total our quest took about hour and a half for stuents to complete it. 

## Difficulties

While we prepared our quest in such a rush we encountered some difficulties while studens tried to complete it. Here they are

- Slow computers. Computers students used to connect to remote servers were extremely old. The often stuck and hanged, so it was an unpleasant thing. Some of students used Windows build-in [RDP][rdp] client to connect to remote servers and some of them used a [thinstation][thinstation] for that. While windows RDP clients were stable, but PCs were slow themselves, thinclients were extremely unstable. They dropped connections randomly and AFAIK we did not find a reason for that. 
- Overloaded server. Students connected to virtual machines which were running on the remote server. While we tested that there was only one user and we did not predicted so high load when about 10 students connected to server simultaneously.
- Lack of time. Well, as I wrote we really had a little time to prepare the quest. Hence we used to test all that things "in production". Luckily we solved most of issues before that.
- Unability to track the progress completely.
- Unability to automate the exam submission and check.

## Feedback

As we did that quest as proof-of-concept, we asked to leave some fedeback about the quest and about 50% of students did it. So here I'll provide some statistics based on their responses.

All the respondents liked the quest and we are really happy about that.
### Quest complexity

We asked students to grade the quest overall complexity from 1 (extremely easy) to 7 (extremely difficult). 

![complexity-chart][complexity-chart]{: .responsive-image}

According to feedback we received, quest had exactly perfect complexity while being a little bit difficult for some students.

Some tasks like _configure DHCP_ seemed too easy for most of respondents. Some taks were easily hackable with bruteforce. On the other side most of respondents found subnetting and routing the most complex one (just as planned).

### Quest engagement

Most of students found the quest pretty interesting and engaging. (0 -- not interestng, 7 -- very interesting).

![engagement-chart][engagement-chart]{: .responsive-image}

While being one of the most difficult tasks, configuring the dynamic routing was also one of the most interesting. The other interesting task was to recieve an email with the instructions. Students had to configure a network (use correct IP addresses, range, mask, default gateway) and answer some questions to get the correct configuration parameters for email client.

### Issues

![issues-chart][issues-chart]{: .responsive-image}

_here blue part is the part which encountered issues during the quest and the red part is those who did not_

Unfortunately about 45% of respondents encountered issues during the quest. That was mostly a problem with either slow and old PCs or Buggy thinstation that were mentioned before. Some students complained about some tasks were not clear. 

### Comments and propositions

Most of them were pretty similar like _"That was a great idea"_. One guy wrote the following proposal:

>  Please add a storyline about hacking the Pentagon

And two guys proposed to add some tasks in command line. _Hey, guys, if you read this, we had some ideas about that but we used to reject them as the were too complex for the most of students =(_

## Conclusion

So it was a great experience with making the exam interesting. Students liked it and it was great. We got some feedback and we know how to prepare even better quest if it will be needed. Special thanks to our theacherfor such experience and to [@LdmlD][gh-ldmld] and [@ttatus][gh-ttatus] for great quizzes and testing. And of course huge thanks to students who did this quest on exam =)


[cisco-ccna]: https://www.netacad.com/courses/ccna/
[student-topology]: /public/images/posts/exam-as-a-quest/student-topology.png
[viginere-cipher]: https://en.wikipedia.org/wiki/Vigen%C3%A8re_cipher
[rdp]: https://en.wikipedia.org/wiki/Remote_Desktop_Protocol
[thinstation]: http://thinstation.github.io/thinstation/
[complexity-chart]: /public/images/posts/exam-as-a-quest/complexity-chart.png
[engagement-chart]: /public/images/posts/exam-as-a-quest/engagement-chart.png
[issues-chart]: /public/images/posts/exam-as-a-quest/issues-chart.png
[gh-ldmld]: https://github.com/LdmlD
[gh-ttatus]: https://github.com/ttatus
