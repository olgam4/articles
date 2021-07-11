# Why Pair Programming Is Dead And Being a Mobster is the New Cool

<img src="https://github.com/olgam4/articles/blob/main/process/mob/4284.jpeg" />

Lately, there definitely a trend of pair programming: just peeking at the most read articles on Medium, and you can't be wrong. I feel like the community is somewhat late and now, we understand more things.

## What is Pair Prog

<img src="https://github.com/olgam4/articles/blob/main/process/mob/SRY_UVS_318-001.jpeg" />

Commonly called 🍐 programming, this technique simply consists of working as a pair on a feature. Usually, one person is focused on the system, the project as a whole and how to implement the latter, whilst the other is typing and thinking about details, the lines if you may. It often is a good idea to switch roles: some people only swear by [Pomodoro](https://en.wikipedia.org/wiki/Pomodoro_Technique) and will recommend switching every 25-30 minutes, but that would deserve an entire article of its own.

I saw some people comparing it to Piano Duos and I liked the idea. Whilst not entirely accurate, it still projects the idea that someone might play the melody and the other could be helping with rythm and bass. Compared to a band, the Piano exists as a single unity and the pair both work on it.

### Why it works

There are a lot of reasons why it works. First, let's gather some facts, shall we?

> An an online survey of pair programmers, 96% of them stated that they enjoyed their work more than when they programmed alone.
>
> Additionally, 95% of the surveyed programmers stated that they were more confident in their solutions when they pair programmed.
>
> Pairs spend about 15% more time on programs than individuals.
>
> However, the resulting code has about 15% fewer defects.
- Rickard Dahlstrom on [Raygun](https://raygun.com/blog/how-good-is-pair-programming-really/)

<img src="https://github.com/olgam4/articles/blob/main/process/mob/driver_navigator.png" />

The afore-mentioned Piano duo is also described as the Driver-Navigator metaphor. One person is focused on the "What" and the "How": the Driver. The other is focused on the same "What", but on the "Why" instead: the Navigator. As some say, two heads are better than one. It might have something to do with the pressure to perform or with better splitting the tasks, but it definitely works. Using the ping-pong method, you will work as both the Driver and the Navigator, letting you reset your focus every few minutes.

<img src="https://github.com/olgam4/articles/blob/main/process/mob/dn5ax0jtfc551.jpeg" width="400" />

It also has been used a recruiting-tool. Why? Because it really is a great tool! You can assert what your interviewee thinks in real time and sometimes, even on a real life project. And then, once you've recruited the person, you can even pair people with different skill sets and skill levels to enhance your team productivity and comprehension. How amazing is that?

### Why It don't

So why am I saying that Pair Programming is dead? Well, first, to catch your attention, but also because I do think we found an upgrade. A real problem with Software Engineering usual Processes is that it is way to easy to split tasks and accumulate Work In Progress (WIP). At first, Pair Programming seemed to solve the problem, but it only did solve some of it. Let's imagine having a team of six people working on a project: if they all work on something different, the WIP is enormous. More often than not, it will mean a merging hell once every one is done. Usually, it is recommended not to diverge too far from the `master` branch. Some will say that it shouldn't be further than `1 Day Work`. So let's say you do 🍐. You've cut your `WIP` to half. But you still have the same dangers as before. One duo may steer away for too long, whilst the other two are shouting at each other because they've merged something which broke everything...

<img src="https://github.com/olgam4/articles/blob/main/process/mob/white-field-photo-ziyhUwkiDnc-unsplash.jpg" />

## So what should i do?

Well...Why not work as a team, but for real? 

MOBSTER

### How do I do it

### Why should I?

#### Walking Skeletons

At the beginning of every project, your team needs to understand the goal of their application. They need to settle down on a solution and find a way to bring a `MVP`. Splitting this job is somewhat odd: there is nothing written, so you're bound to fall into merging hell. Instead, why not work together? Juice up your brains and define a walking skeleton for your project. Once it is walking, you can add muscles, fat and details to your project. This can be easily split up, but putting a skeleton together should always be a team effort.

What is it?

### Its downfalls

At first, it's strange. I feel watched.

My boss says our productivity is falling. Explain that you now have a direct flow.

### Its perks

As said earlier, your `WIP` is stripped down to its minimum.

### During a pandemic

I don't know if you've heard, but the last year has been tainted by a pandemic. Before, you could plug yourself to a tv and have your team gather around it in order to work, but now, how can you do it? Well as most things, nothing beats face-to-face, but there are some wonderful tools to your disposition.

#### [Remote Mob Programming](https://www.remotemobprogramming.org/)
<img src="https://github.com/olgam4/articles/blob/main/process/mob/remotemob_header_screen_grau.png" />

There are a lot of tools which were born last year. This one in particular is quite interesting. It adds timers, codesharing, webcams, everything in a single app. If you want a quick solution with people who aren't especially versed in tech, it could be a perfect fit. Personnaly, I have never used it, but I've only heard praise about it. There are also some other alternatives which strive to do the same thing... But let's talk about some other ones which I prefer.

#### [Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=MS-vsliveshare.vsliveshare)
<img src="https://github.com/olgam4/articles/blob/main/process/mob/vs-code-ls-session.png" />

Visual Studio Code has taken the dev world by storm. Customizable, light and powerful, a lot of people have switched to using it, especially frontend developpers. Some years ago, it added a nice feature: Live Sharing. It lets people connect to your machine remotely and use their Code with yours. You can share buffers, you use your own shortcuts and just like Google Docs, it shows you your friends cursor. Hop on a call and it works wonders. One drawback: back when I used this two years ago, it was sometimes hit or miss. I don't know if Microsoft has upgraded their tool, but I'm sure they did. Sometimes, saving could be difficult and other things like that, but I encourage you to try it out.

#### [Discord](https://discord.com) with good ole' commit and push.
<img src="https://github.com/olgam4/articles/blob/main/process/mob/white-field-photo-ziyhUwkiDnc-unsplash.jpg" />

Personnaly, that is my favourite one to use. Host your server, split your company into rooms and everyone can hop around at will. Share your screens, turn on your webcams and call-in a Music Bot. Discord has a pretty chill vibe too, so you feel less stressed, in my experience. You can also brag to others that you use Vim and don't need to have everyone use the same IDE, which is a total plus. Once you're done with your turn, commit and push a `wip commit` and let someone continue by simpling pulling your work.

This is definitely my favourite solution out there because it is the most versatile. You might need to add plugins to your Discord, but since it lets you do it with bots and whatnot... Well why not?

## So are you convinced?

In the beginning, I told you that pair programming is dead. I think it has evolved: sometimes, doing it might be the solution, but more often that not, mob programming beats it in most ways. Try it with your team. In your next meeting, instead of "thinking and planning what you will be doing in the next few days"... Just share your screen and mob!

---

*Special thanks to:*

[Olivier Lafleur](https://www.linkedin.com/in/olilafleur/)

[Peaky Blinders on Netflix](https://www.netflix.com/title/80002479)

[Roger Delar](https://artuk.org/discover/artworks/one-piano-four-hands-guildford-international-music-festival-13469)

[Martin Fowler](https://martinfowler.com/articles/on-pair-programming.html)
