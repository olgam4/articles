# Why Pair Programming Is Dead And Being a Mobster is the New Cool

<img src="https://github.com/olgam4/articles/blob/main/process/mob/4284.jpeg?raw=true" />

Lately, there definitely has been a trend of pair programming popping everywhere: just peeking at the most read articles on Medium last month, and you can't say I'm wrong. It feels weird to me, as if our community is somewhat late to the party. As of right now, our processes have changed and pair programming was becoming cool half a decade ago... So what about now? How can you still be hip in your daily job?

## What is Pair Prog

<img src="https://github.com/olgam4/articles/blob/main/process/mob/SRY_UVS_318-001.jpeg?raw=true" width="400" />

First off, let's preface this by talking about the Holy Grail that was Pair Programming back then. Commonly called Pear (🍐) Programming, this technique simply consists of working as a pair on a feature. Usually, one person is focused on the system, the project as a whole and how to implement the latter, whilst the other is typing and thinking about details, the lines if you may. It often is a good idea to switch roles: some people only swear by [Pomodoro](https://en.wikipedia.org/wiki/Pomodoro_Technique) and will recommend switching every 25-30 minutes, but that would deserve an entire article of its own.

I saw some people comparing it to Piano Duos and I liked the idea. Whilst not entirely accurate, it still projects the idea that someone might play the melody and the other could be helping with rythm and bass. Compared to a band, the Piano exists as a single unity and the pair both work on it.

### Why It Works

There are a lot of reasons why it works. First, let's gather some facts, shall we?

> In an online survey of pair programmers, 96% of them stated that they enjoyed their work more than when they programmed alone.
>
> Additionally, 95% of the surveyed programmers stated that they were more confident in their solutions when they pair programmed.
>
> Pairs spend about 15% more time on programs than individuals.
>
> However, the resulting code has about 15% fewer defects.
> 
> IBM reported spending about “$250 million repairing and reinstalling fixes to 30,000 customer-reported problems”. Pair programming significantly reduces these expenses by reducing the defects in the programs.
>
> Pairs typically consider more design alternatives than programmers working alone and arrive at simpler, more maintainable designs. They also catch design defects early.

