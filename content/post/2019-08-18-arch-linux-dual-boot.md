+++
title = "Making Windows and Linux hold hands is interesting"
date = 2019-08-18T16:44:28+03:00
draft = false
weight = 0
tags = ["terminal", "sysops", "productivity", "vim", "OS", "arch", "Linux"]
categories = ["System Administration"]
+++

Around two years ago, I installed Ubuntu onto my laptop, along with the
already existing installation of Windows 10. While the experience of using Linux
certainly gave me way to learn a lot of things that will be *very* useful in my
career as a software developer, there were a few glaring issues with the whole
system, most of which were admittedly my fault, caused by my faulty
installation.

Particularly, the biggest problem was the graphics. My laptop has dual graphics,
an integrated Intel HD Graphics 630 and an NVIDIA Quadro M2200, both which are
fantastic graphics cards for rendering video and for the occasional video
gaming. However, Ubuntu really doesn't handle hybrid graphics well (or, at
least, that's what I thought when I installed it), so I decided, back then, to
disable Hybrid Graphics in the BIOS and just go with the "Discrete Graphics"
option. That was a bad idea. Why?

Well, Windows doesn't like change.

* * *

## Windows is a little baby sometimes

I'm not kidding, every once in a while, Windows likes to really pull tantrums
whenever it sees certain hardware or BIOS changes (I mean, anyone would be angry
if you messed with their "organs"). Since Windows is an operating system
designed on the idea of backwards compatibility and stability at a hardware
level (hence its rise during the driver problem in the late 20th century), every
single change on a hardware level can screw with not only Windows, but
applications that relied on certain hardware optimizations to run.  And of
course, you can imagine the amount of issues that arose when Windows saw that
one graphics card *mysteriously disappeared* (it didn't, but only we knew
that).

Even Ubuntu wasn't liking the disappearance of the integrated graphics card.
While some video games were working, and most applications ran just fine, the
battery life was horrendous, due to the discrete graphics card constantly
running and draining battery at maximum performance. In addition, screen tearing
occurred pretty much all the time, possible due to some misconfiguration in the X
server of the computer. Regardless, the peak of my disapproval with my setup was
the appearance of not only constant glitches on the Windows side (not even the
browser worked well, it would constantly freeze and lock up), but also of my
first ever blue screen:

![My first ever blue screen.](/public/img/my-first-blue-screen.jpg)

