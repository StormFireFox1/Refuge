+++
title = "Back to the basics: a simple terminal"
date = 2019-05-10T10:42:17+03:00
draft = false
weight = 0
tags = ["development", "terminal", "vim", "tmux", "alias", "productivity"]
categories = []
+++

Ever since the release of Windows' Virtual Desktops, I've found them very
useful. I thought that compartmentalizing every single part of my PC workflow
would be excellent using Virtual Desktops: I could have one desktop for
development, one for my [L.I.F.E Stack](https://blog.stormhub.io/2019/01/20/the-l.i.f.e-stack/),
one for my times when I simply relax (music, chat, et cetera) and that was
pretty much it. Even after my switch from Windows to Linux, it was actually
pretty good in order to stop my constant gliding  between windows and
procrastination, but it soon turned to this:

![A GIF of me just switching between desktops extremely quickly.](/images/switching-desktops.gif)

> I think this was a bad idea.

To be frank, this soon turned in a constant wasting of time of switching
desktops that was not only visually jarring, but also time-wasting and useless,
and it never really stopped me from opening one of the "non-productive" virtual
desktops anyway. So, obviously, I had to do something about it.

I quickly decided that the best thing by far to improving my productivity and
need to multitask by simply constraining myself significantly: no browser, no
more than one virtual desktop, and trying to limit the apps I could open on my
computer at one time without it causing inconveniences to me.

The answer? A terminal!

* * *

## I love terminals!

Honestly, they're super cool. Not only do they make you look like one of those
l33t haxXxors, but they also make it incredibly easy to program with an actual
understanding of the deeper, more intricate aspects of coding that very many
IDEs tend to abstract. I've always been of the opinion that knowing how things
work beneath the cover to be very important, which is why I've always been fond
of terminals.

As such, when the idea struck to convert my entire computer life to one window,
I quickly fell in love with the idea, and I set out and got to work at being
able to make such a thing. I obviously needed 4 basic things to have in a
terminal that would seriously need migration, the rest was merely a distraction:

* my development environment
* my e-mail and chat rooms
* my music
* my journal and L.I.F.E Stack

The first thing I did for my migration, though, is move to a different terminal:
Zsh. While Bash (the default shell for basically everyone) is good, I prefer
Zsh simply due to the [Oh-My-Zsh](https://github.com/robbyrussell/oh-my-zsh/)
project, which is the only plugin "distribution" I actually like.

I have the default theme, along with *very few* plugins: *sudo*, *git* and 
*git-flow*, *npm*, *golang*, and *you-should-use* (reminds me to use the aliases
set in the Zsh configuration). A simple shell for a simple man, and I love it
just the way it is.

![Screenshot of the very simple shell.](/images/a-simple-shell.jpg)

After that, however, I soon realized that I will probably need a bit of help in
order to keep a bunch of terminal programs in one TTY, and the help came in the
form of an old friend of mine: Tmux! Tmux stands for **T**erminal
**Mu**ltiple**x**er and it is the best way to have multiple terminals in one
TTY (better than *screen*, don't @ me). After a bit of configuration, which took
heavy inspirations from [this .tmux.conf](https://github.com/gpakosz/.tmux), I
finally had the ability to have a terminal work as my main desktop. It also
looks cool, and as we all know, style is always a plus.

![A screenshot of my tmux session.](/images/tmux-screenshot.jpg)

Now, on to the development part. I need a text editor. I don't like Nano,
but Emacs is too hard, so what am I left with?

...Oh, no...

* * *

## We meet again, Vim.

Vim! Of course, the biggest enemy of every non-terminal-savvy programmer of
computer user in the **world**. It doesn't matter who you are, you have been
stuck in Vim without being able to quit from it at least once in your computer
science career. At least that's how the joke goes, right?

![Yeah, yeah, we all get stuff in Vim sometimes.](/images/vim-welcome.jpg)

> I don't get it though, it says how to exit it on the welcome screen!

In case you haven't been exposed to it, Vim is a special kind of text editor in
your terminal, notorious for its incredibly weird keybindings that, while
incredibly stupid at first, allow you to write things incredibly quickly after
a while. My first tip would be the `.` command, which allows you to repeat the
last action you've done in Vim, which can be useful if you have to repeat
something throughout your file, like searching for a word. (You do that by
typing `/` and then the word to search in Normal mode, which is the default
one). Believe it or not, Vim actually makes you quite productive if you start
learning it right, even though it takes a long time.

Personally, I've seen a lot of people be scared of it, and for good reason, but
I have two pieces of advice that I found were crucial to not only get me used to
Vim, but also to be productive to it.

Most importantly, no matter what, you must **never** use anyone else's config blindly,
ever. The best and quickest way to be overwhelmed by Vim is to download some
random Vim distribution and use it with no clue as to what it actually does,
what bindings it has and what plugins it installs. I recommend simply starting
off by installing some [sensible Vim defaults](https://github.com/tpope/vim-sensible)
and then adding plugins as you go to your Vim configuration, depending on what
you need. Always follow the "Keep It Simple, Stupid" rule, and grow along with
your Vim configuration. Only add a line in your .vimrc file if you are ever
actually certain you like that settings.

Personally, the only things I found worth adding to default Vim is a Powerline,
the Monokai theme and
[YouCompleteMe](https://github.com/Valloric/YouCompleteMe), an auto-completion
engine that is actually pretty damn good. That being said, vim is now my main
text editor, and I absolutely love it. I write faster than I've ever written
code before.

![A screenshot of my Vim setup on a C++ exercise.](/images/vim-screenshot.jpg)

* * *

## Mail sucks less now, honestly.

By far my most disorganized part of my life was my e-mail. My old Gmail address
looks horrible, and that is excluding the absolute monstrosity that is my Yahoo!
e-mail (whose password I forgot since its creation nearly 9 years ago). I've
always had a problem with sorting my e-mail: I found interfaces cumbersome,
complicated with their automatic labeling. I would miss e-mails, I would screw
up with my categories, and every time I would connect an e-mail client to them,
some part of it would mess up.

This is why, for one thing, I constructed my own mail server (that'll be a story
for another time), and secondly, it's why I started looking for more clean
alternatives to e-mail clients, and where else to go but the terminal.

Meet Neomutt: a fork of Mutt that turns e-mail into a very simple terminal
application. Nothing fancy, just folders, inboxes, and a dead simple interface
for reading and managing e-mail. No more, no less.

![Neomutt in action.](/images/neomutt-screenshot.jpg)

Surprisingly, this has helped not only with my e-mail organization, but also
made me realize that I had some bad e-mail habits. For instance, I used to
always archive everything, no matter what. Now, I read my e-mails, I sort
through them, I trim away whatever newsletters I'm not interested in, etc.
It's actually really nice now, and I enjoy the process.

Configuring Mutt, no matter what, can be a pain, though, which is why I started
with a bit of help. I first inspected to see what
[this Mutt configuration wizard](https://github.com/LukeSmithxyz/mutt-wizard)
would do, and worked from there. I basically have all my e-mails configured
there for now, but I will slowly deprecate my other e-mail addresses to make sure
I don't end up missing e-mails by not checking. In addition, using this
configuration, Neomutt integrates really well with GPG, so I end up having a
super simple process for singing and encrypting e-mails. Overall, I'd recommend
you try it out, too. It might start off badly, but the pace will probably pick
up soon.

* * *

## Spotify in the terminal? No way.

Yeah, I use Spotify for music. I know, it's basic, but it gets the job done.
Unfortunately, there's no officially supported terminal client for Spotify.
Luckily, there's a workaround.

I used [Mopidy](http://mopidy.com/) which is a really cool daemon for the MPD
protocol, the standard way of listening to music from your terminal. Mopidy
comes with a lot of configuration, but I personally simply added to it the
Spotify backend, along with some local music that I didn't have on Spotify. I
did later add a Podcast backend for the very few podcasts I occasionally listen
to, and a scrobbler for Last.fm. However, you're probably asking:

> "But where's the terminal client for the music?

That, my friend, would be
[ncmpcpp](https://wiki.archlinux.org/index.php/ncmpcpp), which is a terminal
client for the MPD protocol. I followed
[this guide](https://medium.com/@theos.space/using-mopidy-with-spotify-and-ncmpcpp-44352f4a2ce8)
to enable the visualizer as well (I wouldn't recommend following the Spotify
part, it's outdated), and that was it! Music in my terminal. Honestly, it looks
pretty cool, too!

![Me listening to music.](/images/tmux-music-screenshot.jpg)

* * *

## Typing my thoughts in the terminal made me revision my previous workflow.

You see, previously, I used Zim for my note-taking. I realized that,
surprisingly enough, even *that* was too complicated. In addition, it lacked a
compatibility layer with my mobile phone, which would've made it easier to write
in my journal. As such, I switched from Zim to [Joplin](https://joplinapp.org/)
for my note-taking. Honestly, it not only works better with cross-platform
stuff (mobile app and all), it's encrypted and can be synced easily. At its
core, it's also essentially a bunch of Markdown notes, so easily exportable.
Migration was easy, since all I had to do was export notes from Zim using
Markdown and import them to Joplin just as easily. Joplin also comes with a
terminal client, so imagine my delight that at this point, 100% of my activities
on my PC could be switched to a terminal fully! Amazing!

![Joplin in action.](/images/joplin-screenshot.jpg)

* * *

## But what about the browser?

Alas, I cannot transfer my browser to a terminal (I mean, I could, but not
fully), and I am ok with that. The problem with web browsers nowadays is that
they let you do anything in the same environment. This means that they're a
jack-of-all-trades, master of none kind of deal. In addition, browsers are the
bane of my existence, since I can oh so easily open a new tab and go on Reddit
or YouTube and waste time doing stuff there. I think that it's best this way.

I've been using this terminal setup on my PC for a while now and I can honestly
say I am incredibly satisfied with it. I know that it's not fancy-looking, and
obviously not particularly advanced (yet, that .vimrc keeps growing), but I'm
certain that, with time, my terminal will keep growing with me, allowing me to
slowly learn to be more effective in it, more effective than ever before.

I don't need all the tools in the world *right now*, I need just enough to get
myself going, and that's all you really need. If you ever need more, you can get
it when you need it, but for now, all I need is a shell.

And honestly, it might be all I ever need.