- Rickard Dahlstrom on [Raygun](https://raygun.com/blog/how-good-is-pair-programming-really/)

<img src="https://github.com/olgam4/articles/blob/main/process/mob/driver_navigator.png?raw=true" width="400" />

The aforementioned Piano duo is described as the Driver-Navigator metaphor. One person is focused on the "What" and the "How": the Driver. The other is focused on the same "What", but on the "Why" instead: the Navigator. As some say, two heads are better than one. It might have something to do with the pressure to perform or with better splitting the tasks, but it definitely works. Using the ping-pong method, you will work as both the Driver and the Navigator, letting you reset your focus every few minutes.

This metaphor is keen to that of driving a car. One person has the map: they focus on long term goals, they focus on the whole road and their itinerary. One person has the driving wheel: they focus on details such as not driving off the road and listen to directions one by one, they focus in the "now". In 🍐, it is the same thing. The Driver implements the now and the Navigator elaborates an itinerary.

<img src="https://github.com/olgam4/articles/blob/main/process/mob/dn5ax0jtfc551.jpeg?raw=true" width="400" />

It also has been used as a recruiting-tool. Why? Because it lets you see how someone thinks, both as a system-person and a detail-person! You can assert what your interviewee thinks in real time and sometimes, even on a real life project. And then, once you've recruited the person, you can even pair people with different skill sets and skill levels to enhance your team productivity and comprehension. How amazing is that?

### Why It Doesn't

So why am I saying that Pair Programming is dead? Well, first, to catch your attention, but also because I do think that with time, we've found an upgrade. A real problem with Software Engineering usual processes is that it is way too easy to split tasks and accumulate [Work In Progress](https://www.atlassian.com/agile/kanban/wip-limits) (WIP). At first, Pair Programming seemed to solve the problem, and whilst it did, it only solved some of it.
Let's imagine having a team of six people working on a project: if they all work on something different, the WIP is enormous. More often than not, it will mean a merging hell once everyone is done. Usually, it is recommended not to diverge too far from the `master` branch. Some will say that it shouldn't be further than `1 Day Work`. So let's say you do 🍐. You've cut your `WIP` to half. (Six people working on six features vs of three pairs working on three.) 
But you still have the same dangers as before. One duo may steer away for too long, whilst the other two duos are shouting at each other because one duo has merged something which broke everything the other 🍐 had been working on...

Another problem which is sometimes easily fixed, is that duos tend to form and last. Alice and Bianca have been working together for six months now, so do Caroline and Daphne. Problem is that A and B are way better at their job. C and D do work better together, but never as well as the other two. You could switch around the people who work together, but that requires some team buidling and management you maybe would not have thought of beforehand.

<img src="https://github.com/olgam4/articles/blob/main/process/mob/white-field-photo-ziyhUwkiDnc-unsplash.jpg?raw=true" width="400" />

## So What Should I Do? Mob!

<img src="https://github.com/olgam4/articles/blob/main/process/mob/EE1alxVWwAMnwy4.jpeg?raw=true" width="400" />

Well...Why not work as a team, but for real? Don't split up: act as one entity, one hive mind. Alice now shares her screen and everyone follows along, either on their own screen or on the big TV screen in a room. No more spelling mistakes, since everyone is watching. It is a great team building tool.

### How Do I Do It

Assign roles. Someone is writing, someone is thinking about the big picture, someone is googling some obscure design pattern they think will be useful in your case and someone reminds you to stick to the red-green-blue of `TDD`. Isn't it awesome? Just as with 🍐, using `Pomodoro` or anything else, you definitely should change Drivers every now and then. It alleviates stress on people’s minds and gives everyone the chance to shine. Actually, in my honest opinion, it is just Pair Programming, but better.

### Why should I?

#### Walking Skeletons

<img src="https://github.com/olgam4/articles/blob/main/process/mob/Spooky_scary_skeleton_wiki.png?raw=true" width="400" />

At the beginning of every project, your team needs to understand the goal of their application. They need to settle down on a solution and find a way to bring a `MVP`. Splitting this job is somewhat odd: there is nothing written, so you're bound to fall into merging hell. Instead, why not work together? Juice up your brains and define a walking skeleton for your project. Once it is walking, you can add muscles, fat and details to your project. This can be easily split up, but putting a skeleton together should always be a team effort.

#### Code Reviews? What Are Those?

It is known that code reviews don't always add as much value as you think they do. Well yes, you do have incredibly good eyesight: fixing typos right and left like there's no tomorrow... But if the Pull Request you're working on is 1000+ lines long...Are you really catching that sneaky security problem at like `654`? If you are, don't be shy to send me your resume. Some solutions to that problem is to limit `PR` to some line maximum, splitting them into meaningful commits et cetera. Another awesome solution is to have everyone reading the code as it is written. Every developer is familiar with it because, well, they've worked on it, and you can still use the solutions talked about earlier. Change Driver every Pomodoro-timelapse. Split your work into simple commits. Do all of it, but as a team.

In the end, you don’t have to integrate and merge your work, because it has been merged at the same time that it has been written. Everybody’s work is in there, so you don’t need to review and learn about what your coworker has done: you’ve done it too. Double-checking yourselves may be a good idea, but test pipelines are made for that. So be gone are the hours and hours of tedious code reviews! 

### Its downfalls

No solution is perfect, so let's talk about some of the problems people working with it have talked about or some of the things you might think will be a problem for you and your team.

At first, it's strange. Some people say that they feel watched. You are: Bob and Daphne are reading everything as you type. But is it really a problem? They would've read it anyways down the line and also, they're not there to judge: they're doing the same thing as you...They're working on your code. It isn't Alice's code (and it never was), your team shares responsibility on it. It is something you might have to work on. In Engineering, when someone builds a huge bridge, it isn't "their" bridge. Working on a critical part of a pacemaker doesn't make it "yours". It still is a team responsibility and Mob Programming might help with that feeling.

Some managers might think that the productivity will drastically fall... But will it? If you know about `WIP Limits`, you know that a very frequent problem with Software Engineering is that its process is very complex and people have trouble grasping its intricacies. Since your whole team is working on ONE feature, `WIP` is going to be reduced to its minimum (less than that and they aren't doing anything). Give it a try! Let your team find their own skills!

This one I thought was funny, so I could not not include it in this article. "Some people might fall asleep." Since you're in the corner of the room whilst everyone else is working, someone might sleep through it. I'm sorry to be the one who tells you this, but if they are sleeping right now, who says that they weren't sleeping when they were alone? Working as a group actually lets you catch "these people". Also, I really hope you don't have to deal with this kind of trouble because it may probably stem from deep problems in your system.

With everything else, it is NOT always a great solution to everything. Please, don't run around using something you found on the internet without planning or thinking about it.
### Its Perks

With downfalls out there, well let me try to convince you that in fact, Mob Programming is awesome.
Onboarding someone is easy! They are part of the team on day one. They see everyone working and can learn from everyone. Also, no more one-man army or "superhero". Everyone on your team is working at the same time, on the same things. If it wasn't clear by now: no more merging hells. You can brag about being part of a mob. Or of a mind hive? Go back and laugh at every innuendo I slipped in here. Please.

I would lie if I say that I don't love Mob Programming. It is an awesome tool to design your architecture, you have insight from everyone and you feel like you are a part of something bigger than you.

### During A Pandemic

I don't know if you've heard, but the last year has been tainted by a pandemic. Before, you could plug yourself to a tv and have your team gather around it in order to work, but now, how can you do it? Well as most things, nothing beats face-to-face, but there are some wonderful tools to your disposition.

#### [Remote Mob Programming](https://www.remotemobprogramming.org/)
<img src="https://github.com/olgam4/articles/blob/main/process/mob/remotemob_header_screen_grau.png?raw=true" />

There are a lot of tools which were born last year. This one puts together a lot of tricks and tools which they use at work. They give timers, codesharing tools, webcams you should buy, everything in a single place. If you want a quick solution with people who aren't especially versed in tech, it could be a perfect fit.

#### [Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=MS-vsliveshare.vsliveshare)
<img src="https://github.com/olgam4/articles/blob/main/process/mob/vs-code-ls-session.png?raw=true" />

Visual Studio Code has taken the dev world by storm. Customizable, light and powerful, a lot of people have switched to using it, especially frontend developers. Some years ago, it added a nice feature: Live Sharing. It lets people connect to your machine remotely and use their Code with yours. You can share buffers, you use your own shortcuts and just like Google Docs, it shows you your friends cursor. Hop on a call and it works wonders. One drawback: back when I used this two years ago, it was sometimes hit or miss. I know that with the pandemic, they have upgraded their tool. Sometimes, saving could prove to be difficult, so make sure to save your code, but other than that, do give it a try!.

#### [Discord](https://discord.com) with good ole' commit and push.
<img src="https://github.com/olgam4/articles/blob/main/process/mob/external-room-discord_2x_yoi7kh.jpeg?raw=true" />

Personally, that is my favourite one to use. Host your server, split your company into rooms and everyone can hop around at will. Share your screens, turn on your webcams and call-in a Music Bot. Discord has a pretty chill vibe too, so you feel less stressed, in my experience. You can also brag to others that you use Vim and don't need to have everyone use the same IDE, which is a total plus. Once you're done with your turn, commit and push a `wip commit` and let someone continue by simply pulling your work.

This is definitely my favourite solution out there because it is the most versatile. You might need to add plugins to your Discord, but since it lets you do it with bots and whatnot... Well why not?

## So are you convinced?

In the beginning, I told you that pair programming is dead. I think it has evolved: sometimes, doing it might be the solution, but more often that not, mob programming beats it in most ways. Try it with your team. In your next meeting, instead of "thinking and planning what you will be doing in the next few days"... Just share your screen and mob!

---
TW: mob, it has been used lightheartedly
---

*Special thanks to:*

[Olivier Lafleur](https://www.linkedin.com/in/olilafleur/)

[Peaky Blinders on Netflix](https://www.netflix.com/title/80002479)

[Roger Delar](https://artuk.org/discover/artworks/one-piano-four-hands-guildford-international-music-festival-13469)

[Martin Fowler](https://martinfowler.com/articles/on-pair-programming.html)