At this point, I finally decided it was the last straw. After finally finishing
with high school (yes, I'm done!), completing all of the immediate obligations I
had for my transition to college, and thus finally getting some free time in my
summer vacation, I finally committed to reinstalling my Linux OS.

And then I thought:

> I use the terminal all the time anyway, what if I go with something other than
> Ubuntu?

I know what you're thinking, and yes, that's when I became an Arch Linux user.

I use Arch, btw.

* * *

## Arch Linux is cool

Let me start off by saying that, in my opinion, Arch Linux really isn't for
everyone. However, I would also like to mention that a lot of people think that
Arch Linux is a difficult Linux distribution to use. Today, I would like to
dispel that notion.

For those here that might not know, Arch Linux is a rolling-release distribution
that claims to aim for a "Keep It Simple, Stupid" philosophy. Arch users can be,
well, elitist, but I simply chose Arch Linux not to be elitist, but another
reason:

**Terminals!**

As you know, from my
[previous article](/2019/05/10/back-to-the-basics-a-simple-terminal/),
I thoroughly enjoyed switching to terminals, and Arch Linux is a distribution
designed to be simple and lightweight. Therefore, it allows me to build my
workflow from the ground up, trimming out any fat. It also forces you to learn
the intricacies of most Linux-level abstractions (not on the kernel level,
though). If you want to go even deeper, try Gentoo or Slackware. Even better,
try Linux From Scratch. But for now, I'll settle with Arch.

Also, if you're a DIY kind of guy, Arch will be right up your alley.

* * *

## Time to clean house (I mean PC)

Well, things started safely here. Firstly, I pulled out the hard drive which
contained my Ubuntu installation and backed it up as a disk image:

```
$ dd if=/dev/sda of=Ubuntu-Drive-Backup.img status=progress
```

That part took longer than I expected, to be frank (my external SATA reader was
very bad). I also decided to create a separate disk image for my /home
partition, in order to have all the old documents quickly available whenever I'd
need them:

```
$ dd if=/dev/sda2 of=Ubuntu-Home-Backup.img status=progress
```

After that, I pulled the Ubuntu drive out of my computer, re-enabled "Hybrid
Graphics" in the BIOS and booted Windows. As of that moment, my computer was
exactly the same as in the packaging (with the exception of one 2TB NTFS drive,
but that guy never screwed anything up, now did he?) and, lo and behold, soon
enough, things started to look up.

* * *

## Sometimes, Windows fixes itself

I have had multiple times when I screwed things over in Windows (hey, I was a
kid once, too) and every once in a while, I'll admit that Windows impresses me.
Soon enough, after I returned the computer back to normal, it began fixing a lot
of stuff.

For starters, my browser stopped freezing. My games returned to normal, with no
screen tearing, and my video editor, Adobe Premiere Pro, had its rendering speed
boosted significantly. Before, it'd take 5 minute to render 1 minute of 1080p
video. Now, it was a real time render, 1:1 ratio! Pretty cool! How's that
happening?

Well, drivers and optimizations. Since most of the desktop world uses Windows,
most of software development manpower is devoted to improving performance on
Windows. Some drivers essentially pass over certain restrictions set in place by
operating systems to interact directly with the BIOS (and subsequently, the
hardware), permitting for increased performance. However, this operates under
the assumption that Windows has full control of the computer's hardware (as well
as the computer and drivers being custom built and tuned up) which means no
sharing with potential intruders. And, well, I sort of messed that assumption
up. And here lie my problems.

But this time, I know what I'm doing. Essentially, we leave everything we can
unchanged: no changing of the BIOS settings except for those that are strictly
necessary, no screwing with other settings, and most importantly, making sure
Linux will play nicely with Windows (or rather, the other way around). Now how
do we do that?

* * *

## Let's do it ourselves

