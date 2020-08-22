+++
title = "Keeping Everything Together"
description = "A file containing all blog posts written in Org for the Refuge."
date = 2020-08-04
draft = false
tags = ["productivity", "software", "tools", "coding"]
category = ["Lifestyle"]
+++

Recently, I had a bit of a pickle with my task management.

Yeah, I know, if you've read about my [L.I.F.E Stack](https://blog.stormhub.io/2019/01/20/the-l.i.f.e-stack/), you'd think I'm pretty fine
at sorting out this sort of stuff. While the actual stack's components have
changed a lot, much of the actual ideas behind it have not, so I'm fine there.
But the tools used to maintain the Stack have always fallen short by a bit,
particularly in the cohesion department.

**Everything is always too different! Why?**

Recently, for example, I've taken to [Todoist](https://todoist.com) as a task manager and [Notion](https://notion.so) as a
knowledge base/note-taker, but their absolute disparity killed me. Even though
Todoist has an amazing API, Notion doesn't, and integrating them was hard. While
I could've tried using Notion as a task manager instead of Todoist, its handling
of tasks is bad-you only have the option to use checkboxes and Kanban boards,
both of which I've tried and haven't been satisfactory for me. The biggest pet
peeve is also simple; **why can't I search for tasks _specifically_?**

Regardless, I began searching for alternatives that could work better for me, as
I've been doing for a while. I needed something that could keep as much of my
Stack together as possible; tasks, time tracking, health, notes, all of it.

> Is that even possible?

During my search for a more universal way of keeping everything together,
though, I reminded myself of the one thing I always heard that could supposedly
do everything cohesively: Emacs.

Wait, _Emacs?_ Oh no.

## This is how I become an Emacs user