Most let installation scripts install their operating system. Not this time.
Arch Linux's installation process is a relatively hands-on operation (at least,
mostly). 80% of the installation process is manual, requiring a person to pay
close attention to the edge cases, covering up any potential issues that might
arise. Luckily, there is this wonderful thing called the
[Arch Wiki](https://wiki.archlinux.org/), a beautiful place where magical things
happen. In the Arch Wiki, there are a myriad of pages filled with help,
documentation, and useful pages to not only fix problems with your Arch Linux
installation, but with recommendations for any kind of software or help you
might need. Cool stuff. After finding the Arch Wiki, I don't think I used Google
to search for Linux help even once (especially because, for some reason, all
Linux articles lead to AskUbuntu).

Installation wasn't very difficult on my computer, since the laptop
configuration I have is relatively standard. I just followed the
[installation guide](https://wiki.archlinux.org/index.php/Installation_guide).
There were only a few issues that needed to be done that weren't so obvious from
the installation guide:

- Secure Boot had to be disabled in the BIOS. To be frank, it's not like it's
  doing much anyway. Theoretically, it's used to ensure no unsigned operating
  systems and drivers are run, but the hassle of signing Arch Linux is huge.
- I made sure to boot the installation image in UEFI mode, and when reaching the
  partitioning step in the installation guide, I mounted the EFI partition
  Windows comes with instead of making a new one. This is essential so as to not
  confuse either Windows or the BIOS. I would highly recommend that you make a
  backup of the EFI partition every time you have a "feature update" on Windows,
  as it **will** screw up your EFI partition (I found out the hard way). To do a
  backup of the EFI partition on Windows, run this command in an Administrator
  PowerShell:

```
> bcdedit /export C:\backup.bcd
```

After that, I finally had an Arch Linux shell! Hooray! And my Windows worked
fine, too!

Of course, having a shell isn't enough. You will need a desktop environment, a
bunch of programs, a terminal emulator...

> Wait, what? Don't those come with the OS?
>
> -You, probably

No, they don't. And I think we all learn that the hard way.

* * *

## OSes have loads of bloat

A base installation of Arch Linux clocks in at around 800 megabytes of disk
space. Now, you probably think that's very small, and rightfully so! I mean,
Windows takes 10 gigabytes of space *at best*, but it'll most likely take more.
The reason why Arch Linux is initially so small is that *it comes installed with
the minimum required for the machine to run*, which is a lot less than you would
expect.

There's no desktop environment, no window manager, none of the stock programs
you'd expect a computer to come with (like a browser). There's just, well...

A shell.

```
[root@ARCHLINUX]:~$
```

Of course, just as I did, you'll probably want more, but the beauty of Arch
Linux is that *you get to pick how much more.* While some may find that
time-consuming and useless, I find it liberating.

* * *

## Remember: read the whole wiki

This is a reminder for you as much as it is for myself, because I also always
forget to read the wiki to find solutions to my problems. It's a huge place, and
I would highly recommend you read all the sections from the ["General
recommendations"](https://wiki.archlinux.org/index.php/General_recommendations)
page, which can help with what to do after finishing the installation process,
and where to go from there. I personally decided to opt for a more
keyboard-centric desktop environment, using the [i3 window
manager](https://github.com/Airblader/i3), the ["st" terminal
emulator](https://st.suckless.org/), and a whole bunch of terminal programs that
are essentially alternatives for desktop applications, but you can find most of
them in my previous article.

For those incredibly curious, here is a screenshot of how it looks now:

![The screenshot of my desktop.](/public/img/screenshot-arch-linux.jpg)

If you would like a similar setup, you can check out [LARBS](https://larbs.xyz),
a script for automatically installing a functional desktop environment with a
keyboard-centric workflow. That is the setup I started with, and tweaked as time
went on to my liking. I would recommend you test it out first with a new user
before actually diving into the whole setup. If you simply install it with no
idea what's awaiting you, it won't be fun.

* * *

## So, does this whole thing work?

Kind of. There are still a few issues with my computer that I will never be able
to fix. For instance, there is no open-source driver that works with my graphics
card, since my graphics card is "experimental" compared to mainstream cards,
which means there's not much support for it. I could install proprietary
drivers, but that's a whole other behemoth that is only fitting for another
time. This essentially means that there are still two tasks that can only be
done on Windows: video editing and video gaming. Fortunately enough, the
times in which I do either almost always never overlap with times I use Linux
(coding, doing anything else).

*Update (2019-09-08): After a bit of browsing around, I ended up fixing the
video gaming problem by installing* [proprietary NVIDIA
drivers](https://wiki.archlinux.org/index.php/NVIDIA) *and then using*
[optimus-manager](https://wiki.archlinux.org/index.php/NVIDIA_Optimus#Using_optimus-manager)
*to allow for switching between graphics cards. There were a few ACPI issues
that were specific to my laptop that I had to fix as well, but hopefully you
won't have them if you try the same thing. When in doubt, read the wiki!*

I'm happy with the way it turned out, though. Compared to the incomprehensible
chaos that was my computer before, now it's clean, lean, and works splendidly.
But even more important is the fact that I love using it now more than ever,
hence why I feel like doing so much more work! That's how everyone should feel
when using a computer. You should feel at home, with the computer being an
extension of you, bending to your will and helping you shape the world.

Maybe you can try changing your computer too, I'm certain you'll feel the same
way.

* * *

If you want help with Arch Linux, check the wiki (gotcha). *But* if you have
questions regarding my setup, and how I'm faring with my new PC, don't hesitate
to email me.

I'm also thinking of making a comment section, but I'll think about it. I don't
have to do it *today*...

*Update (2019-11-24): Comments are live all over the blog!*