Admittedly, I expected this. I use Vim and Vim keybindings for pretty much
everything, and who's to say I won't go deeper? (Some might say [Emacs is less
elitist than Vim](https://xkcd.com/378))

For the unexposed (good for you, honestly), GNU Emacs is a text editor with one
single premise: everything is customizable. The idea is that you extend it using
its own language, Emacs Lisp. Regardless, I was not interested in diving full
head on deep into what is by far the most complex text editor out there
nowadays, and neither would that make for an original post (there are millions
of them at this point, honestly) so I began with an "Emacs distribution".

An "Emacs distribution" just takes care of the majority of the configuration
you'd likely already be using (package management, themes, etc.) and puts it in
a nice package. Really, I like the distributions because they give you a good
starter on packages to try out and explore; perfect for someone diving into
Emacs out of nowhere.

![Screenshot of Doom Emacs.](/images/doom-emacs-screenshot.png)

Anyway, in short, I first tried out [Spacemacs](https://www.spacemacs.org/). Honestly, it looks amazing and
has fantastic support for a lot of applications and packages in the community.
It's a great starter kit and it even has Vim keybindings out of the box! [Doom Emacs](https://github.com/hlissner/doom-emacs)
was my later stop because of its sheer speed. Spacemacs had too much
abstraction upon it, while Doom Emacs is closer to the bare-bones a bit, so it
made for a better experience for a slightly more involved tinkerer.

I will concede that I think the biggest obstacles to Emacs are the configuration
and the keybindings. The keybindings of the original Emacs are easily avoided
using `evil-mode`, which is essentially Vim keybindings in Emacs. However, the
configuration is definitely the biggest obstacle to this program. It ends up
being a more involved version of installing extensions to VS Code (to which
Emacs is comparable, but in my opinion far more customizable).

Regardless, once I stopped getting distracted by my new shiny toy, I opted to
return to my original objective. Now, to move my L.I.F.E Stack to a cohesive
system, I needed to find good alternatives to everything. I began digging to see
what options I had.

Well, I quickly discovered that Emacs _really_ is an OS, not a text editor.

## Emacs has _everything_

When I started digging for what options I had available in terms of apps and
whatnot, I realized there was almost _everything_ in this text editor. And I
really mean it!

The first packages were obvious; I needed modules for programming languages like
C, Go, Java, JavaScript or Typescript, take your pick. I also started installing
other packages related to these like auto-completion frameworks (Helm is the
best). But then is where all the wild options began appearing.

First one was mu4e, one of the more popular email clients for Emacs. While I
[have used terminal mail clients before](https://blog.stormhub.io/2019/05/10/back-to-the-basics-a-simple-terminal/#mail-sucks-less-now-honestly), it was a surprise to find a client
_inside_ the text editor. Configuring it was not as hard as the tutorials
online, as I already had email configured for the command line, but once it was
all well and done, it was amazing.

The real advantage of having email in Emacs was just the sheer speed of reading
it. Much like my previous mail client, it's all text, which removes a lot of
distracting content. It's also super quick at searching and handling mail.

Nothing beats the feeling of nuking 500 emails using only three keys: `d` and `x y`.

- `d` marks email for trashing (sends to Trash folder)
- `x` enables mark execution (executes action marked before, like delete)
- `y` confirms your execution

Done. Observe.

![Video of nuking 65 mails.](/videos/MailNuke.gif)

Absolutely beautiful.

There were also even more packages that I couldn't believe I found, like a
[**Spotify client**](https://github.com/danielfm/spotify.el). Honestly, it's kind of hilarious this even exists, but also
believable at this point; Emacs really has everything. It ends up being pretty useful
as well, and subtle. I can just change tracks in my playlist from within my editor,
even if I'm playing music on another device (Spotify Connect for the win).

![Screenshot of spotify.el](/images/spotify-el-screenshot.png)

There's also an amazing package in Emacs, _Magit_, that is essentially Git in Emacs.
It's an _amazing_ interface for the Git CLI, and probably the most comprehensive one.
Frankly, it is one of the closest things you can get to idiomatic Git usage in a non-CLI
interface. It also has support for GitHub issues and PR's, if you configure it right.
You can even do GitHub PR reviews straight within Magit as well, with the help of another
package:

![Screenshot of Magit.](/images/magit-screenshot.png)

There are some other packages I've installed, like an [RSS reader](https://github.com/skeeto/elfeed), all of which
have nice Vim keybindings and are all configured all in the same place. The cohesion
began showing as well; my tendency to switch workspaces while working decreased a lot
as I was using Emacs, because I didn't have much of a need to switch anymore. Unless
I procrastinated, but that's a different problem entirely. This all culminated with
the bread and butter of Emacs, and pretty much the main reason I even considered it
in the first place.

## Org Mode: The Digital Paper

> Organize your Life in Plain Text

_Why is this the main tag?_

Org Mode is a set of packages for Emacs that allows for some tightly-knit
features surrounding a plain-text format, Org files. In particular, these
features focus on task and project management, time tracking, outlining,
writing, literate programming and more.

The main marketing tag of Org Mode is, in my opinion, a bit disingenuous to the
actual reason why Org Mode is really good. I don't think it really has to do
with Org Mode being powerful in tooling. After all, pretty much all applications
nowadays run on SQL databases with fancy user interfaces and amazing sorting and
filtering capabilities. Turns out that the reason Org mode is good is because it
shares an advantage with the best tool for organizing your life you can possibly
use: _paper_.

Paper is free-form, paper is blank, paper is a canvas. It gives you absolute
freedom to do whatever you want with it. I've recently gone around to
recommending prospective individuals to use paper as a starter point with
organization, since it gives you the freedom to forge proper habits with your
brain. Instead of molding your amazingly efficient brain to a primitive tooling,
why not mold your tools to fit you specifically? Paper is the ultimate canvas
for that.

The only thing that gets close to paper on a PC is plain text. Admittedly, you
can't draw on it, but there are replacements to drawing; images, LaTeX, take
your pick. One could argue that other software does the job of [mimicking paper
better](https://www.microsoft.com/en/microsoft-365/onenote/digital-note-taking-app), but it's not as good as plain text. With plain text, there's nothing.
Just you and the file. Kind of like you and the paper, pen in hand. Sure, you
can create common structures on the piece of paper, like checklists and headers,
or charts, but you don't have to. It's as free as you can get.

Org Mode is, in my opinion, probably the best set of tooling built upon plain
text. It expands the physical aspect of paper (or plain text, in this case), and
leverages a computer's inherent capabilities to _make paper better._ **This** is
why Org Mode is amazing. It's the absolute best set of capabilities built upon
paper!

Ok, you probably need proof. Examples, stuff like that. We'll start with that.

## Playing with the Digital Paper

First, let's get a new piece of "paper".

```bash
emacs brand-new-side-project.org
```

Empty canvas, free for us to lay down our thoughts. So, what do we do? Suppose
we are whipping up a plan for our brand new side-project, we come up with some ideas
we write down.

```org
Ok, so I had this idea to do a specific thing.
I also had this other idea.
Oh, wait, I could also do this easy thing in a couple of hours to get started.

Oh, I also found this weird link online that would help me: https://example.com
```

Alright, so we have the ideas. It's nice, quick to use and good enough, perhaps?
Maybe that's all you need, writing ideas down and keeping them in one file. No
more complexity, just a file you check later; for most, that's really enough.
But suppose you want some more structure; we can begin using the Org Mode
conventions.

First off, we'll split these ideas in different sections. Good to
compartmentalize; we'll use headers, essentially. In Org Mode, they're items,
but they achieve the same thing.

Just add an `*` next to the section title and that's it, you get a header:

```org
 * First idea
   Ok, so I had this idea to do a specific thing.

 * Second idea
   I also had this other idea.

 * I could also do this easy thing in a couple of hours to get started.

 * Oh, I also found this weird link online that would help me: https://example.com
```

In Org Mode, you can also just press `TAB` inside a header and hide the
contents temporarily, which makes for easy focus on specific sections. Tab the
second idea, which we think isn't as important, and it looks like this:

```org
 * First idea
   Ok, so I had this idea to do a specific thing.

 * Second idea...

 * I could also do this easy thing in a couple of hours to get started.

 * Oh, I also found this weird link online that would help me: https://example.com
```

Now we notice there's an item that is actionable, a task. We can mark it as one by adding
`TODO` before its title. So let's do that:

```org
 * First idea
   Ok, so I had this idea to do a specific thing.

 * Second idea...

 * TODO I could also do this easy thing in a couple of hours to get started.

 * Oh, I also found this weird link online that would help me: https://example.com
```

`TODO` ends up highlighted so it grabs your attention, and you can just change
it to `DONE`. To-do list is now made.

What about keeping track of all of your tasks across multiple files, which is something
Notion is horrible at?[^fn:1] You can use `org-agenda` after configuring
it slightly and you get a full week view of all your tasks.

![Screenshot of Org Agenda.](/images/org-agenda-screenshot.png)

> Only 5 minutes and we've overtaken Notion in terms of functionality[^fn:2].

This is the absolute tip of the iceberg of Org mode's functionality, and there are a lot
of other features, tools, and packages that Org mode has that put it above and beyond
most organizational tools out there; exports in any format, time-tracking, calendar syncing,
mobile syncing, contacts management, the list goes on as much as MELPA does.

In my opinion, you shouldn't care about all that at first; Org Mode is already
good enough in this short 5 minute tutorial, and the reality is you will
probably not use 100% of Org mode's features. But the point is simple; the
features expand upon the plain text format and create as close to a experience
on paper as possible, while leveraging the capabilities of a computer in an efficient
manner; searching, file system sorting, and the sheer performance of editor software.

But back from the massive sidetrack that was Org Mode, I really want to point
out Emacs' and Org Mode's best capability, which is the peak of putting everything together.

## The Open Source Ecosystem

I don't think I've experienced an ecosystem lock-in outside of proprietary
companies that feels like Emacs. Sure, you might think that's debilitating, but,
for example Apple has a fantastic ecosystem that cannot be beaten. Similarly,
Emacs has a tight-knit ecosystem which can do a lot of things at once; music,
email, tasks, coding, writing, a multitude of text-based creative activities in
one place, with the same set of keys and zero context switching. There are
packages such as `org-capture` that let you save tasks or items in Org files
from pretty much anywhere, and link to the origin point. For instance, you can
link to files or emails directly from your Org files.

Yes, these probably only work properly in Emacs and your specific configuration,
but as opposed to most ecosystems, this is one you own and one _you can change!_
Emacs Lisp is not hard to learn and you can quickly whip up your own changes
to fit the way you work, which can be beaten by nothing else. Additionally, Emacs
is open source, so it's never going away.

Is it fancy-looking like other apps out there? Not really (although there are
themes), but looks really do not concern me; functionality is imperative. And,
in all honesty, Emacs does this really well.

Everything is together, I can finally rest.

Hopefully I don't spend too much time configuring Emacs.

---

_Fun fact: This entire blog post was written solely in Emacs._ Not only was the Git
commit process in Emacs using Magit, so was the written blog file (exported to Markdown for my
blog using `ox-hugo`) and the refreshing of the blog page, using a terminal emulator
inside of Emacs. I never left my Emacs frame while writing this.

Proves to show you can do a lot within it.

[^fn:1]: I am talking about checkboxes here, pages are searchable, but my particular point still stands; tasks are not first-class citizens in Notion like items are in Org mode.
[^fn:2]: I am not going to pretend Org mode is better than Notion in every way here, but in terms of strict functionality, I'm of the opinion Org mode beats Notion in most things. Notion does have a better UI, and it also has collaborative tools, but asides from that, Org mode has feature parity, if not overtaking Notion (see `org-babel`, which is Jupyter notebooks in Org Mode.)
